---
title: 設定內容傳遞網路憑證和身份驗證
description: 瞭解如何在設定檔案中宣告規則，再使用Cloud Manager設定管道來部署，以設定CDN憑證和驗證。
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 68a41d468650228b4ac35315690a76465ffe4c0b
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 3%

---


# 設定內容傳遞網路憑證和身份驗證 {#cdn-credentials-authentication}

Adobe提供的CDN具有多項功能和服務，部分功能和服務會仰賴憑證和驗證，以確保適當等級的企業安全性。 透過在使用Cloud Manager [設定管道](/help/operations/config-pipeline.md)部署的設定檔案中宣告規則，客戶可以自助方式設定以下專案：

* Adobe CDN用來驗證來自客戶管理CDN之請求的X-AEM-Edge-Key HTTP標題值。
* 用來清除CDN快取中資源的API權杖。
* 透過提交基本驗證表單，可存取受限制內容的使用者名稱/密碼組合清單。

各項（包括設定語法）將於下文其本身的章節中說明。

可以使用`${{..}}`語法參考環境或管道（部署步驟）秘密，並且可以在條件或setter中使用常值的任何地方使用。

```
kind: "CDN"
version: "1"
data:
  originSelectors:
    rules:
      - name: select-origin-example
        when: { reqHeader: "x-auth-header", equals: "${{AUTH_HEADER}}" }
        action:
          type: selectOrigin
          originName: origin-name
          headers:
            Authorization: "${{AUTH_HEADER}}"
    ...
```

處理秘密時，請謹記以下一些准則：

* 環境密碼必須解除部署為[Cloud Manager密碼型別的環境變數](/help/operations/config-pipeline.md#secret-env-vars)。 在「已套用服務」欄位中，選取全部。
* 秘密參考不會內插在字串中(例如 `"Token ${{AUTH_TOKEN}}"`將無法運作)
* 如果設定中仍參考參考某個參考的環境機密，則不應移除此環境機密。

  >[!WARNING]
  >請勿移除CDN設定中參照的環境變數。 這樣做可能會導致更新CDN設定失敗（例如，更新規則或自訂網域和憑證）。

* 秘密應定期旋轉。 有一節說明如何[旋轉金鑰](#rotating-secrets)，這是良好的安全性作法。

  >[!NOTE]
  > 定義為環境變數的秘密應視為不可變。 您應建立具有新名稱的新密碼並在設定中參照該密碼，而不是變更其值。 若未這麼做，將會導致秘密更新不可靠。


## 客戶管理的CDN HTTP標頭值 {#CDN-HTTP-value}

如AEM as a Cloud Service[頁面中的](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)CDN中所述，客戶可以選擇透過自己的CDN路由流量，這稱為「客戶CDN」（有時也稱為BYOCDN）。

在設定過程中，Adobe CDN和客戶CDN必須同意`X-AEM-Edge-Key` HTTP標題的值。 此值在傳送至Adobe CDN之前，會先在客戶CDN的每個要求上設定，接著由CDN驗證值是否如預期般符合，因此可信任其他HTTP標頭，包括有助於將要求傳送至適當AEM來源的標頭。

*X-AEM-Edge-Key*&#x200B;值由名為`edgeKey1`或類似檔案中的`edgeKey2`和`cdn.yaml`屬性參考，位於最上層`config`資料夾的某個位置。 閱讀[使用設定管道](/help/operations/config-pipeline.md#folder-structure)，以取得資料夾結構以及如何部署設定的詳細資訊。  以下範例說明語法。

如需進一步偵錯資訊和常見錯誤，請檢查[常見錯誤](/help/implementing/dispatcher/cdn.md#common-errors)。

>[!WARNING]
>不符合條件的所有要求（在以下範例中，代表對發佈層級的所有要求）將會拒絕沒有正確X-AEM-Edge-Key的直接存取。 如果您需要逐步引入驗證，請參閱[安全移轉以降低封鎖流量的風險](#migrating-safely)區段。

```
kind: "CDN"
version: "1"
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

如需詳細資訊，請參閱[設定和部署HTTP標頭驗證CDN規則](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/content-delivery/custom-domain-names-with-customer-managed-cdn#configure-and-deploy-http-header-validation-cdn-rule)教學課程步驟。

其他屬性包括：

* 包含子`Data`節點的`authentication`節點。
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
>在部署參考Edge金鑰的組態之前，必須將其設定為[密碼型別Cloud Manager環境變數](/help/operations/config-pipeline.md#secret-env-vars)。 建議使用至少32個位元組長度的唯一隨機金鑰；例如，Open SSL密碼編譯程式庫可以透過執行命令`openssl rand -hex 32`來產生隨機金鑰。

### 安全地移轉，以減少流量受阻的風險 {#migrating-safely}

如果您的網站已上線，請謹慎移轉至客戶管理的CDN，因為設定錯誤可能會封鎖公開流量，這是因為Adobe CDN只會接受具有預期X-AEM-Edge-Key標頭值的請求。 建議您在驗證規則中暫時包含其他條件的情況下，採取此做法，如此一來，只有在包含測試標頭或路徑符合時，才會封鎖請求：

```
    - name: edge-auth-rule
        when:
          allOf:  
            - { reqProperty: tier, equals: "publish" }
            - { reqHeader: x-edge-test, equals: "test" }
        action:
          type: authenticate
          authenticator: edge-auth
```

```
    - name: edge-auth-rule
        when:
          allOf:
            - { reqProperty: tier, equals: "publish" }
            - { reqProperty: path, like: "/test*" }
        action:
          type: authenticate
          authenticator: edge-auth
```

可以使用下列`curl`要求模式：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <CONFIGURED_EDGE_KEY>" -H "x-edge-test: test"
```

成功測試後，可移除其他條件並重新部署設定。

### 移轉程式(如果Adobe支援先前產生`X-AEM-Edge-Key` HTTP標頭值) {#migrating-legacy}

>[!NOTE]
>在繼續移轉之前，請排程中繼環境上的測試移轉以驗證策略。

>[!WARNING]
> 在步驟4之前，請勿變更客戶管理的CDN中的金鑰。

先前，與客戶管理的CDN整合的程式涉及客戶向Adobe支援請求X-AEM-Edge-Key HTTP標題值，而非自行定義值。 若要遷移到新的自助服務方法（您可定義自己的邊緣索引鍵值），請按照以下步驟以確保順利轉換且沒有停機時間：

1. 使用指定為`edgeKey1`和`edgeKey2`的新（客戶產生）和舊(Adobe產生)密碼來設定CDN設定。 這是[旋轉秘密](/help/implementing/dispatcher/cdn-credentials-authentication.md#rotating-secrets)檔案的變數。

2. 部署秘密和自助CDN設定。 在這個程式中的這個階段，舊的Adobe定義密碼仍應維持為客戶管理的CDN所傳遞的X-AEM-Edge-Key值。

3. 請聯絡Adobe支援，要求Adobe切換使用自助設定，並指定您已部署該設定。

4. 在Adobe確認已執行該動作後，請將您的客戶管理的CDN設定為`X-AEM-Edge-Key` HTTP標頭值使用新的客戶定義金鑰。

5. 從CDN設定中移除舊金鑰，並再次部署設定管道。

>[!WARNING]
>如果您未將兩個金鑰同時設定為遞補，則可能會導致移轉期間發生停機。

## 清除API Token {#purge-API-token}

客戶可以使用宣告的清除API權杖[清除CDN快取](/help/implementing/dispatcher/cdn-cache-purge.md)。 Token是在名為`cdn.yaml`或類似的檔案中宣告的，位於最上層`config`資料夾的某處。 閱讀[使用設定管道](/help/operations/config-pipeline.md#folder-structure)，以取得資料夾結構以及如何部署設定的詳細資訊。

語法如下所述：

```
kind: "CDN"
version: "1"
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

* 包含子`data`節點的`authentication`節點。
* 在`authentication`底下，有一個`authenticators`節點和一個`rules`節點，兩者都是陣列。
* 驗證者：可讓您宣告權杖或認證的型別，在此例中為清除金鑰。 其內容包含下列屬性：
   * name — 描述性字串。
   * 型別 — 必須是永久刪除。
   * purgeKey1 — 其值必須參考[Cloud Manager秘密型別的環境變數](/help/operations/config-pipeline.md#secret-env-vars)。 在「已套用服務」欄位中，選取全部。 建議值（例如`${{CDN_PURGEKEY_031224}}`）反映新增日期。
   * purgeKey2 — 用於輪換密碼，在下方[輪換密碼](#rotating-secrets)一節中有所說明。 至少必須宣告`purgeKey1`和`purgeKey2`其中之一。
* 規則：可讓您宣告應該使用哪一個驗證器，以及它是否用於發佈和/或預覽層。  內容包括：
   * 名稱 — 描述性字串
   * when — 根據[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)文章中的語法，決定何時應該評估規則的條件。 通常包括目前階層的比較（例如，發佈）。
   * 動作 — 必須指定「authenticate」，並參考所要的驗證者。

>[!NOTE]
>在部署參考清除金鑰的組態之前，必須將清除金鑰設定為[機密型別Cloud Manager環境變數](/help/operations/config-pipeline.md#secret-env-vars)。 建議使用至少32個位元組長度的唯一隨機金鑰；例如，Open SSL密碼編譯程式庫可以透過執行命令openssl rand -hex 32來產生隨機金鑰

您可以參考以設定清除金鑰和執行CDN快取清除為重點的[教學課程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache)。

## 基本驗證 {#basic-auth}

透過彈出要求使用者名稱和密碼的基本驗證對話方塊來保護某些內容資源。此功能主要用於輕度驗證使用案例（例如業務利害關係人審查內容），而不是作為一般使用者存取權的完整解決方案。

一般使用者會看到基本驗證對話方塊突然出現，如下所示：

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


語法如下：

```
kind: "CDN"
version: "1"
data:
  authentication:
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

* 包含`data`節點的`authentication`節點。
* 在`authentication`底下，有一個`authenticators`節點和一個`rules`節點，兩者都是陣列。
* 驗證者：在此案例中，會宣告基本驗證者，其結構如下：
   * 名稱 — 描述性字串
   * 型別 — 必須是`basic`
   * 最多10個憑證的陣列，每個憑證都包含以下名稱/值組，一般使用者可在基本驗證對話方塊中輸入這些名稱/值組：
      * user — 使用者的名稱。
      * 密碼 — 其值必須參考[Cloud Manager密碼型別環境變數](/help/operations/config-pipeline.md#secret-env-vars)，並選取&#x200B;**全部**&#x200B;做為服務欄位。
* 規則：可讓您宣告應使用哪些驗證者，以及應保護哪些資源。 每個規則包含：
   * 名稱 — 描述性字串
   * when — 根據[流量篩選規則](/help/security/traffic-filter-rules-including-waf.md)文章中的語法，決定何時應該評估規則的條件。 通常會包含發佈層級或特定路徑的比較。
   * 動作 — 必須指定「authenticate」，並參考所要的驗證者，這是此情境的基本驗證

>[!NOTE]
>
>在部署參考密碼的組態之前，必須將密碼設定為[機密型別Cloud Manager環境變數](/help/operations/config-pipeline.md#secret-env-vars)。

## 旋轉密碼 {#rotating-secrets}

定期變更認證是良好的安全性做法。 請記住，環境變數不應直接變更，而是應建立新密碼並在設定中參照新名稱。

此使用案例使用邊緣索引鍵的範例說明如下，不過相同的策略也可以用於清除索引鍵。

1. 一開始只定義了`edgeKey1`，在此案例中是參考為`${{CDN_EDGEKEY_052824}}`，這作為建議的慣例，會反映其建立日期。

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
   ```

1. 輪換金鑰時，請建立新的Cloud Manager密碼，例如`${{CDN_EDGEKEY_041425}}`。
1. 在設定中，從`edgeKey2`參照並部署。

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. 一旦確定不再使用舊的Edge金鑰，請從設定中移除`edgeKey1`以將其移除。

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. 從Cloud Manager刪除舊密碼參考(`${{CDN_EDGEKEY_052824}}`)並進行部署。

1. 準備好進行下一次輪換時，請遵循相同的程式，不過這次您會新增`edgeKey1`至組態，並參考名為的新Cloud Manager環境密碼，例如`${{CDN_EDGEKEY_031426}}`。

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
         edgeKey1: ${{CDN_EDGEKEY_031426}}
   ```

旋轉在請求標頭中設定的秘密時（例如驗證後端），建議分兩個步驟進行旋轉，以確保標頭值切換時不會出現暫時間隙。

1. 旋轉前的初始設定。 在此狀態下，會將舊金鑰傳送至後端。

   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_1}}
   ```

1. 將相同的標頭設定兩次，以引入新的索引鍵`API_KEY_2` （新索引鍵應設定在舊索引鍵之後）。 部署此專案後，您會在後端看到新索引鍵。

   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_1}}
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_2}}
   ```

1. 從設定中移除舊金鑰`API_KEY_1`。 部署此專案後，您會在後端看到新金鑰，然後可以安全地移除舊金鑰的環境變數。


   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_2}}
   ```


