---
title: 版發行說明 [!DNL Workfront for Experience Manager enhanced connector]
description: 版發行說明 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: f49ac67b7a90d638e266b9f7f5bf5ac9d7f78e3a
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

#  版發行說明[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下章節概述的一般發行說明 [!DNL Workfront for Experience Manager enhanced connector].

## 發行日期 {#release-date}

最新版本1.9.2的發行日期： [!DNL Workfront for Experience Manager enhanced connector] 是2022年8月3日。

## 發行重點 {#release-highlights}

最新版本 [!DNL Workfront for Experience Manager enhanced connector] 包含下列增強功能和錯誤修正：

* 此 **[!UICONTROL 上傳檔案]** 工作流程步驟無法將檔案附加至Workfront。

* 此 **[!UICONTROL 上傳檔案]** 工作流程步驟無法將檔案附加至Workfront中的工作和問題。 工作流步驟將文檔成功附加到項目。

>[!IMPORTANT]
>
>Adobe建議您 [升級至最新1.9.2版](../assets/update-workfront-enhanced-connector.md) 的 [!DNL Workfront for Experience Manager enhanced connector].

## 已知問題 {#known-issues}

* 使用AEM 6.4設定專案連結資料夾時，Experience Manager不會儲存 **[!UICONTROL 子資料夾]** 和 **[!UICONTROL 在具有產品組合的專案中建立連結資料夾]** 欄位。 的值 **[!UICONTROL 子資料夾]** 欄位更新至 **[!UICONTROL 未定義]** 和 **[!UICONTROL 在具有產品組合的專案中建立連結資料夾]** 欄位更新至 **[!UICONTROL 預設Portfolio]** 儲存設定後自動執行。

* 使用傳統Workfront體驗時， **[!UICONTROL 傳送至]** 選項 **[!UICONTROL 更多]** 下拉式清單不允許您選取Experience Manager內的目標目標。 此 **[!UICONTROL 傳送至]** 選項可使用 **[!UICONTROL 文檔操作]** 下拉式清單。 此 **[!UICONTROL 傳送至]** 選項可正確運作 **[!UICONTROL 更多]** 下拉式清單以及 **[!UICONTROL 文檔操作]** 新Workfront體驗中提供的下拉式清單。

## 舊版 {#previous-releases}

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

