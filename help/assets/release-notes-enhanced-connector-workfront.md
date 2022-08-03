---
title: ' 版發行說明 [!DNL Workfront for Experience Manager enhanced connector]'
description: ' 版發行說明 [!DNL Workfront for Experience Manager enhanced connector]'
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: f49ac67b7a90d638e266b9f7f5bf5ac9d7f78e3a
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

#  版發行說明[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下部分概述了有關 [!DNL Workfront for Experience Manager enhanced connector]。

## 發行日期 {#release-date}

最新版本1.9.2的發佈日期 [!DNL Workfront for Experience Manager enhanced connector] 是2022年8月3日。

## 發佈亮點 {#release-highlights}

的最新版本 [!DNL Workfront for Experience Manager enhanced connector] 包括以下增強和錯誤修復：

* 的 **[!UICONTROL 上載文檔]** 工作流步驟無法將文檔附加到Workfront。

* 的 **[!UICONTROL 上載文檔]** 工作流步驟無法將文檔附加到Workfront的任務和問題。 工作流步驟將文檔成功附加到項目。

>[!IMPORTANT]
>
>Adobe建議您 [升級到最新1.9.2版](../assets/update-workfront-enhanced-connector.md) 的 [!DNL Workfront for Experience Manager enhanced connector]。

## 已知問題 {#known-issues}

* 在使用6.4配置項AEM目連結資料夾時，Experience Manager不保存 **[!UICONTROL 子資料夾]** 和 **[!UICONTROL 在具有項目組合的項目中建立連結資料夾]** 的子菜單。 的值 **[!UICONTROL 子資料夾]** 欄位更新 **[!UICONTROL 未定義]** 和 **[!UICONTROL 在具有項目組合的項目中建立連結資料夾]** 欄位更新 **[!UICONTROL 預設Portfolio]** 自動保存配置。

* 當你用經典Workfront經驗時， **[!UICONTROL 發送到]** 的 **[!UICONTROL 更多]** 下拉清單不允許您在Experience Manager中選擇目標目標。 的 **[!UICONTROL 發送到]** 選項使用 **[!UICONTROL 文檔操作]** 下拉清單。 的 **[!UICONTROL 發送到]** 選項正確工作 **[!UICONTROL 更多]** 下拉清單以及 **[!UICONTROL 文檔操作]** 新Workfront體驗中提供的下拉清單。

## 以前的版本 {#previous-releases}

### 2022年7月發行 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.1版包含以下更新：

* 為遷移到Adobe IMS的實例增加了對使用WorkfrontAPI密鑰的Experience Manager和Workfront應用程式之間身份驗證的支援。

* 連結外部檔案或資料夾時，Workfront應用程式將顯示 `SERVER_ERROR` 錯誤消息。 錯誤消息引用由於API鍵不匹配而導致的未授權異常。

* 為資產執行「建立任務」工作流時，日誌消息中將顯示「空指針」例外。

* 啟用 `Replace Spaces with DASH` Experience Manager中的「高級設定」下的配置選項，將導致在Workfront建立重複的資料夾。

### 2022年6月發行 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 現在包括以下更新：

* 通過連結資料夾上載或使用 `Send To` 在Workfront可以執行的將資產上載到Experience Manageras a Cloud Service的操作，這些資產會損壞，無法在Adobe Photoshop開啟。

### 2022年3月發行 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 現在包括以下更新：

* 現在，即使存在多個項目連結資料夾配置，您也可以在Adobe Workfront和AEM Assetsas a Cloud Service之間建立連結資料夾。

* 已添加對事件訂閱分頁的支援。

* 增加了AEM對6.4.x的支援。

* 增加了對代理環境的支援。

* 根據合作夥伴和客戶反饋修復幾個錯誤。

>[!MORELIKETHIS]
>
>* [整合 [!DNL Workfront for Experience Manager enhanced connector] Experience Manager6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [整合 [!DNL Workfront for Experience Manager enhanced connector] Experience Manager6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)

