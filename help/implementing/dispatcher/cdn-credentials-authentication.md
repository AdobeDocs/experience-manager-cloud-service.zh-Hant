---
title: 設定內容傳遞網路憑證和身份驗證
description: 瞭解如何在設定檔案中宣告規則，再使用Cloud Manager設定管道來部署，以設定CDN憑證和驗證。
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: e8c40d6205bfa2de18374e5161fe0fea42c8ce32
workflow-type: tm+mt
source-wordcount: '1283'
ht-degree: 5%

---


# 設定內容傳遞網路憑證和身份驗證 {#cdn-credentials-authentication}

Adobe提供的CDN具有多項功能和服務，部分功能和服務需仰賴憑證和驗證，以確保適當等級的企業安全性。 透過在使用Cloud Manager [設定管道部署的設定檔案中宣告規則，](/help/operations/config-pipeline.md)客戶可以自助方式設定以下專案：

* AdobeCDN用來驗證來自客戶管理CDN之請求的X-AEM-Edge-Key HTTP標題值。
* 用來清除CDN快取中資源的API權杖。
* 透過提交基本驗證表單，可存取受限制內容的使用者名稱/密碼組合清單。 [此功能可供早期採用者使用。](/help/release-notes/release-notes-cloud/release-notes-current.md#foundation-early-adopter)

各項（包括設定語法）將於下文其本身的章節中說明。

有一節說明如何[旋轉金鑰](#rotating-secrets)，這是良好的安全性作法。

## 客戶管理的CDN HTTP標頭值 {#CDN-HTTP-value}

如AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)頁面中的[CDN中所述，客戶可以選擇透過自己的CDN路由流量，這稱為「客戶CDN」（有時也稱為BYOCDN）。

在設定過程中，AdobeCDN和客戶CDN必須同意`X-AEM-Edge-Key` HTTP標頭的值。 此值是在每個請求中在客戶CDN處設定的，之後再傳送至AdobeCDN，由其驗證值是否如預期般符合，因此它可以信任其他HTTP標頭，包括有助於將請求傳送至適當AEM來源的那些標頭。

*X-AEM-Edge-Key*&#x200B;值由名為`cdn.yaml`或類似檔案中的`edgeKey1`和`edgeKey2`屬性參考，位於最上層`config`資料夾的某處。 閱讀[使用設定管道](/help/operations/config-pipeline.md#folder-structure)，以取得資料夾結構以及如何部署設定的詳細資訊。

語法如下所述：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
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

請參閱[「使用設定管道」](/help/operations/config-pipeline.md#common-syntax)，取得 `data` 節點上方屬性的描述。`kind`屬性值應該是&#x200B;*CDN*，且`version`屬性應該設定為`1`。

其他屬性包括：

* 包含子`authentication`節點的`Data`節點。
* 在`authentication`底下，有一個`authenticators`節點和一個`rules`節點，兩者都是陣列。
* 驗證者：可讓您宣告權杖或認證的型別，在此例中是邊緣金鑰。 其內容包含下列屬性：
   * name — 描述性字串。
   * 型別 — 必須是`edge`。
   * edgeKey1 - *X-AEM-Edge-Key*&#x200B;的值，它必須參考[Cloud Manager秘密型別環境變數](/help/operations/config-pipeline.md#secret-env-vars)。 在「已套用服務」欄位中，選取全部。 建議值（例如，`${{CDN_EDGEKEY_052824}}`）反映新增日期。
   * edgeKey2 — 用於旋轉機密，如下面的[旋轉機密區段](#rotating-secrets)所述。 定義方式與edgeKey1類似。 至少必須宣告`edgeKey1`和`edgeKey2`其中之一。
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* 規則：可讓您宣告應該使用哪一個驗證器，以及它是否用於發佈和/或預覽層。  內容包括：
   * name — 描述性字串。
   * when — 根據[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)文章中的語法，決定何時應該評估規則的條件。 通常會包含目前階層的比較（例如publish），以便驗證所有即時流量為透過客戶CDN的路由。
   * 動作 — 必須指定「authenticate」，並參考所要的驗證者。

>[!NOTE]
>在部署參考Edge金鑰的組態之前，必須將其設定為[密碼型別Cloud Manager環境變數](/help/operations/config-pipeline.md#secret-env-vars)。

## 清除API Token {#purge-API-token}

客戶可以使用宣告的清除API權杖[清除CDN快取](/help/implementing/dispatcher/cdn-cache-purge.md)。 Token是在名為`cdn.yaml`或類似的檔案中宣告的，位於最上層`config`資料夾的某處。 閱讀[使用設定管道](/help/operations/config-pipeline.md#folder-structure)，以取得資料夾結構以及如何部署設定的詳細資訊。

語法如下所述：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
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

請參閱[「使用設定管道」](/help/operations/config-pipeline.md#common-syntax)，取得 `data` 節點上方屬性的描述。`kind`屬性值應該是&#x200B;*CDN*，且`version`屬性應該設定為`1`。

其他屬性包括：

* 包含子`authentication`節點的`data`節點。
* 在`authentication`底下，有一個`authenticators`節點和一個`rules`節點，兩者都是陣列。
* 驗證者：可讓您宣告權杖或認證的型別，在此例中為清除金鑰。 其內容包含下列屬性：
   * name — 描述性字串。
   * 型別 — 必須是永久刪除。
   * purgeKey1 — 其值必須參考[Cloud Manager秘密型別的環境變數](/help/operations/config-pipeline.md#secret-env-vars)。 在「已套用服務」欄位中，選取全部。 建議值（例如`${{CDN_PURGEKEY_031224}}`）反映新增日期。
   * purgeKey2 — 用於輪換密碼，如下面的[輪換密碼區段](#rotating-secrets)部分所述。 至少必須宣告`purgeKey1`和`purgeKey2`其中之一。
* 規則：可讓您宣告應該使用哪一個驗證器，以及它是否用於發佈和/或預覽層。  內容包括：
   * 名稱 — 描述性字串
   * when — 根據[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)文章中的語法，決定何時應該評估規則的條件。 通常包括目前階層的比較（例如，發佈）。
   * 動作 — 必須指定「authenticate」，並參考所要的驗證者。

>[!NOTE]
>在部署參考清除金鑰的組態之前，必須將清除金鑰設定為[機密型別Cloud Manager環境變數](/help/operations/config-pipeline.md#secret-env-vars)。

您可以參考以設定清除金鑰和執行CDN快取清除為重點的[教學課程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache)。

## 基本驗證 {#basic-auth}

>[!NOTE]
>此功能尚未正式推出。若要加入早期採用者計畫，請傳送電子郵件至`aemcs-cdn-config-adopter@adobe.com`。

透過彈出要求使用者名稱和密碼的基本驗證對話方塊來保護某些內容資源。此功能主要用於輕度驗證使用案例（例如業務利害關係人審查內容），而不是作為一般使用者存取權的完整解決方案。

一般使用者會看到基本驗證對話方塊突然出現，如下所示：

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


語法如下：

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

請參閱[「使用設定管道」](/help/operations/config-pipeline.md#common-syntax)，取得 `data` 節點上方屬性的描述。`kind`屬性值應該是&#x200B;*CDN*，且`version`屬性應該設定為`1`。

此外，語法包括：

* 包含`experimental_authentication`節點的`data`節點（釋放功能時會移除實驗首碼）。
* 在`experimental_authentication`底下，有一個`authenticators`節點和一個`rules`節點，兩者都是陣列。
* 驗證者：在此案例中，會宣告基本驗證者，其結構如下：
   * 名稱 — 描述性字串
   * 型別 — 必須是`basic`
   * 認證陣列，每個認證包括下列名稱/值組，一般使用者可在基本驗證對話方塊中輸入：
      * user — 使用者的名稱
      * 密碼 — 其值必須參考[Cloud Manager密碼型別環境變數](/help/operations/config-pipeline.md#secret-env-vars)，並選取&#x200B;**全部**&#x200B;做為服務欄位。
* 規則：可讓您宣告應使用哪些驗證者，以及應保護哪些資源。 每個規則包含：
   * 名稱 — 描述性字串
   * when — 根據[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)文章中的語法，決定何時應該評估規則的條件。 通常會包含發佈層級或特定路徑的比較。
   * 動作 — 必須指定「authenticate」，並參考所要的驗證者，這是此情境的基本驗證

>[!NOTE]
>在部署參考密碼的組態之前，必須將密碼設定為[機密型別Cloud Manager環境變數](/help/operations/config-pipeline.md#secret-env-vars)。

## 旋轉密碼 {#rotating-secrets}

1. 不定期變更認證是很好的安全性做法。 雖然清除金鑰使用相同的策略，但還是可以透過邊緣金鑰的範例來達到此目的。

1. 一開始只定義了`edgeKey1`，在此案例中是參考為`${{CDN_EDGEKEY_052824}}`，這作為建議的慣例，會反映其建立日期。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
   ```
1. 輪換金鑰時，請建立新的Cloud Manager密碼，例如`${{CDN_EDGEKEY_041425}}`。
1. 在設定中，從`edgeKey2`參照並部署。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. 一旦確定不再使用舊的Edge金鑰，請從設定中移除`edgeKey1`以將其移除。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```
1. 從Cloud Manager刪除舊密碼參考(`${{CDN_EDGEKEY_052824}}`)並進行部署。

1. 準備好進行下一次輪換時，請遵循相同的程式，不過這次您會新增`edgeKey1`至組態，並參考名為的新Cloud Manager環境密碼，例如`${{CDN_EDGEKEY_031426}}`。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
         edgeKey1: ${{CDN_EDGEKEY_031426}}
   ```
