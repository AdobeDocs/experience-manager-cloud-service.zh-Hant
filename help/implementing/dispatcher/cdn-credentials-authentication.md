---
title: 設定CDN認證和驗證
description: 瞭解如何在設定檔案中宣告規則，再使用Cloud Manager設定管道來部署，以設定CDN憑證和驗證。
feature: Dispatcher
source-git-commit: ee993798739232da794dbf7ff0a643ca93effa7d
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 1%

---

# 設定CDN認證和驗證 {#cdn-credentials-authentication}

>[!NOTE]
>此功能尚未正式推出。若要加入率先採用者計畫，請傳送電子郵件至 `aemcs-cdn-config-adopter@adobe.com`.

Adobe提供的CDN具有多項功能和服務，部分功能和服務需仰賴憑證和驗證，以確保適當等級的企業安全性。 透過在使用部署的組態檔中宣告規則 [Cloud Manager設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)，客戶可自助設定下列專案：

* AdobeCDN用來驗證來自客戶管理CDN之請求的HTTP標題值。
* 用來清除CDN快取中資源的API權杖。

各項（包括設定語法）將於下文其本身的章節中說明。 此 [通用設定](#common-setup) 一節會說明兩者通用的設定以及部署。 最後，本節將說明如何 [旋轉鍵](#rotating-secrets)，這被視為良好的安全性實務。

## 客戶管理的CDN HTTP標頭值 {#CDN-HTTP-value}

如 [AEMas a Cloud Service的CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) 頁面，客戶可選擇透過自己的CDN （亦稱為客戶CDN，有時稱為BYOCDN）來路由流量。

在設定過程中，AdobeCDN和客戶CDN必須就 `X-AEM-Edge-Key` HTTP標頭。 此值是在每個請求中在客戶CDN處設定的，之後再傳送至AdobeCDN，由其驗證值是否如預期般符合，因此它可以信任其他HTTP標頭，包括有助於將請求傳送至適當AEM來源的那些標頭。

此 `X-AEM-Edge-Key` 值會以下列語法宣告。 請參閱 [通用設定](#common-setup) 一節以瞭解如何部署它。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
      - name: edge-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_052824}}
        edgeKey2: ${{CDN_EDGEKEY_041425}}
        onFailure: log # optional, default: log, enum: log/block
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

的語法 `X-AEM-Edge-Key` 值包括：

* 種類、版本和中繼資料。
* 包含子項的資料節點 `experimental_authentication` 節點（釋放特徵時，會移除實驗性前置詞）。
* 在experimental_authentication下，具有一個驗證器節點和一個規則節點，兩者都是陣列。
* 驗證者：可讓您宣告權杖或認證的型別，在此例中是邊緣金鑰。 其內容包含下列屬性：
   * name — 描述性字串。
   * 型別 — 必須為edge。
   * edgeKey1 — 其值必須參考秘密權杖，該權杖不應儲存在git中，而是宣告為 [Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md) 型別密碼的。 在「已套用服務」欄位中，選取全部。 建議使用的值(例如`${{CDN_EDGEKEY_052824}}`)反映新增日期。
   * edgeKey2 — 用於輪換秘密，相關說明請參閱 [旋轉秘密區段](#rotating-secrets) 底下。 至少一個 `edgeKey1` 和 `edgeKey2` 必須宣告。
   * OnFailure — 定義動作，可以 `log` 或 `block`，當請求不符合以下任一值時： `edgeKey1` 或 `edgeKey2`. 的 `log`，將會繼續處理請求，而 `block` 將產生403錯誤。 此 `log` 在即時網站上測試新Token時，值相當實用，因為您可以先確認CDN可正確接受新Token，然後再變更為 `block` 模式；也能減少客戶CDN與AdobeCDN之間因設定錯誤而中斷連線的機會。
* 規則：可讓您宣告應該使用哪一個驗證器，以及它是否用於發佈和/或預覽層。  內容包括：
   * name — 描述性字串。
   * when — 根據 [流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) 文章。 通常會包含目前階層的比較（例如publish），以便驗證所有即時流量為透過客戶CDN的路由。
   * 動作 — 必須指定「authenticate」，並參考所要的驗證者。

>[!NOTE]
>Edge金鑰必須設定為 [Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md) 型別變數 `secret`，然後才部署參考的設定。

## 清除API Token {#purge-API-token}

客戶可以使用宣告的清除API權杖來清除CDN快取。 使用下列語法來宣告權杖。  請參閱 [通用設定](#common-setup) 一節以瞭解如何部署它。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
       - name: purge-auth
         type: purge
         purgeKey1: ${{CDN_PURGEKEY_031224}}
         purgeKey2: ${{CDN_PURGEKEY_021225}}
    rules:
     - name: purge-auth-rule
       when: { reqProperty: tier, equals: "publish" }
       action:
         type: authenticate
         authenticator: purge-auth
```

語法包括：

* 種類、版本和中繼資料。
* 包含子項的資料節點 `experimental_authentication` 節點（釋放特徵時，會移除實驗性前置詞）。
* 在 `experimental_authentication`，單一驗證者節點。
* 驗證者：可讓您宣告權杖或認證的型別，在此例中為清除金鑰。 包含下列屬性：
   * name — 描述性字串。
   * 型別 — 必須是永久刪除。
   * purgeKey1 — 其值必須參考秘密權杖，該權杖不應儲存在git中，而是宣告為 [Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md) 型別 `secret`.
   * 在「已套用服務」欄位中，選取全部。 建議使用的值(例如 `${{CDN_PURGEKEY_031224}}`)反映新增日期。
   * purgeKey2 — 用於輪換秘密，詳情請參閱 [旋轉秘密區段](#rotating-secrets) 一節。 至少一個 `purgeKey1` 和 `purgeKey2` 必須宣告。
* 規則：可讓您宣告應該使用哪一個驗證器，以及它是否用於發佈和/或預覽層。  內容包括：
   * 名稱 — 描述性字串
   * when — 根據 [流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) 文章。 通常包括目前階層的比較（例如，發佈）。
   * 動作 — 必須指定「authenticate」，並參考所要的驗證者。

>[!NOTE]
>Edge金鑰必須設定為 [Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md) 型別變數 `secret`，然後才部署參考的設定。

## 通用設定 {#common-setup}

所有驗證器的設定如下：

* 首先，在Git專案的頂層資料夾中建立下列資料夾和檔案結構：

```
config/
     cdn.yaml
```

* 其次， `cdn.yaml` 設定檔應包含下列範例中說明的節點。 此 `kind` 屬性應設為 `CDN` 而版本應設為結構描述版本，目前為 `1`. 中繼資料節點具有「envTypes」屬性，可指示將在哪些環境型別（開發、階段、生產）上評估此組態。

* 最後，在Cloud Manager中建立目標部署設定管道。 另請參閱 [設定生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 和 [設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

請注意：

* RDE目前不支援設定管道。
* 您可以使用 `yq` 在本機驗證設定檔的 YAML 格式 (例如 `yq cdn.yaml`)。

## 旋轉密碼 {#rotating-secrets}

不定期變更認證是很好的安全性做法。 雖然清除金鑰使用相同的策略，但還是可以透過邊緣金鑰的範例來達到此目的。

* 剛剛 `edgeKey1` 已定義，在此案例中為 `${{CDN_EDGEKEY_052824}}`，此為建議的慣例，會反映建立日期。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* 輪換金鑰時，請建立新的Cloud Manager密碼，例如 `${{CDN_EDGEKEY_041425}}`.
* 在設定中，從參照 `edgeKey2` 和部署。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* 確定舊的Edge金鑰不再使用後，透過移除來移除它 `edgeKey1` 從設定。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* 刪除舊密碼參考(`${{CDN_EDGEKEY_052824}}`)並部署。
* 準備好進行下一次旋轉時，請遵循相同的程式，不過這次您將新增 `edgeKey1` 對於設定，參考新的Cloud Manager環境秘密，例如， `${{CDN_EDGEKEY_031426}}`.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
