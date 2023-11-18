---
title: 管理您的數位資產
description: 在  [!DNL Assets view] 中移動、刪除、複製、重新命名、更新您的資產，並進行版本設定。
role: User,Leader
contentOwner: AG
exl-id: b01e98b9-0cc2-47c5-9f5b-79b8e6bef39f
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 92%

---

# 管理資產 {#manage-assets}

您可以使用 [!DNL Assets view] 的人性化介面，輕鬆進行各種數位資產管理 (DAM) 任務。新增資產後，即可搜尋、下載、移動、複製、重新命名、刪除、更新和編輯您的資產。

使用 [!DNL Assets view] 完成下列資產管理任務。選取資產時，下列選項會在頂部的工具列中顯示。

![選取資產時可用的工具列選項](assets/toolbar-image-selected.png)

*圖：在選取影像的工具列中可用的選項。*

* ![取消選取圖示](assets/do-not-localize/close-icon.png) 取消選取。
* ![詳細資料圖示](assets/do-not-localize/edit-in-icon.png) 按一下以預覽資產和檢視詳細的中繼資料。預覽時，您可以檢視版本和編輯影像。
* ![下載圖示](assets/do-not-localize/download-icon.png) 將選取的資產下載到您的本機檔案系統。
* ![刪除圖示](assets/do-not-localize/delete-icon.png) 刪除選取的資產或檔案夾。
* ![簽出圖示](assets/do-not-localize/checkout-icon.png) 簽出選取的資產。
* ![複製圖示](assets/do-not-localize/copy-icon.png) 複製選取的檔案或資料夾。
* ![移動圖示](assets/do-not-localize/move-icon.png) 將選取的資產或資料夾移至存放庫階層中不同的位置。
* ![重新命名圖示](assets/do-not-localize/rename-icon.png) 重新命名選取的資產或資料夾。請使用唯一名稱，否則重新命名動作會失敗並出現警告。您可以使用新的名稱再試。
* ![指派任務圖示](assets/do-not-localize/review-delegate-icon.png) 指派任務給其他使用者，以在資產上共同作業。

您可以在資產縮圖上檢視相同選項。

![資產縮圖上用於管理資產的選項](assets/options-on-thumbnail.png)

[!DNL Assets view] 只會在工具列中根據選取的資產類型，顯示相關的選項。

![選取資產時可用的工具列選項](assets/toolbar-folder-selected.png)

*圖：在選取資料夾的工具列中可用的選項。*

![選取資產時可用的工具列選項](assets/toolbar-pdf-selected.png)

*圖：在選取 PDF 檔案的工具列中可用的選項。*

## 下載和散發資產 {#download}

您可以選取一個或更多資產或資料夾或兩者的組合，然後將選取項目下載到您的本機檔案系統。您可以再次編輯資產和上傳或在 [!DNL Assets view] 外部散發資產。 您也可以[下載資產的轉譯](/help/assets/add-delete-assets-view.md#renditions)。

## 資產版本設定 {#versions-of-assets}

<!-- 
TBD: query for engineering: How many versions are maintained. What happens when we reach that limit? Are old versions automatically removed? -->

再次上傳已上傳或編輯的資產時，[!DNL Assets view] 便會對資產進行版本設定。您可以檢視版本記錄、先前的版本，並可以將資產先前的版本還原成最新版本 (必要時回復至先前的版本)。資產版本會在以下情況中建立：

* 上傳新資產時，新資產的檔案名稱跟現有的資產相同，以及所在的資料夾跟現有的資產相同。[!DNL Assets view] 會提示覆寫先前的資產，或將新資產另存新版本。請參閱[上傳重複資產](/help/assets/add-delete-assets-view.md)。

  ![上傳時建立版本](assets/uploads-manage-duplicates.png)

  *圖：上傳名稱與現有資產名稱相同的資產時，您可以建立該資產的版本。*

* 編輯影像然後按一下「**[!UICONTROL 另存新版本]**」。請參閱[編輯影像](/help/assets/edit-images-assets-view.md)。

  ![將編輯的影像另存新版本](assets/edit-image2.png)

  *圖：將編輯的影像另存新版本。*

* 開啟現有資產的版本。按一下「**[!UICONTROL 新版本]**」，然後上傳存放庫中較新版本的資產。

  ![從版本記錄上傳新版本資產的選項](assets/view-asset-versions2.png)

### 檢視資產的版本 {#view-versions}

上傳資產的重複複本或修改的複本時，您可以建立其版本。版本設定功能可讓您檢閱歷史資產並在必要時恢復成先前的版本。

若要檢視版本，請開啟資產的預覽，然後從右側邊欄按一下「**[!UICONTROL 版本]**」 ![版本圖示](assets/do-not-localize/versions-clock-icon.png)。若要預覽特定版本，請選取該版本。若要恢復至該版本，請按一下「**[!UICONTROL 製作最新]**」。

您也可以從版本時間表建立版本。選取最新的版本、按一下「**[!UICONTROL 新版本]**」，然後從您的本機檔案系統上傳該資產的新複本。

![檢視資產的版本](assets/view-asset-versions1.png)

*圖：檢視資產的版本、恢復成先前的版本，或上傳另一個新版本。*

## 管理資產狀態 {#manage-asset-status}

**需要的權限：**`Can Edit`、`Owner` 或資產的管理員權限。

「資產」檢視可讓您對存放庫中可用的資產設定狀態。 設定資產狀態以將數位資產的下游消費控管和管理得更好。

您可以在資產上設定下列狀態：

* 已核准

* 已拒絕

* 無狀態

### 設定資產狀態 {#set-asset-status}

若要設定資產狀態：

1. 選取該資產，然後按一下工具列中的「**[!UICONTROL 詳細資料]**」。

1. 在 **[!UICONTROL 基本]** 索引標籤中，選取資產狀態 **[!UICONTROL 狀態]** 下拉式清單。 可能的值包括「已核准」、「已拒絕」以及「無狀態」(預設)。

   >[!VIDEO](https://video.tv.adobe.com/v/342495)


### 設定資產到期日 {#set-asset-expiration-date}

「資產」檢視也可讓您設定存放庫中可用資產的有效日期。 您可以[](search-assets-view.md#refine-search-results) 根據`Expired`資產狀態來篩選搜尋結果。此外，您可以指定資產的有效日期範圍以進一步篩選搜尋結果。

若要設定資產到期日：

1. 選取該資產，然後按一下工具列中的「**[!UICONTROL 詳細資料]**」。

1. 在「**[!UICONTROL 基本]**」標籤中，使用「**[!UICONTROL 到期日]**」欄位設定資產的到期日。

`Expired` 資產卡指標便會覆寫為資產所設定的 `Approved` 或 `Rejected` 指標。

您也可以根據資產狀態來篩選資產，如需詳細資訊，請參閱 [在「資產」檢視中搜尋資產](search-assets-view.md).

## 自訂中繼資料表單以包含資產狀態欄位 {#customize-asset-status-metadata-form}

**需要的權限：**&#x200B;管理員

資產檢視預設會提供許多標準中繼資料欄位。 組織擁有其他中繼資料需求，並需要更多中繼資料欄位以新增特定企業中繼資料。中繼資料表單可讓企業將自訂中繼資料欄位新增到資產的[!UICONTROL 詳細資訊]頁面。特定企業中繼資料能夠改善其資產的控管和探索。

如需更多有關如何將更多中繼資料欄位新增到中繼資料表單的資訊，請參閱「[中繼資料表單](metadata-assets-view.md#metadata-forms)」。

**將資產狀態中繼資料欄位新增至表單**

若要將資產狀態中繼資料欄位新增至表單，請將「**[!UICONTROL 資產狀態]**」元件從左側邊欄拖曳至表單。對應屬性會自動預先填入。儲存表單以確認變更。

**將到期日中繼資料欄位新增至表單**

若要將到期日中繼資料欄位新增至表單，請將「**[!UICONTROL 日期]**」元件從左側邊欄拖曳至表單。將「**到期日**」指定為標籤，並將 `pur:expirationDate` 指定為對應屬性。儲存表單以確認變更。

## 後續步驟 {#next-steps}

* [觀看在「資產」檢視中管理資產的相關影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/managing.html)

* 使用資產檢視使用者介面所提供的[!UICONTROL 意見回饋]選項提供產品意見回饋

* 若要提供文件意見回饋，請使用右側邊欄提供的[!UICONTROL 編輯此頁面]![來編輯頁面](assets/do-not-localize/edit-page.png)或[!UICONTROL 記錄問題]![來建立 GitHub 問題](assets/do-not-localize/github-issue.png)

* 聯絡[客戶服務](https://experienceleague.adobe.com/?support-solution=General#support)
