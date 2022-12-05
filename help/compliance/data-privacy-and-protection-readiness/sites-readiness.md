---
title: 資料保護和資料隱私權法規 - Adobe Experience Manager as a Cloud Service Sites 整備
description: 了解對各種資料保護和資料隱私權法規的 Adobe Experience Manager as a Cloud Service Sites 支援；包括歐盟一般資料保護規範 (GDPR)、加州消費者隱私法，以及在實施新的 AEM as a Cloud Service 專案時如何遵守。
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: ht
source-wordcount: '1032'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service Sites 的資料保護和資料隱私權法規整備 {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文件的內容並不構成法律建議，其宗旨並非取代專業的法律建議。
>
>有關資料保護和數據隱私權法規的建議，請諮詢貴公司的法律部門。

>[!NOTE]
>
>如需關於 Adobe 對隱私權問題的回應以及這對於您身為 Adobe 客戶所代表之意義的詳細資訊，請參閱 [Adobe 隱私權中心](https://www.adobe.com/tw/privacy.html)。

Adobe Experience Manager as a Cloud Service Sites 已準備好幫助客戶履行其資料隱私權和保護的合規義務。此頁面將指導客戶完成在 AEM Sites 中處理此類請求的過程。它描述了儲存私人資料的位置，以及如何以手動方式或使用程式碼移除它們。

如需更進一步的資訊，請參閱 [Adobe 隱私權中心](https://www.adobe.com/tw/privacy.html)。

>[!NOTE]
>
>請參閱 [Adobe Experience Manager as a Cloud Service Sites 的資料保護和資料隱私權法規整備](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md)以取得更進一步的詳情。

## AEM 作者階層 {#aem-author-tier}

作者伺服器上的使用者帳戶和 UGC 內容包含在 [AEM Foundation 文件](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)中。

## AEM 發佈階層 {#aem-publish-tier}

用於驗證網站訪客身分的使用者帳戶以及發佈伺服器上的 UGC 內容都包含在 [AEM Foundation 文件](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md)中。

預設情況下，AEM Sites 元件不會將訪客輸入的表單資料存放在發佈伺服器上。 建議將資料轉發給第三方系統或 Adobe Campaign 進行進一步處理。

## 選擇退出/選擇加入 {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager 受用於管理使用者選擇加入/選擇退出的 cookie 選擇退出服務的約束。

要選擇退出：

1. 瀏覽到:
   [ Adobe 隱私權中心 - 選擇退出](https://www.adobe.com/privacy/opt-out.html)

1. 向下捲動到「**服務**-**Experience Cloud 服務使用資料**」。

1. 選擇參照的連結；目前標題在&#x200B;**這裡**。

1. 您將看到以下詳細資料，以及選擇退出或加入的選項：

   * 要選擇退出有關您造訪本網站的資料的彙總和分析，必須在您的瀏覽器上安裝 cookie。此 cookie 表明您已選擇退出。

      如果您刪除選擇退出 cookie，或者如果您變更電腦或網頁瀏覽器，您將需要再次選擇退出。

      選擇退出 - 將我從訪客工作階段彙總和分析中排除 (安裝`amcglobal.sc.omtrdc.net`選擇退出 cookie) - 按一下這裡。

      選擇加入 - 將我包含在訪客工作階段彙總和分析中 (不安裝`amcglobal.sc.omtrdc.net`選擇退出 cookie) - 按一下這裡。
   按照上述步驟來存取實際連結。

   >[!NOTE]
   >
   > 進一步說明位於 **2.隱私權。** 部分 ([Adobe 一般使用條款](https://www.adobe.com/tw/legal/terms.html))。

## Analytics Foundation {#analytics-foundation}

AEM Sites 包括與 Analytics Foundation 的選擇性整合，後者使用 Adobe Analytics 隨選服務中的功能。

有關管理與 Adobe Analytics 相關的資料主體請求的進一步資訊，請參閱 [Adobe Analytics 和資料隱私權](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html)。

## Personalization Foundation by Target {#personalization-foundation-by-target}

AEM Sites 包括與 Personalization Foundation by Target 的選擇性整合，後者使用 Adobe Target 隨選服務中的功能。

有關管理與 Adobe Target 相關的資料主體請求的進一步資訊，請參閱 [Adobe Target - 隱私權和一般資料保護規範](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM 透過 ContextHub 提供一個選用資料層。這會將訪客特定的資料保存在瀏覽器中，用於規則型個人化。

預設情況下，此訪客資料不儲存在 AEM 中；AEM 將規則傳送到資料層以在瀏覽器中做出個人化決策。

### 實施選擇加入/選擇退出 {#implementing-opt-in-opt-out}

網站擁有者需要根據以下準則實施選擇退出元件。

這些準則會將選擇加入實施為預設值。因此，網站訪客必須先明確同意，才會將任何個人資料儲存在瀏覽器 (用戶端) 的持續性中。

* 每次包含 ContextHub 元件時都應包含選擇退出元件。
* 與網站資料保護和隱私權相關的條款與條件必須展示給網站訪客，允許他們：

   * 接受
   * 拒絕
   * 變更他們之前的選擇

* 如果網站訪客接受網站的條款與條件，則應移除 ContextHub 選擇退出 cookie：

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果網站訪客不接受網站的條款與條件，則應設定 ContextHub 選擇退出 cookie：

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 要檢查 ContextHub 是否以選擇退出模式執行，應在瀏覽器的主控台中進行以下呼叫：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### 預覽 ContextHub 的持續性 {#previewing-persistence-of-contexthub}

要預覽使用 ContextHub 的持續性，使用者可以：

* 使用瀏覽器的主控台；例如：

   * Chrome：

      * 開啟「開發人員工具」>「應用程式」>「儲存」：

         * 「本機儲存」> (網站) > ContextHubPersistence
         * 「工作階段儲存」> (網站) > ContextHubPersistence
         * 「Cookie」> (網站) > SessionPersistence
   * Firefox：

      * 開啟「開發人員工具」>「儲存」：

         * 「本機儲存」> (網站) > ContextHubPersistence
         * 「工作階段儲存」> (網站) > ContextHubPersistence
         * 「Cookie」> (網站) > SessionPersistence
   * Safari：

      * 開啟「偏好設定」>「進階」> 在選單列中顯示「開發」選單
      * 開啟「開發」>「顯示 JavaScript 主控台」

         * 「主控台」>「儲存」>「本機儲存」> (網站) > ContextHubPersistence
         * 「主控台」>「儲存」>「工作階段儲存」> (網站) > ContextHubPersistence
         * 「主控台」>「儲存」>「Cookie」> (網站) > ContextHubPersistence
   * Internet Explorer：

      * 開啟「開發人員工具」>「主控台」

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* 在瀏覽器的主控台中使用 ContextHub API：

   * ContextHub 提供以下資料持續層：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub 存放區會定義將使用哪個持續層，因此要檢視持續性的目前狀態，應檢查所有層。


例如，檢視儲存在 localStorage 中的資料：

要預覽使用 ContextHub 的持續性，使用者可以：

* 使用瀏覽器的主控台：

   * Chrome - 開啟「開發人員工具」>「應用程式」>「儲存」：

      * 「本機儲存」> (網站) > ContextHubPersistence
      * 「工作階段儲存」> (網站) > ContextHubPersistence
      * 「Cookie」> (網站) > SessionPersistence
   * Firefox - 開啟「開發人員工具」>「儲存」：

      * 「本機儲存」> (網站) > ContextHubPersistence
      * 「工作階段儲存」> (網站) > ContextHubPersistence
      * 「Cookie」> (網站) > SessionPersistence


* 在瀏覽器的主控台中使用 ContextHub API：

   * ContextHub 提供以下資料持續層：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub 存放區會定義將使用哪個持續層，因此要檢視持續性的目前狀態，應檢查所有層。


例如，檢視儲存在 localStorage 中的資料：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除 ContextHub 的持續性 {#clearing-persistence-of-contexthub}

要清除 ContextHub 的持續性：

* 要清除目前載入之存放區的持續性：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 要清除特定的持續層；例如，sessionStorage：

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有 ContextHub 持續層，必須為所有層呼叫適當的程式碼：

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
