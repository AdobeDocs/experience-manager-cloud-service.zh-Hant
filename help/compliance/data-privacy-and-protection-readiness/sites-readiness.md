---
title: 資料保護和資料隱私法規 — Adobe Experience Manager as a Cloud Service站點就緒性
description: 瞭解Adobe Experience Manager as a Cloud Service站點對各種資料保護和資料隱私法規的支援；包括歐盟一般資料保護條例(GDPR)、加利福尼亞消費者隱私法以及實施新as a Cloud Service項目時如AEM何遵守。
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud Service站點為資料保護和資料隱私法規做好準備 {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本檔案的內容不構成法律咨詢，也不是作為法律咨詢的替代。
>
>有關資料保護和資料隱私法規的建議，請咨詢您公司的法律部門。

>[!NOTE]
>
>有關Adobe對隱私問題的響應以及這對您作為Adobe客戶意味著什麼的詳細資訊，請參閱 [Adobe隱私中心](https://www.adobe.com/privacy.html)。

Adobe Experience Manager as a Cloud Service網站已準備好幫助客戶履行其資料隱私和保護合規性義務。 本頁指導客戶完成在AEM Sites處理此類請求的過程。 它描述了儲存的專用資料的位置，以及如何手動或使用代碼刪除這些資料。

有關詳細資訊，請參閱 [Adobe隱私中心](https://www.adobe.com/privacy.html)。

>[!NOTE]
>
>請參閱 [Adobe Experience Manager as a Cloud Service為資料保護和資料隱私法規做好準備](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md) 的上界。

## AEM 作者階層 {#aem-author-tier}

作者伺服器上的用戶帳戶和UGC內容在 [基AEM礎文檔](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)。

## AEM 發佈階層 {#aem-publish-tier}

用於驗證站點上訪問者的用戶帳戶以及發佈伺服器上的UGC內容在 [基AEM礎文檔](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md)。

預設情況下，AEM Sites元件不儲存訪問者在發佈伺服器上輸入的表單資料。 建議將資料轉發給第三方系統或Adobe Campaign以進一步處理。

## 選擇加入/選擇退出 {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager受cookie opt-out服務的約束，該服務用於管理用戶的opt-in/opt-out。

要選擇退出：

1. 導航到:
   [Adobe隱私中心 — 選擇退出](https://www.adobe.com/privacy/opt-out.html)

1. 向下滾動到 **服務** - **Experience Cloud服務使用資料**。

1. 選擇引用的連結；當前標題 **這裡**。

1. 您將收到以下詳細資訊，以及選擇退出或加入的選項：

   * 要選擇不聚合和分析有關您訪問此站點的資料，必須在瀏覽器上安裝Cookie。 此Cookie標識您已選擇退出。

      如果刪除選擇退出Cookie，或者更改電腦或Web瀏覽器，則需要再次選擇退出。

      選擇退出 — 將我排除在訪問者會話聚合和分析之外(安裝 `amcglobal.sc.omtrdc.net` opt-out cookie) — 按一下這裡。

      選擇加入 — 在訪問者會話聚合和分析中包括我(不安裝 `amcglobal.sc.omtrdc.net` opt-out cookie) — 按一下這裡。
   按照上述步驟訪問實際連結。

   >[!NOTE]
   >
   > 在 **2. 隱私策略.** 的下界 [Adobe一般使用條款](https://www.adobe.com/tw/legal/terms.html)。

## 分析基礎 {#analytics-foundation}

AEM Sites包括與Analytics Foundation的可選整合，該整合使用Adobe Analytics按需服務中的功能。

有關管理與Adobe Analytics有關的資料主題請求的進一步資訊，請參見 [Adobe Analytics與資料隱私](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html)。

## 按目標排列的個性化基礎 {#personalization-foundation-by-target}

AEM Sites公司包括可選的與Personalization Foundation by Target的整合，該整合使用Adobe Target按需服務中的功能。

有關管理與Adobe Target有關的資料主題請求的進一步資訊，請參見 [Adobe Target — 隱私和一般資料保護法規](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

提供AEM了可選的ContextHub資料層。 這會保留瀏覽器中特定於訪問者的資料，以用於基於規則的個性化。

預設情況下，此訪問者資料不儲存在AEM中；將規AEM則發送到資料層以在瀏覽器中做出個性化決策。

### 實施選擇加入/選擇退出 {#implementing-opt-in-opt-out}

站點所有者需要根據以下准則實施選擇退出元件。

這些准則將預設情況下的選擇加入。 因此，網站訪問者必須明確同意，才能將任何個人資料儲存在瀏覽器（客戶端）的持久性中。

* 每次包括ContextHub元件時都應包括opt-out元件。
* 必須向網站訪問者顯示與網站資料保護和隱私相關的條款和條件，以便他們：

   * 接受
   * 拒絕
   * 更改上一個選項

* 如果站點訪問者接受站點的條款和條件，則應刪除ContextHub opt-outcookie:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果站點訪問者不接受站點的條款和條件，則應設定ContextHub opt-out cookie:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 要檢查ContextHub是否在選擇退出模式下運行，應在瀏覽器的控制台中進行以下調用：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### 預覽ContextHub的持久性 {#previewing-persistence-of-contexthub}

要預覽使用的持久性ContextHub，用戶可以：

* 使用瀏覽器的控制台；例如：

   * 鉻：

      * 開啟開發人員工具>應用程式>儲存：

         * 本地儲存>（網站）> ContextHubPersistence
         * 會話儲存>（網站）> ContextHubPersistence
         * Cookie >（網站）> SessionPersistence
   * Firefox:

      * 開啟開發人員工具>儲存：

         * 本地儲存>（網站）> ContextHubPersistence
         * 會話儲存>（網站）> ContextHubPersistence
         * Cookie >（網站）> SessionPersistence
   * Safari:

      * 開啟「首選項」>「高級」>「在菜單欄中顯示開發」菜單
      * 開啟「開發」>「顯示JavaScript控制台」

         * 控制台>儲存>本地儲存>（網站）> ContextHubPersistence
         * 控制台>儲存>會話儲存>（網站）> ContextHubPersistence
         * 控制台>儲存> Cookies >（網站）> ContextHubPersistence
   * Internet Explorer:

      * 開啟開發人員工具>控制台

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* 使用瀏覽器控制台中的ContextHub API:

   * ContextHub提供以下資料持久性層：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub儲存區定義將使用的持久性層，因此應檢查所有層的持久性的當前狀態。


例如，要查看儲存在localStorage中的資料：

要預覽使用的持久性ContextHub，用戶可以：

* 使用瀏覽器的控制台：

   * Chrome — 開啟開發人員工具>應用程式>儲存：

      * 本地儲存>（網站）> ContextHubPersistence
      * 會話儲存>（網站）> ContextHubPersistence
      * Cookie >（網站）> SessionPersistence
   * Firefox — 開啟開發人員工具>儲存：

      * 本地儲存>（網站）> ContextHubPersistence
      * 會話儲存>（網站）> ContextHubPersistence
      * Cookie >（網站）> SessionPersistence


* 使用瀏覽器控制台中的ContextHub API:

   * ContextHub提供以下資料持久性層：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub儲存區定義將使用的持久性層，因此應檢查所有層的持久性的當前狀態。


例如，要查看儲存在localStorage中的資料：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除ContextHub的持久性 {#clearing-persistence-of-contexthub}

要清除ContextHub持久性：

* 要清除當前載入的儲存的持久性：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 清除特定的持久性層；例如，sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有ContextHub持久性層，必須為所有層調用相應的代碼：

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
