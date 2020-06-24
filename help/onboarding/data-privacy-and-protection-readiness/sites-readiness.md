---
title: 資料保護與資料隱私權法規- Adobe Experience Manager作為雲端服務網站的就緒性
description: '瞭解Adobe Experience Manager如何以雲端服務網站的形式支援各種資料保護與資料隱私權規定； 包括歐盟通用資料保護規則(GDPR)、加州消費者隱私法，以及如何在將新AEM實作為雲端服務專案時符合規定。 '
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 1%

---


# Adobe Experience Manager作為雲端服務網站，可隨時針對資料保護和資料隱私權法規做好準備 {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本檔案內容不構成法律咨詢，不代表法律咨詢。
>
>請洽詢貴公司的法律部門，以取得有關資料保護與資料隱私權法規的建議。

>[!NOTE]
>
>如需Adobe對隱私權問題之回應，以及這對您身為Adobe客戶意味著什麼的詳細資訊，請參 [閱Adobe的隱私權中心](https://www.adobe.com/privacy.html)。

Adobe Experience Manager作為雲端服務網站，已準備好協助客戶履行其資料隱私及保護合規性義務。 本頁面會引導客戶完成在AEM Sites中處理此類要求的程式。 它說明儲存的私人資料位置，以及如何手動或使用程式碼移除這些資料。

如需詳細資訊，請參 [閱Adobe隱私權中心](https://www.adobe.com/privacy.html)。

>[!NOTE]
>
>如需詳 [細資訊，請參閱Adobe Experience Manager的雲端服務就緒性資料保護與資料隱私權法規](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md) 。

## AEM 作者階層 {#aem-author-tier}

AEM Foundation檔案中涵蓋作者伺服器上的使用者帳戶和UGC [內容](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)。

## AEM 發佈階層 {#aem-publish-tier}

AEM Foundation檔案中涵蓋用來驗證網站訪客的使用者帳戶，以及發佈伺服器上的UGC [內容](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)。

依預設，AEM Sites元件不會儲存訪客在發佈伺服器上輸入的表單資料。 建議將資料轉送至協力廠商系統或Adobe Campaign以進一步處理。

## 選擇加入／選擇退出 {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager受Cookie選擇退出服務約束，該服務用於管理使用者的選擇加入／選擇退出。

要退出：

1. 導航到:
   [Adobe隱私權中心——選擇退出](https://www.adobe.com/privacy/opt-out.html)

1. 向下捲動至 **服務** - **Experience Cloud服務使用資料**。

1. 選擇引用的連結； 目前的 **標題**。

1. 您將會看到下列詳細資訊，以及選擇退出或加入的選項：

   * 若要選擇退出匯總和分析您造訪此網站的相關資料，您必須在您的瀏覽器上安裝Cookie。 此Cookie可識別您已選擇退出。

      如果您刪除選擇退出Cookie，或者您變更電腦或網頁瀏覽器，則需要再次選擇退出。

      選擇退出——將我排除在訪客作業匯總和分析之外(安裝選擇退 `amcglobal.sc.omtrdc.net` 出Cookie)-按一下此處。

      選擇加入——將我納入訪客作業匯總與分析(請勿安裝選擇 `amcglobal.sc.omtrdc.net` 退出Cookie)-按一下此處。
   請依照上述步驟來存取實際連結。

   <!--
    NOTE TO WRITER: Change link to https://www.adobe.com/legal/terms.html and edit note.
    -->

   >[!NOTE]
   >
   > 「使用條款」的「隱 **私權政策** 」一節中 [有進一步說明](https://marketing.adobe.com/resources/help/zh_TW/terms.html)。

## Analytics Foundation {#analytics-foundation}

AEM Sites包含Analytics Foundation的選購整合，該整合使用Adobe Analytics隨選服務中的功能。

如需有關管理Adobe Analytics相關資料主體要求的詳細資訊，請參閱 [Adobe Analytics和資料隱私權](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-view-settings.html)。

## Target的個人化基礎 {#personalization-foundation-by-target}

AEM Sites包含與Personalization Foundation by Target的選購整合，此整合使用Adobe Target隨選服務中的功能。

如需有關管理Adobe Target相關資料主體要求的詳細資訊，請參閱 [Adobe Target —— 隱私權與一般資料保護規則](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM提供ContextHub的選用資料層。 如此可保留瀏覽器中特定訪客的資料，以便用於規則型個人化。

依預設，此訪客資料不會儲存在AEM中； AEM會傳送規則至資料層，以便在瀏覽器中做個人化決策。

### 實作選擇加入／選擇退出 {#implementing-opt-in-opt-out}

網站擁有者必鬚根據下列准則建置退出元件。

這些准則會以預設方式實作選擇加入。 因此，網站訪客必須明確同意，才能將任何個人資料儲存在瀏覽器（用戶端）的永續性中。

* 每次包含ContextHub元件時，都應包含退出元件。
* 與網站資料保護和隱私權相關的條款與條件必須顯示給網站訪客，讓他們能夠：

   * 接受
   * 拒絕
   * 變更先前的選擇

* 如果網站訪客接受網站的條款與條件，ContextHub選擇退出Cookie應該移除：

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果網站訪客不接受網站的條款與條件，應設定ContextHub退出Cookie:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 若要檢查ContextHub是否在選擇退出模式下執行，應在瀏覽器的主控台中進行下列呼叫：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### 預覽ContextHub的永續性 {#previewing-persistence-of-contexthub}

若要預覽使用ContextHub的永久性，使用者可以：

* 使用瀏覽器的主控台； 例如：

   * Chrome:

      * 開啟「開發人員工具>應用程式>儲存空間：

         * 本機儲存>（網站）> ContextHubPersistence
         * 作業儲存>（網站）> ContextHubPersistence
         * Cookie >（網站）> SessionPersistence
   * Firefox:

      * 開啟「開發人員工具>儲存空間」:

         * 本機儲存>（網站）> ContextHubPersistence
         * 作業儲存>（網站）> ContextHubPersistence
         * Cookie >（網站）> SessionPersistence
   * Safari:

      * 在功能表列中開啟「偏好設定>進階>顯示開發功能表」
      * 開啟「開發>顯示JavaScript主控台」

         * 控制台>儲存>本機儲存>（網站）> ContextHubPersistence
         * 控制台>儲存>作業儲存>（網站）> ContextHubPersistence
         * 控制台>儲存> Cookie >（網站）> ContextHubPersistence
   * Internet Explorer:

      * 開啟「開發人員工具>主控台」

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* 使用瀏覽器主控台中的ContextHub API:

   * ContextHub提供下列資料永續性層：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub儲存器定義將使用哪個持久性層，因此查看持久性的當前狀態，應檢查所有層。


例如，要查看儲存在localStorage中的資料：

若要預覽使用ContextHub的永久性，使用者可以：

* 使用瀏覽器的控制台：

   * Chrome —— 開啟「開發人員工具>應用程式>儲存空間」:

      * 本機儲存>（網站）> ContextHubPersistence
      * 作業儲存>（網站）> ContextHubPersistence
      * Cookie >（網站）> SessionPersistence
   * Firefox —— 開啟「開發人員工具>儲存空間」:

      * 本機儲存>（網站）> ContextHubPersistence
      * 作業儲存>（網站）> ContextHubPersistence
      * Cookie >（網站）> SessionPersistence


* 使用瀏覽器主控台中的ContextHub API:

   * ContextHub提供下列資料永續性層：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub儲存器定義將使用哪個持久性層，因此查看持久性的當前狀態，應檢查所有層。


例如，要查看儲存在localStorage中的資料：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除ContextHub的永續性 {#clearing-persistence-of-contexthub}

要清除ContextHub持久性，請執行以下操作：

* 要清除當前載入的儲存的持久性，請執行以下操作：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 清除特定的持久層； 例如，sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有ContextHub持久層，必須對所有層調用適當的代碼：

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
