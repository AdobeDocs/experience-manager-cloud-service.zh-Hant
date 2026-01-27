---
title: 如何使用連結Forms Portal元件在AEM Sites頁面上新增表單連結？
description: 瞭解如何將表單連結新增至AEM Sites頁面。
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
exl-id: a55d0776-8827-46cc-9625-5d6f5f6bda3b
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 1%

---

# 將表單連結新增至網站頁面

在銀行網站情境中，**連結** Forms Portal元件可引導使用者瀏覽網站各區段的特定表單，藉以強化導覽。 它為策略性地放在整個網站中的表單（例如貸款申請、帳戶開立表單或意見調查）提供直接參考。 **Link**&#x200B;元件插入的連結可將使用者引導至Sites頁面中的特定Adaptive Forms。 例如，在銀行的網站上，匿名使用者可以存取一般查詢表單，而登入使用者則可以直接存取更安全的表單，例如貸款申請或交易授權表單。

![連結圖示](/help/forms/assets/link-forms.png)


## 將連結元件新增至您的網站頁面

若要將&#x200B;**Link**&#x200B;入口網站元件新增至您的網站頁面，請執行下列步驟：

1. 以&#x200B;**編輯**&#x200B;模式開啟AEM Sites頁面。
1. 移至&#x200B;**[!UICONTROL 頁面資訊]** > **[!UICONTROL 編輯範本]**
   ![編輯範本原則](/help/forms/assets/save-form-as-draft-edit-template.png)

1. 按一下&#x200B;**[!UICONTROL 原則]**，然後選取&#x200B;**[!UICONTROL AEM Archetype專案名稱]** - Forms和通訊入口網站&#x200B;**[下的]連結**&#x200B;核取方塊。

   ![原則選擇](/help/forms/assets/add-link.png)

1. 按一下&#x200B;**[!UICONTROL 完成]**。
1. 現在，請在撰寫模式中重新開啟AEM Sites頁面。
1. 在頁面編輯器中找出區段，讓您新增Forms Portal元件。

1. 按一下&#x200B;**新增**&#x200B;圖示。 圖示是加號(+)，表示可新增元件的選項。

   按一下&#x200B;**新增**&#x200B;圖示會顯示&#x200B;**插入新元件**&#x200B;對話方塊，其中顯示要插入的各種元件。

   >[!NOTE]
   >
   > 或者，您也可以拖放元件。

1. 瀏覽對話方塊中的可用元件，並從清單中選取所需元件。 例如，從清單中選取&#x200B;**Link**&#x200B;元件，以新增&#x200B;**Link** Forms Portal元件。

   ![連結元件](/help/forms/assets/add-link-in-sites.png)

現在設定&#x200B;**連結**&#x200B;元件的屬性。

## 瞭解連結元件的屬性

您可以使用[設定]對話方塊輕鬆自訂&#x200B;**連結**&#x200B;元件屬性，以提供順暢的使用者體驗。 若要設定，請選取元件，然後選取![設定圖示](assets/configure_icon.png)。 **[!UICONTROL 連結]**&#x200B;對話方塊開啟。

### 顯示標籤

![顯示標籤](/help/forms/assets/link-asset-tab.png)

在&#x200B;**[!UICONTROL 顯示]**&#x200B;索引標籤中，提供連結標題和工具提示，以方便識別連結所代表的表單。

### 資產資訊索引標籤

![Assets資訊標籤](/help/forms/assets/link-asset-info.png)

在&#x200B;**[!UICONTROL 資產資訊]**&#x200B;索引標籤中，指定儲存資產的存放庫路徑。

### 查詢引數索引標籤

![查詢引數標籤](/help/forms/assets/link-query-tab.png)

在&#x200B;**[!UICONTROL 查詢引數]**&#x200B;索引標籤中，以索引鍵值配對格式指定其他引數。 按一下連結時，這些額外的引數會與表單一起傳遞。

## 使用連結元件檢視「網站」頁面上的表單連結

預覽Sites頁面以檢視最適化表單的連結，該表單已在&#x200B;**Link**&#x200B;元件的&#x200B;**Assets資訊**&#x200B;屬性標籤中指定。 按一下連結後，畫面就會顯示表單，供使用者根據許可權存取。

![查詢引數標籤](/help/forms/assets/link-forms.png)

## 相關的文章

{{forms-portal-see-also}}

## 另請參閱 {#see-also}

{{see-also}}
