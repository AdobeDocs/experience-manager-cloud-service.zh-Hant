---
title: 在表單中建立和管理審核
seo-title: Creating and managing reviews in forms
description: 「審核」是一種機制，可讓一或多位審核者對表單中可用的資產發表評論。
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
topic-tags: forms-manager
source-git-commit: 400e9fa0263b3e9bdae10dc80d524b291f99496d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# 建立和管理表單中資產的審核{#creating-and-managing-reviews-for-assets-in-forms}

## 評論 {#review}

審核是一種機制，可讓一或多位審核者對表單中可用的資產發表評論。

## 設定審核 {#setting-up-a-review}

1. 導覽至Forms標籤並選取表單。
1. 如果表單未進行審核，則啟動審核 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 圖示。 按一下「Start Review（開始審閱）」 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 表徵圖。
1. 輸入以下資訊：

   * 標題：必填，可包含英數字元、連字型大小或底線。
   * 說明：選用，說明用途/內容以供審核。
   * 截止日期：可選，審核結束的日期。 超過截止日期時，任務將顯示為「已逾期」。
   * 審閱者：至少必須有一個。 鍵入組名或用戶名將列出除服務用戶組之外的所有匹配名稱。 選取名稱，然後按一下「新增」 。

1. 按一下「開始」(Start)以開始審核。

>[!NOTE]
>
>* 管理員可以存取與表單使用者相關聯的任何群組。
>* 服務用戶組無法供選擇查看。


### 設定審核時發生的動作 {#actions-that-occur-when-a-review-is-set-up}

本節說明建立或設定審核時會發生什麼情況。

1. 將建立新審閱任務並分配給所選審閱者。
1. 所有審閱者都被分配一個審閱任務。 該任務將顯示在其「通知」部分中。 審核者可以按一下通知，或轉到收件箱查看任務。 審核者可以按一下以開啟審核任務、查看表單並開始添加註釋。

   ![審核者通知警報](assets/review-notification-img.png)

   審核者通知警報

1. 「表單」的審核者可使用注釋框。 其他人可以查看注釋，但無法寫入注釋。

## 管理審核 {#managing-a-review}

>[!NOTE]
>
>只能修改正在進行的審核。 無法修改已完成的審閱。

1. 導覽至Forms標籤並選取表單。

1. 如果資產正在進行審核，而您是審核的發起者，則管理審核 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 圖示會出現在動作列中。 只有審核啟動器可以管理（更新/結束）審核。

   按一下管理審閱 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)表徵圖。

   對於啟動器以外的用戶，「管理審閱」表徵圖被禁用。

1. 畫面會顯示資訊：

   * **標題**:無法編輯。

   * **說明**:可編輯。

   * **截止時間**:可編輯。 可以將截止日期修改為當前日期和時間以外的任何日期和時間。

   * **審核者名稱**:可編輯。 可以添加或刪除審閱者。 如果任務逾期，則只能在將截止日期延長到當前日期之後才添加審閱者。

1. 編輯必要欄位，然後按一下「完成」。

   ![在任務管理器中查看更新狀態](assets/manage-review-img.png)

   在任務管理器中查看更新狀態

1. 要結束審閱，請按一下「結束審閱」。

### 修改審核時發生的操作 {#actions-that-occur-when-a-review-is-modified}

本節說明檢閱更新/結束時會發生什麼事：

1. 如果修改了審閱描述，則會更新審閱者和發起者的相應任務。
1. 如果修改了「審閱」(Review)截止期，則審閱者的相應任務將以新日期更新。

1. 如果刪除審核者：

   ![移除審核者](assets/removeduser.png)

   移除審核者

   1. 如果未完成，則會終止分配的任務。
   1. 審核者無法再對表單進行注釋。

1. 如果已添加審核者：

   ![添加審核者](assets/addedreviewer.png)

   添加審核者

   1. 將建立審核任務並分配給新添加的審核者。
   1. 新添加的審核者可以添加有關表單的注釋。

1. 審核結束時：

   1. **審核者**:對於每個審閱者，與審閱相關的未完成任務將終止。 審核者的「通知」區段中不再將任務顯示為「待定」。
   1. **啟動器**:分配給審核啟動器的任務標籤為完成。 該任務將從審閱啟動器的「通知」部分中刪除。
   1. **全部**:審閱將顯示在「前一個審閱」(Previous Reviews)部分。 無法添加其他評論。
      ![檢閱完成](assets/review-complete-imgg.png)


