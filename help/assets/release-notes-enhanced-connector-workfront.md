---
title: 版發行說明 [!DNL Workfront for Experience Manager enhanced connector]
description: 版發行說明 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 3a00faaf285be693243e3fb55159149520293610
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 1%

---

#  版發行說明[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下部分概述了有關 [!DNL Workfront for Experience Manager enhanced connector]。

## 發行日期 {#release-date}

最新版本1.9.10的發佈日期 [!DNL Workfront for Experience Manager enhanced connector] 是2023年5月18日。

## 發佈亮點 {#release-highlights}

的最新版本 [!DNL Workfront for Experience Manager enhanced connector] 包括以下更新：

* Workfront基於從Experience Manager到Workfront的REST調用，為重複事件訂閱返回409 HTTP響應，這會導致空指針異常。


>[!IMPORTANT]
>
>Adobe建議您 [升級到最新1.9.10版](../assets/update-workfront-enhanced-connector.md) 的 [!DNL Workfront for Experience Manager enhanced connector]。

## 已知問題 {#known-issues}

* 在使用6.4配置項AEM目連結資料夾時，Experience Manager不保存 **[!UICONTROL 子資料夾]** 和 **[!UICONTROL 在具有項目組合的項目中建立連結資料夾]** 的子菜單。 的值 **[!UICONTROL 子資料夾]** 欄位更新 **[!UICONTROL 未定義]** 和 **[!UICONTROL 在具有項目組合的項目中建立連結資料夾]** 欄位更新 **[!UICONTROL 預設Portfolio]** 自動保存配置。

* 當你用經典Workfront經驗時， **[!UICONTROL 發送到]** 的 **[!UICONTROL 更多]** 下拉清單不允許您在Experience Manager中選擇目標目標。 的 **[!UICONTROL 發送到]** 選項使用 **[!UICONTROL 文檔操作]** 下拉清單。 的 **[!UICONTROL 發送到]** 選項正確工作 **[!UICONTROL 更多]** 下拉清單以及 **[!UICONTROL 文檔操作]** 新Workfront體驗中提供的下拉清單。

## 以前的版本 {#previous-releases}

### 2023年4月發行 {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] 2023年4月10日發佈的1.9.9版包含以下更新：

* Experience Manager顯示 `DateTimeParseException` 在連結資料夾建立期間從Workfront接收上次修改日期時例外。

* 在短時間內建立多個連結項目資料夾時出現問題。

* 無法配置新項目連結資料夾集數的閾值限制。

### 2023年3月發行 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] 2023年3月03日發佈的1.9.8版包含以下更新：

* 在Workfront建立項目連結資料夾時，Experience Manager效能得到改善。

* Workfront的評論刪除現在反映在Experience Manager。

* 能夠在as a Cloud Service於配置連接器的Experience Manager上管理阻止新客戶。


### 2023年1月發行 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 2023年2月02日發佈的1.9.7版包含以下更新：

* 在安裝1.9.6版之後，元資料編輯器不會列出Workfront自定義表單屬性。

* 設備控制台顯示 `/content/dam/jcr:content/metadata/wfProjectURL not found` 安裝Workfront增強連接器並開啟Assets首頁後出現錯誤消息。

### 2022年12月發行 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.6版，於2009年12月發佈，包括以下更新：

**增強**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront增強連接器現在支援對資產和資料夾執行全文搜索。

**錯誤修正**

* 文檔版本元資料在Workfront和Experience Manager之間無法正確同步。
* 建立連結到WorkfrontExperience Manager的資料夾時，當資料夾使用全局配置中缺少定義的架構時出現問題。
* 由於載入時間比預期長，當您按一下任何欄位時，元資料架構編輯器表單將停止響應。 為自定義表單添加了特定OSGi配置以解決此問題。 添加到元資料架構編輯器的自定義表單的名稱在日誌中可用。

### 2022年11月發行 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 11月11日發佈的1.9.5版包括以下更新：

* 如果在Workfront中只為多值欄位定義一個值，則欄位值不會適當映射到Experience Manager。

* Experience Manager顯示 `SERVER_ERROR` 的 **[!UICONTROL 連結外部檔案和資料夾]** 訪問資產資料夾時進行螢幕顯示，因為 `/content/dam/collections`。

* 啟用 **[!UICONTROL 將資產發佈到Brand Portal]** 「Workfront增強的連接器配置」頁上的選項會建立錯誤事件。 即使禁用該選項後，也不會刪除該事件。

   要解決此問題：

   1. 升級到1.9.5版的增強連接器。

   1. 禁用 **[!UICONTROL 將資產發佈到Brand Portal]** 的子菜單。

   1. 啟用 **[!UICONTROL 將資產發佈到Brand Portal]** 的雙曲餘切值。

   1. 刪除錯誤的事件訂閱。

      1. 執行GET呼叫 `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         對每個頁碼執行一個API調用。

      1. 搜索以下文本以查找與以下URL匹配且沒有 `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         確保 `"objId": "",` 和 `"url"` 與JSON響應匹配。 建議的方法是從具有 `objId` 然後刪除該號碼。

      1. 注意事件訂閱ID。

      1. 刪除錯誤的事件訂閱。 將刪除API調用 `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` 因為響應代碼表示成功刪除錯誤事件訂閱。
   >[!NOTE]
   >
   >如果在執行此過程中提到的步驟之前已刪除了錯誤的事件預訂，則可以跳過此過程的最後一步。

### 2022年10月發行 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.4版，於10月7日發佈，包括以下更新：

* 由於發生大量事件，無法查看增強的連接器配置頁上的「事件訂閱」頁籤。

* Workfront無法獲取項目中現有資料夾的清單，這將導致建立重複資料夾。

### 2022年9月發行 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 9月16日發佈的1.9.3版包括以下更新：

* 無法上載大小超過8 GB的檔案。
* 自動發佈從Workfront發送到的資產時AEM出現問題。
* 編輯預設的元資料架構表單時，根路徑欄位不可用於「標籤」欄位。
* 使用工作流在Workfront添加新版本AEM時出現問題。
* 當您執行搜索AEMWorkfront可用的資AEM產時，將顯示錯誤消息。
* 在從資產創AEM建任務建立工作流且未定義父任務名稱時，不會在Workfront建立該任務。

### 2022年8月發行 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.2版，於8月3日發佈，包括以下更新：

* 的 **[!UICONTROL 上載文檔]** 工作流步驟無法將文檔附加到Workfront。

* 的 **[!UICONTROL 上載文檔]** 工作流步驟無法將文檔附加到Workfront的任務和問題。 工作流步驟將文檔成功附加到項目。

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

