---
title: 設定內容傳遞網路憑證和身份驗證
description: 瞭解如何在設定檔案中宣告規則，再使用Cloud Manager設定管道來部署，以設定CDN憑證和驗證。
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 73d0a4a73a3e97a91b2276c86d3ed1324de8c361
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 3%

---

# 設定內容傳遞網路憑證和身份驗證 {#cdn-credentials-authentication}

>[!NOTE]
>此功能尚未正式推出。若要加入早期採用者計畫，請傳送電子郵件至`aemcs-cdn-config-adopter@adobe.com`。

Adobe提供的CDN具有多項功能和服務，部分功能和服務需仰賴憑證和驗證，以確保適當等級的企業安全性。 透過在使用[Cloud Manager設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)部署的設定檔案中宣告規則，客戶可以自助方式設定下列專案：

* AdobeCDN用來驗證來自客戶管理CDN之請求的HTTP標題值。
* 用來清除CDN快取中資源的API權杖。
* 透過提交基本驗證表單，可存取受限制內容的使用者名稱/密碼組合清單。


各項（包括設定語法）將於下文其本身的章節中說明。 「[通用設定](#common-setup)」區段說明兩者的通用設定以及部署。 最後，還有如何[旋轉金鑰](#rotating-secrets)的章節，這被視為良好的安全性作法。

## 客戶管理的CDN HTTP標頭值 {#CDN-HTTP-value}

如AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)頁面中的[CDN中所述，客戶可以選擇透過自己的CDN路由流量，這稱為「客戶CDN」（有時也稱為BYOCDN）。

在設定過程中，AdobeCDN和客戶CDN必須同意`X-AEM-Edge-Key` HTTP標頭的值。 此值是在每個請求中在客戶CDN處設定的，之後再傳送至AdobeCDN，由其驗證值是否如預期般符合，因此它可以信任其他HTTP標頭，包括有助於將請求傳送至適當AEM來源的那些標頭。

`X-AEM-Edge-Key`值是以下列語法宣告，實際值由edgeKey1和edgeKey2屬性參照。 請參閱[通用設定](#common-setup)一節，瞭解如何部署設定。

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
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

`X-AEM-Edge-Key`值的語法包括：

* 種類、版本和中繼資料。
* 包含子`experimental_authentication`節點的資料節點（釋放功能時，會移除實驗首碼）。
* 在`experimental_authentication`底下，有一個`authenticators`節點和一個`rules`節點，兩者都是陣列。
* 驗證者：可讓您宣告權杖或認證的型別，在此例中是邊緣金鑰。 其內容包含下列屬性：
   * name — 描述性字串。
   * 型別 — 必須是`edge`。
   * edgeKey1 - *X-AEM-Edge-Key*&#x200B;的值，它必須參考不應儲存在git中的機密權杖，而是宣告為型別機密的[Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md)。 在「已套用服務」欄位中，選取全部。 建議值（例如，`${{CDN_EDGEKEY_052824}}`）反映新增日期。
   * edgeKey2 — 用於旋轉機密，如下面的[旋轉機密區段](#rotating-secrets)所述。 定義方式與edgeKey1類似。 至少必須宣告`edgeKey1`和`edgeKey2`其中之一。
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* 規則：可讓您宣告應該使用哪一個驗證器，以及它是否用於發佈和/或預覽層。  內容包括：
   * name — 描述性字串。
   * when — 根據[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)文章中的語法，決定何時應該評估規則的條件。 通常會包含目前階層的比較（例如publish），以便驗證所有即時流量為透過客戶CDN的路由。
   * 動作 — 必須指定「authenticate」，並參考所要的驗證者。

>[!NOTE]
>在部署參考Edge金鑰的組態之前，必須先將其設定為型別`secret`的[Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md)變數（已針對套用的服務選取&#x200B;*全部*）。

## 清除API Token {#purge-API-token}

客戶可以使用宣告的清除API權杖[清除CDN快取](/help/implementing/dispatcher/cdn-cache-purge.md)。 使用下列語法來宣告權杖。  請參閱[通用設定](#common-setup)一節，瞭解如何部署它。

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
* 包含子`experimental_authentication`節點的資料節點（釋放功能時，將會移除實驗首碼）。
* 在`experimental_authentication`底下，有一個`authenticators`節點和一個`rules`節點，兩者都是陣列。
* 驗證者：可讓您宣告權杖或認證的型別，在此例中為清除金鑰。 其內容包含下列屬性：
   * name — 描述性字串。
   * 型別 — 必須是永久刪除。
   * purgeKey1 — 其值必須參考不應儲存在git中的機密權杖，而是宣告為型別`secret`的[Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md)。
   * 在「已套用服務」欄位中，選取全部。 建議值（例如`${{CDN_PURGEKEY_031224}}`）反映新增日期。
   * purgeKey2 — 用於輪換密碼，如下面的[輪換密碼區段](#rotating-secrets)部分所述。 至少必須宣告`purgeKey1`和`purgeKey2`其中之一。
* 規則：可讓您宣告應該使用哪一個驗證器，以及它是否用於發佈和/或預覽層。  內容包括：
   * 名稱 — 描述性字串
   * when — 根據[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)文章中的語法，決定何時應該評估規則的條件。 通常包括目前階層的比較（例如，發佈）。
   * 動作 — 必須指定「authenticate」，並參考所要的驗證者。

>[!NOTE]
>在部署參考Edge金鑰的組態之前，必須先將其設定為型別`secret`的[Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md)變數。

## 基本驗證 {#basic-auth}

透過彈出要求使用者名稱和密碼的基本驗證對話方塊來保護某些內容資源。此功能主要用於輕度驗證使用案例（例如業務利害關係人審查內容），而不是作為一般使用者存取權的完整解決方案。

一般使用者會看到基本驗證對話方塊突然出現，如下所示：

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


語法會依照下方所述進行宣告。 如需如何部署的資訊，請參閱下面的[通用設定](#common-setup)一節。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
       - name: my-basic-authenticator
         type: basic
         credentials:
           - user: johndoe
             password: ${{JOHN_DOE_PASSWORD}}
           - user: janedoe
             password: ${{JANE_DOE_PASSWORD}}
    rules:
       - name: basic-auth-rule
         when: { reqProperty: path, like: "/summercampaign" }
         action:
           type: authenticate
           authenticator: my-basic-authenticator
```

語法包括：

* 種類、版本和中繼資料。
* 包含`experimental_authentication`節點的資料節點（釋放功能時會移除實驗首碼）。
* 在`experimental_authentication`底下，有一個`authenticators`節點和一個`rules`節點，兩者都是陣列。
* 驗證者：在此案例中，會宣告基本驗證者，其結構如下：
   * 名稱 — 描述性字串
   * 型別 — 必須是`basic`
   * 認證陣列，每個認證包括下列名稱/值組，一般使用者可在基本驗證對話方塊中輸入：
      * user — 使用者的名稱
      * 密碼 — 其值必須參考不應儲存在git中的機密權杖，而是宣告為機密型別的Cloud Manager環境變數（已選取&#x200B;**所有**&#x200B;作為服務欄位）
* 規則：可讓您宣告應使用哪些驗證者，以及應保護哪些資源。 每個規則包含：
   * 名稱 — 描述性字串
   * when — 根據[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)文章中的語法，決定何時應該評估規則的條件。 通常會包含發佈層級或特定路徑的比較。
   * 動作 — 必須指定「authenticate」，並參考所要的驗證者，這是此情境的基本驗證

>[!NOTE]
>在部署參考Edge金鑰的組態之前，必須先將其設定為型別`secret`的[Cloud Manager環境變數](/help/implementing/cloud-manager/environment-variables.md)變數。

## 通用設定 {#common-setup}

所有驗證器的設定如下：

* 首先，在Git專案的頂層資料夾中建立下列資料夾和檔案結構：

```
config/
     cdn.yaml
```

* 其次，`cdn.yaml`設定檔應該包含下列範例中說明的節點。 `kind`屬性應該設定為`CDN`，而版本應該設定為結構描述版本，目前為`1`。 中繼資料節點具有「envTypes」屬性，可指示將在哪些環境型別（開發、階段、生產）上評估此組態。

* 最後，在Cloud Manager中建立目標部署設定管道。 請參閱[設定生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)和[設定非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。

請注意：

* RDE目前不支援設定管道。
* 您可以使用 `yq` 在本機驗證設定檔的 YAML 格式 (例如 `yq cdn.yaml`)。

## 旋轉密碼 {#rotating-secrets}

不定期變更認證是很好的安全性做法。 雖然清除金鑰使用相同的策略，但還是可以透過邊緣金鑰的範例來達到此目的。

* 一開始只定義了`edgeKey1`，在此案例中是參考為`${{CDN_EDGEKEY_052824}}`，這作為建議的慣例，會反映其建立日期。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* 輪換金鑰時，請建立新的Cloud Manager密碼，例如`${{CDN_EDGEKEY_041425}}`。
* 在設定中，從`edgeKey2`參照並部署。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* 一旦確定不再使用舊的Edge金鑰，請從設定中移除`edgeKey1`以將其移除。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* 從Cloud Manager刪除舊密碼參考(`${{CDN_EDGEKEY_052824}}`)並進行部署。
* 準備好進行下一次輪換時，請遵循相同的程式，不過這次您會新增`edgeKey1`至組態，並參考名為的新Cloud Manager環境密碼，例如`${{CDN_EDGEKEY_031426}}`。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
