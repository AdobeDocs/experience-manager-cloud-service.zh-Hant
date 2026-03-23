---
title: Cloud Manager 2026.3.0 版發行說明
description: 了解 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2026.3.0 版的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 2556f606db8b74bce25cd504a183abdc43e31227
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 19%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2026.3.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2026.3.0 的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2026.3.0發行日期是2026年3月5日星期四。

下一個預計發行日期為2026年4月2日星期四。


## 新增功能 — Cloud Manager {#cloud-manager-whats-new}

* **Cloud Manager現在支援**&#x200B;內容復本&#x200B;**匯入**&#x200B;的&#x200B;**擦去**&#x200B;選項

  當您啟用&#x200B;**擦去**&#x200B;時，Cloud Manager會在開始匯入之前刪除目的地上的現有內容，這樣您就可以從頭開始，避免與現有的內容衝突。 如果您讓&#x200B;**擦去**&#x200B;保持停用，Cloud Manager會在現有目的地內容之上匯入新內容。 擦除開始前會顯示確認提示，Cloud Manager會記錄擦除動作並匯入詳細資訊，以利追蹤。

  另請參閱[複製內容](/help/implementing/developing/tools/content-copy.md#copy-content)。

* **支援AEM Experience Hub中的UI擴充功能**
[AEM Experience Hub](https://experience.adobe.com/experiencemanager)中的UI擴充功能支援現已啟用，讓開發人員得以使用Adobe App Builder建立的自訂功能和Widget來擴充介面。

  若要進一步瞭解，請參閱[AEM Experience Hub](https://developer.adobe.com/uix/docs/services/aem-experience-hub/)。

* **改善穩定性、效能和可靠性**

  此版本包含最佳化和維護更新，改善了Cloud Manager的穩定性、效能和可靠性。


## Beta 版方案 {#private-beta-program}

參與 Cloud Manager 的 Beta 版方案享有獨家存取權，在即將推出的功能正式發佈之前搶先體驗。

>[!IMPORTANT]
>
>Beta發行版本可能包含瑕疵，並依「現況」提供，並無任何保固。 Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援（透過Adobe支援服務或其他方式）測試版。 Adobe建議客戶謹慎行事，不要依賴Beta版正確運作或效能，或依賴任何隨附的檔案或資料。 Beta版中的功能和API可能會有所變更，恕不另行通知。 因此，使用測試版完全由客戶自行承擔風險。

另請參閱[AEM Beta計畫](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

目前提供下列機會：
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### 適用於AI提供技術支援的IDE的Cloud Manager MCP伺服器{#mcp-server-for-cm}

您現在可以嘗試使用MCP （模型內容通訊協定）伺服器，將Cloud Manager公用API公開為啟用AI的IDE工具（例如游標）。 連線後，您可以使用對話式提示來列出和管理計畫、管道、環境和存放庫，幫助您在不離開編輯器的情況下更快速地移動。

請參閱檔案[搭配AEM as a Cloud Service使用MCP](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)。

請參閱教學課程[Cloud Manager MCP伺服器](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-server/cloud-manager#)。

有興趣使用 Beta 版嗎？使用您的Adobe OrgID和方案ID以電子郵件傳送[GRP-AEM-CM-MCP-FEEDBACK@adobe.com](mailto:GRP-AEM-CM-MCP-FEEDBACK@adobe.com)。


<!--
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

### 模組快取能加快建置速度 {#quick-build-cm-pipelines}

新的建置模型會使用模組層級快取來編譯已變更的模組 (而非整個存放庫)，藉此縮短建置時間。 此建置模型適用於程式碼品質、完整堆疊和僅限中繼管道。

![編輯非生產管道對話方塊，其中顯示兩個建置策略選項，即Full Build和Smart Build](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*編輯非生產管道對話方塊，其中顯示兩個建置策略選項：完整建置和智慧型建置。*

在&#x200B;**新增/編輯管道**&#x200B;對話方塊的&#x200B;**Source程式碼**&#x200B;索引標籤下方，新的&#x200B;**建置策略**&#x200B;區段可讓您選擇下列其中一個建置選項：

* **完整組建** — 每次執行都會建置存放庫中的所有模組。
* **智慧型組建** — 僅建置自上次認可後變更的模組，這會縮短整體建置時間。

您控制哪些管道使用&#x200B;**智慧型組建**。 在Beta版期間，此選項僅針對&#x200B;**程式碼品質**&#x200B;和&#x200B;**開發完整棧疊部署**&#x200B;管道顯示。

請參閱[關於在非生產管道中使用Smart Build](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build)和[新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)

感興趣嗎？ 請寄送電子郵件至 [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com)，並附上您的 Adobe OrgID 和方案 ID。

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

## 錯誤修正 {#bug-fixes}

* 解決擷取還原點時，還原點API可能傳回500錯誤的問題。 端點現在可以正確處理null值，確保一致且可靠的回應。 (CMGR-72963)
* Cloud Manager現在接受具有或不具有`.git`尾碼的GitHub存放庫URL，使API行為與UI一致，並使存放庫上線更靈活。 (CMGR-73296)
* 產品設定檔名稱驗證現在不區分大小寫，以防止在建立名稱僅因大寫不同而有所差異的設定檔時發生錯誤。 (CMGR-74075)
* 您現在可以從相同的管道執行中執行多個還原操作，為中繼和生產等環境啟用順序還原，而無需新的管道執行。 (CMGR-73538)


<!-- ## Known issues {#known-issues} -->

