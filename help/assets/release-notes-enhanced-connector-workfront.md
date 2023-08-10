---
title: 版發行說明 [!DNL Workfront for Experience Manager enhanced connector]
description: 版發行說明 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 4b63c00847fa21967560a59c3bcd931433a3a73f
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 1%

---

#  版發行說明[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下區段會概述以下的一般發行說明： [!DNL Workfront for Experience Manager enhanced connector].

## 發行日期 {#release-date}

最新版本1.9.12的發行日期 [!DNL Workfront for Experience Manager enhanced connector] 為2023年8月9日。

## 發行重點說明 {#release-highlights}

最新版本的 [!DNL Workfront for Experience Manager enhanced connector] 包含下列更新：

* 無法在Experience Manager中建立連結資料夾，因為沒有與連結資料夾相關聯的使用者帳戶。

* 在Experience Manager中資產的中繼資料更新期間發生競爭條件。


>[!NOTE]
>
>AEM 6.4已終止延伸支援。 如需詳細資訊，請參閱我們的 [技術支援期間](https://helpx.adobe.com/tw/support/programs/eol-matrix.html). 尋找支援的版本 [此處](https://experienceleague.adobe.com/docs/?lang=en).


>[!IMPORTANT]
>
>Adobe建議您 [升級至最新的1.9.12版本](/help/assets/workfront-connector-install.md) 的 [!DNL Workfront for Experience Manager enhanced connector].

## 已知問題 {#known-issues}

* 使用AEM 6.4設定專案連結資料夾時，Experience Manager不會儲存 **[!UICONTROL 子資料夾]** 和 **[!UICONTROL 在具有投資組合的專案中建立連結資料夾]** 欄位。 的值 **[!UICONTROL 子資料夾]** 欄位更新至 **[!UICONTROL 未定義]** 和的值 **[!UICONTROL 在具有投資組合的專案中建立連結資料夾]** 欄位更新至 **[!UICONTROL 預設Portfolio]** 儲存設定後自動進行。

* 使用傳統Workfront體驗時， **[!UICONTROL 傳送至]** 中可用的選項 **[!UICONTROL 更多]** 下拉式清單不允許您在Experience Manager中選取目標目的地。 此 **[!UICONTROL 傳送至]** 選項可透過 **[!UICONTROL 檔案動作]** 下拉式清單。 此 **[!UICONTROL 傳送至]** 選項正確運作於 **[!UICONTROL 更多]** 下拉式清單與 **[!UICONTROL 檔案動作]** 新Workfront體驗中可用的下拉式清單。

## 舊版 {#previous-releases}

### 2023年6月發行版本 {#june-2023-release}

* 當您設定進階網路時，從Adobe Workfront傳送內容到AEMas a Cloud Service時出現問題。


### 2023年5月發行版本 {#may-2023-release}

* Workfront會根據從Experience Manager到Workfront的REST呼叫，針對重複事件訂閱傳回409 HTTP回應，這會導致空指標例外狀況。

### 2023年4月發行版本 {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.9版（於2023年4月10日發行）包含下列更新：

* Experience Manager顯示 `DateTimeParseException` 連結資料夾建立期間從Workfront收到上次修改日期時會發生例外狀況。

* 在短時間內建立多個連結的專案資料夾時發生問題。

* 無法設定新專案連結資料夾集合數目的臨界值限制。

### 2023年3月發行版本 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.8版（於2023年3月3日發行）包含下列更新：

* 改善在Workfront中建立專案連結資料夾時Experience Manager的效能。

* Workfront中的評論刪除現在會反映在Experience Manager中。

* 在as a Cloud Service於設定聯結器的Experience Manager上管理封鎖全新客戶的功能。


### 2023年1月發行版本 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.7版（於2023年2月2日發行）包含下列更新：

* 安裝1.9.6版後，中繼資料編輯器沒有列出Workfront自訂表單屬性。

* 隨即顯示開發主控台 `/content/dam/jcr:content/metadata/wfProjectURL not found` 安裝Workfront增強型聯結器並開啟資產首頁後的錯誤訊息。

### 2022年12月發行版本 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.6版（於2009年12月發行）包含下列更新：

**增強功能**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront增強型聯結器現在支援對資產和資料夾執行全文搜尋。

**錯誤修正**

* 檔案版本中繼資料未在Workfront和Experience Manager之間正確進行同步。
* 當資料夾使用的結構描述在全域設定中缺少定義時，建立連結到Workfront中Experience Manager的資料夾時出現問題。
* 由於載入時間比預期還長，當您按一下任何欄位時，中繼資料結構描述編輯器表單會停止回應。 為自訂表單新增特定的OSGi設定以解決問題。 您新增到中繼資料結構描述編輯器的自訂表單的名稱可在紀錄中取得。

### 2022年11月發行版本 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.5版於11月11日發行，包含下列更新：

* 當您在Workfront中只為多值欄位定義一個值時，該欄位值未正確對應到Experience Manager。

* Experience Manager顯示 `SERVER_ERROR` 於 **[!UICONTROL 連結外部檔案和資料夾]** 存取資產資料夾時畫面，因為對的許可權無效 `/content/dam/collections`.

* 啟用 **[!UICONTROL 將資產發佈至Brand Portal]** Workfront增強型聯結器設定頁面上的選項會建立不正確的事件。 即使停用選項後，事件也不會刪除。

  若要解決問題：

   1. 升級至增強型聯結器的1.9.5版。

   1. 停用 **[!UICONTROL 將資產發佈至Brand Portal]** 選項。

   1. 啟用 **[!UICONTROL 將資產發佈至Brand Portal]** 選項。

   1. 刪除錯誤的事件訂閱。

      1. 執行GET呼叫至 `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         為每個頁碼執行一個API呼叫。

      1. 搜尋下列文字以尋找符合下列URL且沒有的事件訂閱 `objId`：

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         確定內容介於 `"objId": "",` 和 `"url"` 符合JSON回應。 建議這樣做的方法是從任何具有「 」的「事件訂閱」複製 `objId` 然後刪除該號碼。

      1. 記下事件訂閱ID。

      1. 刪除錯誤的事件訂閱。 對進行Delete API呼叫 `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` 因為回應代碼表示已成功刪除錯誤的事件訂閱。
  >[!NOTE]
  >
  >如果您在執行此程式所述的步驟之前刪除了錯誤的事件訂閱，則可以略過此程式的最後一個步驟。

### 2022年10月發行版本 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.4版（於2007年10月發行）包含下列更新：

* 由於許多事件，無法在增強型聯結器設定頁面上檢視事件訂閱索引標籤。

* Workfront無法擷取專案中現有資料夾的清單，因此會建立重複的資料夾。

### 2022年9月發行版本 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 9月16日發行的1.9.3版包含下列更新：

* 無法上傳超過8 GB的檔案。
* 自動發佈從Workfront傳送至AEM的資產時發生問題。
* 編輯預設中繼資料結構表單時，「標籤」欄位無法使用「根路徑」欄位。
* 使用AEM工作流程在Workfront中新增版本時發生問題。
* 當您執行AEM搜尋Workfront中的可用資產時，AEM會顯示錯誤訊息。
* 當您從資產建立用於任務建立的AEM工作流程，且未定義父級任務名稱時，任務不會在Workfront中建立。

### 2022年8月發行版本 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.2版於2003年8月發行，包含下列更新：

* 此 **[!UICONTROL 上傳檔案]** 工作流程步驟無法將檔案附加至Workfront。

* 此 **[!UICONTROL 上傳檔案]** 工作流程步驟無法將檔案附加至Workfront中的任務和問題。 工作流程步驟已成功將檔案附加到專案。

### 2022年7月發行版本 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.1版包含下列更新：

* 針對移轉至Adobe IMS的執行個體，新增對Experience Manager與Workfront應用程式之間使用Workfront API金鑰進行驗證的支援。

* 當您連結外部檔案或資料夾時，Workfront應用程式會顯示 `SERVER_ERROR` 錯誤訊息。 錯誤訊息會因API金鑰不符而參考未經授權的例外狀況。

* 當您執行資產的「建立作業」工作流程時，記錄訊息中會顯示「Null指標」例外狀況。

* 當您啟用 `Replace Spaces with DASH` 在Experience Manager的「進階設定」底下的組態選項，會在Workfront中建立重複的資料夾。

### 2022年6月發行版本 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 現在包含下列更新：

* 當您透過連結的資料夾上傳或使用 `Send To` Workfront中可供上傳資產至Experience Manageras a Cloud Service的動作，資產會損毀，無法在Adobe Photoshop中開啟。

### 2022年3月發行版本 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 現在包含下列更新：

* 現在，即使有多個專案連結資料夾設定，您仍可以在Adobe Workfront和AEM Assetsas a Cloud Service之間建立連結資料夾。

* 新增對事件訂閱分頁的支援。

* 新增對AEM 6.4.x的支援。

* 新增對Proxy環境的支援。

* 根據合作夥伴和客戶的意見回應進行多項錯誤修正。

>[!MORELIKETHIS]
>
>* [整合 [!DNL Workfront for Experience Manager enhanced connector] 搭配Experience Manager6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
