---
title: 資料保護與資料隱私權法規 — Adobe Experience Manager作為Cloud Service網站整備
description: 了解Adobe Experience Manager作為各種資料保護和資料隱私權法規的Cloud Service網站支援；包括歐盟一般資料保護規範(GDPR)、加州消費者隱私法，以及實作新AEM as aCloud Service專案時如何遵循。
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 1%

---

# Adobe Experience Manager as aCloud Service網站對資料保護和資料隱私權法規的整備 {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本檔案的內容不構成法律建議，且用意並非取代法律建議。
>
>如需資料保護與資料隱私權法規的相關建議，請諮詢貴公司的法律部門。

>[!NOTE]
>
>如需有關Adobe對隱私權問題的回應，以及這對您身為Adobe客戶所代表之意義的詳細資訊，請參閱[Adobe的隱私權中心](https://www.adobe.com/privacy.html)。

Adobe Experience Manager as aCloud ServiceSites已準備好協助客戶履行其資料隱私權和保護法規遵循的義務。 本頁面會引導客戶完成在AEM Sites中處理此類請求的程式。 它說明了儲存的私人資料位置，以及如何手動或使用程式碼移除這些資料。

如需詳細資訊，請參閱[Adobe隱私中心](https://www.adobe.com/privacy.html)。

>[!NOTE]
>
>如需詳細資訊，請參閱[Adobe Experience Manager as a Readiness for Data Protection and Data Privacy Regulations](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md) 。

## AEM 作者階層 {#aem-author-tier}

[AEM Foundation檔案](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)中涵蓋製作伺服器上的使用者帳戶和UGC內容。

## AEM 發佈階層 {#aem-publish-tier}

用於驗證網站訪客的使用者帳戶，以及發佈伺服器上的UGC內容，在[AEM Foundation檔案](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md)中有說明。

依預設，AEM Sites元件不會儲存訪客在發佈伺服器上輸入的表單資料。 建議將資料轉送至協力廠商系統或Adobe Campaign以進行進一步處理。

## 選擇加入/選擇退出 {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager受限於cookie選擇退出服務，此服務用於管理使用者的選擇加入/退出。

若要退出：

1. 導航到:
   [Adobe隱私中心 — 選擇退出](https://www.adobe.com/privacy/opt-out.html)

1. 向下捲動至&#x200B;**Services** - **Experience Cloud服務使用資料**。

1. 選擇引用的連結；目前標題為&#x200B;**here**。

1. 系統會提供下列詳細資料，以及選擇退出或加入的選項：

   * 若要選擇退出匯總及分析您造訪此網站的相關資料，必須在瀏覽器上安裝Cookie。 此Cookie可識別您已選擇退出。

      如果您刪除選擇退出Cookie，或變更電腦或網頁瀏覽器，則需要再次選擇退出。

      選擇退出 — 將我排除在訪客工作階段匯總及分析之外（安裝`amcglobal.sc.omtrdc.net`選擇退出Cookie） — 按一下這裡。

      選擇加入 — 將我加入訪客工作階段匯總及分析（請勿安裝`amcglobal.sc.omtrdc.net`選擇退出Cookie） — 按一下這裡。
   請依照上述步驟來存取實際連結。

   >[!NOTE]
   >
   > **2中有進一步說明。 隱私策略.** Adobe一 [般使用條款](https://www.adobe.com/tw/legal/terms.html)。

## Analytics Foundation {#analytics-foundation}

AEM Sites包含與Analytics Foundation的選用整合，後者使用Adobe Analytics隨需服務中的功能。

如需管理與Adobe Analytics相關的資料主體請求的詳細資訊，請參閱[Adobe Analytics和資料隱私權](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html)。

## 依Target的個人化基礎 {#personalization-foundation-by-target}

AEM Sites包含選用的Personalization Foundation by Target整合，可在Adobe Target隨需服務中使用功能。

如需管理Adobe Target相關資料主體請求的詳細資訊，請參閱[Adobe Target — 隱私權與一般資料保護規範](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM提供ContextHub的選用資料層。 這可讓瀏覽器中的訪客專屬資料保留，以用於規則型個人化。

依預設，此訪客資料不會儲存在AEM中；AEM會將規則傳送至資料層，以在瀏覽器中做出個人化決策。

### 實作選擇加入/選擇退出 {#implementing-opt-in-opt-out}

網站擁有者必鬚根據下列准則實作選擇退出元件。

這些准則會將選擇加入設為預設。 因此，網站訪客必須明確同意，才會將任何個人資料儲存在瀏覽器（用戶端）的持續性中。

* 每次包含ContextHub元件時，都應包含選擇退出元件。
* 與網站資料保護和隱私權相關的條款與條件必須顯示給網站訪客，讓他們能夠：

   * 接受
   * 拒絕
   * 改變先前的選擇

* 如果網站訪客接受網站的條款與條件，應移除ContextHub選擇退出Cookie:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果網站訪客不接受網站的條款與條件，應設定ContextHub選擇退出Cookie:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 若要檢查ContextHub是否在選擇退出模式中執行，應在瀏覽器的主控台中進行下列呼叫：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### ContextHub的預覽持續性 {#previewing-persistence-of-contexthub}

若要預覽使用ContextHub的持續時間，使用者可以：

* 使用瀏覽器的主控台；例如：

   * 鉻黃：

      * 開啟開發人員工具>應用程式>儲存：

         * 本機儲存>（網站）> ContextHubPersistence
         * 工作階段儲存>（網站）> ContextHubPersistence
         * Cookie >（網站）> SessionPersistence
   * Firefox:

      * 開啟開發人員工具>儲存：

         * 本機儲存>（網站）> ContextHubPersistence
         * 工作階段儲存>（網站）> ContextHubPersistence
         * Cookie >（網站）> SessionPersistence
   * Safari:

      * 在菜單欄中開啟「首選項」>「高級」>「顯示開發」菜單
      * 開啟「開發>顯示JavaScript主控台」

         * 控制台>儲存>本地儲存>（網站）> ContextHubPersistence
         * 控制台>儲存>工作階段儲存>（網站）> ContextHubPersistence
         * 控制台>儲存> Cookie >（網站）> ContextHubPersistence
   * Internet Explorer:

      * 開啟開發人員工具>主控台

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* 在瀏覽器的主控台中使用ContextHub API:

   * ContextHub提供下列資料持續性層：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub存放區會定義將使用的持續性層，因此，若要檢視持續性的目前狀態，應檢查所有層。


例如，要查看儲存在localStorage中的資料：

若要預覽使用ContextHub的持續時間，使用者可以：

* 使用瀏覽器的主控台：

   * Chrome — 開啟開發人員工具>應用程式>儲存：

      * 本機儲存>（網站）> ContextHubPersistence
      * 工作階段儲存>（網站）> ContextHubPersistence
      * Cookie >（網站）> SessionPersistence
   * Firefox — 開啟開發人員工具>儲存：

      * 本機儲存>（網站）> ContextHubPersistence
      * 工作階段儲存>（網站）> ContextHubPersistence
      * Cookie >（網站）> SessionPersistence


* 在瀏覽器的主控台中使用ContextHub API:

   * ContextHub提供下列資料持續性層：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub存放區會定義將使用的持續性層，因此，若要檢視持續性的目前狀態，應檢查所有層。


例如，要查看儲存在localStorage中的資料：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除ContextHub的持續性 {#clearing-persistence-of-contexthub}

若要清除ContextHub持續性：

* 要清除當前載入的儲存的持久性，請執行以下操作：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 清除特定持久層；例如，sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 若要清除所有ContextHub持續性層，必須為所有層呼叫適當的程式碼：

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (預設)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
