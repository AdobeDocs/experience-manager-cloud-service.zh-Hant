---
title: 重構工具快速入門
description: 瞭解如何開始使用AEM as a Cloud Service中的重構工具
exl-id: 84394bdd-2b92-4f5d-b08a-7dc2c681baa4
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 4%

---

# 重構工具快速入門 {#getting-started-refactoring-tools}

## 可用性 {#availability}

<!-- Alexandru: duplicate contextualhelp id, drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_rs_upload"
>title="Download"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=zh-Hant" text="Release Notes"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution Portal"

-->

## 執行重構工具 {#running-refactoring-tools}

使用重構工具來移轉您的程式碼，以與AEM as a Cloud Service相容。

1. 如果您尚未建立CAM專案，請參閱[在CAM中建立和管理專案](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md#create-project)。
1. 按一下&#x200B;**程式碼重構**&#x200B;卡片以上傳原始程式碼。

   ![影像](/help/journey-migration/refactoring-tools/assets/rscam1.png)

1. 第一次存取&#x200B;**Source程式碼檢視**&#x200B;時，您會看到空白狀態，提示您上傳原始程式碼。

   ![影像](/help/journey-migration/refactoring-tools/assets/rscam2.png)

## 上傳Source程式碼 {#uploading}

客戶首次存取&#x200B;**重構工具**&#x200B;時，**Source程式碼檢視**&#x200B;中會顯示空白狀態。 請依照下列步驟上傳您的專案並開始進行檢查程式：

1. **存取專案上傳頁面**\
   按一下處於空白狀態的&#x200B;**專案上傳**&#x200B;按鈕以開始上傳程式。

   ![影像](/help/journey-migration/refactoring-tools/assets/rscam3.png)

1. **上傳您的Source程式碼**
   - 在上傳對話方塊中，選取您的原始碼ZIP檔案。
   - 按一下&#x200B;**上傳**&#x200B;開始。
   - 上傳進度將顯示在對話方塊中。 持續時間取決於您的專案大小。

   ![影像](/help/journey-migration/refactoring-tools/assets/rscam4.png)

1. **檢查程式**
   - 上傳之後，**檢查程式**&#x200B;會在背景自動開始。
   - **Source程式碼檢視**&#x200B;現在會顯示您上傳的專案及其檢查狀態。

1. **檢查狀態**&#x200B;檢查程式的設計目的是透過減少手動設定的額外負荷，來簡化重構工具的執行。

   檢查會顯示下列其中一種狀態：
   - **正在執行** — 檢查正在進行中。
   - **就緒** — 檢查已完成；您現在可以執行重構工具。
   - **失敗** — 發生錯誤。 按一下專案以複查檢查報告並解決任何問題。

   ![影像](/help/journey-migration/refactoring-tools/assets/rscam5.png)

>[!NOTE]
>
>上傳新專案將會刪除現有專案。 在繼續之前，請確定已儲存任何必要的資料。

>[!NOTE]
>
>只有在原始程式碼上傳成功時，才能執行重構作業。

## 重構工作 {#refactoring-jobs}

當您按一下「**重構工作**」標籤時，您將會看到現有工作的清單。 如果尚未建立任何工作，則會顯示空白狀態以提示建立工作。

![影像](/help/journey-migration/refactoring-tools/assets/rscam6.png)

### 1.建立新的重構工作

- 按一下&#x200B;**建立新工作**&#x200B;按鈕。
- 選取所需的重構工具。
- 按一下&#x200B;**開始**&#x200B;以啟動重構程式。

![影像](/help/journey-migration/refactoring-tools/assets/rscam7.png)

>[!NOTE]
>
>您可以使用&#x200B;**所有工具一起**&#x200B;選項，觸發個別重構工作或一次執行所有可用工具。

### 2.工作狀態

- **執行中** — 工作目前正在進行中。 狀態會在完成或失敗時自動更新。
- **已完成** — 工作已成功完成。 您現在可以檢閱結果或下載重構的程式碼。
- **失敗** — 工作發生錯誤。 按一下工作以檢視詳細記錄檔並疑難排解問題。

![影像](/help/journey-migration/refactoring-tools/assets/rscam8.png)

當工作成功完成時，**下載**&#x200B;按鈕將變為可用，可讓您擷取：

- **重構的專案**：這是套用轉換後的更新程式碼。 客戶可下載專案的最新程式碼。
- **活動記錄**：在作業執行期間，工具執行的所有步驟以及所做的變更都會記錄為此作業的一部分。
- **發現專案報告**：此報告包含工具未完全執行但仍需要處理的專案。 所有這類變更都會記錄在這裡。

![影像](/help/journey-migration/refactoring-tools/assets/rscam9.png)

>[!NOTE]
>
>每項工作最多需要1小時才能完成。 如果狀態未更新，請聯絡Adobe支援。
