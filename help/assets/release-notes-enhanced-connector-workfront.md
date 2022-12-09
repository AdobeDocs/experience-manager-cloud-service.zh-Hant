---
title: 版發行說明 [!DNL Workfront for Experience Manager enhanced connector]
description: 版發行說明 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: f98704357c38f61e8e7d36b33ad32e9154c611e6
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 1%

---

#  版發行說明[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下章節概述的一般發行說明 [!DNL Workfront for Experience Manager enhanced connector].

## 發行日期 {#release-date}

最新版本1.9.6的發行日期： [!DNL Workfront for Experience Manager enhanced connector] 是2022年12月9日。

## 發行重點 {#release-highlights}

最新版本 [!DNL Workfront for Experience Manager enhanced connector] 包含下列增強功能和錯誤修正：

**增強功能**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront enhanced connector現在支援對資產和資料夾執行全文搜尋。

**錯誤修正**

* 檔案版本中繼資料無法在Workfront和Experience Manager之間適當同步。
* 在Workfront中建立連結至Experience Manager的資料夾時，若資料夾使用的架構在全域設定中缺少定義，則會發生問題。
* 由於載入時間超過預期，當您按一下任何欄位時，中繼資料結構編輯器表單會停止回應。 已新增自訂表單的特定OSGi設定以解決問題。 記錄檔中會提供您新增至中繼資料結構編輯器的自訂表單名稱。

>[!IMPORTANT]
>
>Adobe建議您 [升級至最新1.9.6版](../assets/update-workfront-enhanced-connector.md) 的 [!DNL Workfront for Experience Manager enhanced connector].

## 已知問題 {#known-issues}

* 使用AEM 6.4設定專案連結資料夾時，Experience Manager不會儲存 **[!UICONTROL 子資料夾]** 和 **[!UICONTROL 在具有產品組合的專案中建立連結資料夾]** 欄位。 的值 **[!UICONTROL 子資料夾]** 欄位更新至 **[!UICONTROL 未定義]** 和 **[!UICONTROL 在具有產品組合的專案中建立連結資料夾]** 欄位更新至 **[!UICONTROL 預設Portfolio]** 儲存設定後自動執行。

* 使用傳統Workfront體驗時， **[!UICONTROL 傳送至]** 選項 **[!UICONTROL 更多]** 下拉式清單不允許您選取Experience Manager內的目標目標。 此 **[!UICONTROL 傳送至]** 選項可使用 **[!UICONTROL 文檔操作]** 下拉式清單。 此 **[!UICONTROL 傳送至]** 選項可正確運作 **[!UICONTROL 更多]** 下拉式清單以及 **[!UICONTROL 文檔操作]** 新Workfront體驗中提供的下拉式清單。

## 舊版 {#previous-releases}

### 2022年11月發行 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 11月11日發行的1.9.5版包含下列更新：

* 若您在Workfront中只為多值欄位定義一個值，則欄位值無法適當對應至Experience Manager。

* Experience Manager顯示 `SERVER_ERROR` 在 **[!UICONTROL 連結外部檔案和資料夾]** 畫面，同時存取資產資料夾，因為 `/content/dam/collections`.

* 啟用 **[!UICONTROL 將資產發佈至Brand Portal]** 「 Workfront enhanced connector設定」頁面上的「 」選項會建立不正確的事件。 即使停用選項後，也不會刪除事件。

   若要解決此問題：

   1. 升級至1.9.5版的增強連接器。

   1. 停用 **[!UICONTROL 將資產發佈至Brand Portal]** 選項。

   1. 啟用 **[!UICONTROL 將資產發佈至Brand Portal]** 選項。

   1. 刪除錯誤的事件訂閱。

      1. 執行GET呼叫 `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         對每個頁碼執行一個API呼叫。

      1. 搜尋下列文字，以尋找符合下列URL且沒有的事件訂閱 `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         請確定 `"objId": "",` 和 `"url"` 符合JSON回應。 建議的執行方法是從具有 `objId` 然後刪除數字。

      1. 記下事件訂閱ID。

      1. 刪除錯誤的事件訂閱。 對發出刪除API呼叫 `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` 因為回應代碼表示成功刪除錯誤的事件訂閱。
   >[!NOTE]
   >
   >如果在執行本過程中提到的步驟之前已刪除錯誤的事件訂閱，則可以跳過本過程的最後一步。

### 2022年10月發行 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.4版（於10月07日發行）包含下列更新：

* 由於大量事件，無法在增強連接器設定頁面上檢視「事件訂閱」索引標籤。

* Workfront無法擷取專案中現有資料夾的清單，而導致建立重複資料夾。

### 2022年9月發行 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.3版（於9月16日發行）包含下列更新：

* 無法上傳大小超過8 GB的檔案。
* 自動發佈從Workfront傳送至AEM的資產時發生問題。
* 編輯預設的中繼資料結構表單時，「標籤」欄位沒有「根路徑」欄位可用。
* 使用AEM工作流程在Workfront中新增版本時發生問題。
* 當您對Workfront中可用的資產執行AEM搜尋時，AEM會顯示錯誤訊息。
* 從資產建立任務建立的AEM工作流程且未定義父任務名稱時，不會在Workfront中建立該任務。

### 2022年8月發行 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.2版（於8月03日發行）包含下列更新：

* 此 **[!UICONTROL 上傳檔案]** 工作流程步驟無法將檔案附加至Workfront。

* 此 **[!UICONTROL 上傳檔案]** 工作流程步驟無法將檔案附加至Workfront中的工作和問題。 工作流步驟將文檔成功附加到項目。

### 2022年7月發行 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.1版包含下列更新：

* 針對移轉至Adobe IMS的執行個體，新增對使用Workfront API金鑰的Experience Manager與Workfront應用程式之間驗證的支援。

* 當您連結外部檔案或資料夾時，Workfront應用程式會顯示 `SERVER_ERROR` 錯誤訊息。 錯誤訊息是指API金鑰不符，導致未授權的例外狀況。

* 為資產執行「建立任務」工作流程時，記錄訊息中會顯示「Null指標」例外狀況。

* 當您啟用 `Replace Spaces with DASH` 「Experience Manager中的進階設定」下的設定選項，會在Workfront中建立重複的資料夾。

### 2022年6月發行 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 現在包含下列更新：

* 透過連結的資料夾上傳或使用 `Send To` Workfront中可用來上傳資產至Experience Manageras a Cloud Service的動作，資產會損毀，且無法在Adobe Photoshop中開啟。

### 2022年3月發行 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 現在包含下列更新：

* 您現在可以在Adobe Workfront和AEM Assetsas a Cloud Service之間建立連結的資料夾，即使有多個專案連結資料夾設定亦然。

* 新增對事件訂閱分頁的支援。

* 新增對AEM 6.4.x的支援。

* 新增對Proxy環境的支援。

* 根據合作夥伴和客戶意見進行數項錯誤修正。

>[!MORELIKETHIS]
>
>* [整合 [!DNL Workfront for Experience Manager enhanced connector] 與Experience Manager6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [整合 [!DNL Workfront for Experience Manager enhanced connector] 與Experience Manager6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)

