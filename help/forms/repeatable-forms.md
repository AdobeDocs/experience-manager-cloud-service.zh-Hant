---
description: 本教學課程包含讓表單的某個區段可重複的指示
title: Edge Delivery Services中的可重複區段
feature: Edge Delivery Services
source-git-commit: fd2e5df72e965ea6f9ad09b37983f815954f915c
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---


# 邊緣傳遞中的可重複區段

可重複區段是表單的一個元件，會重複或多次複製以收集相同資料多次出現的資訊。

例如，假設有一個表單，用於從申請貸款的使用者那裡收集資訊。 此表單可讓使用者提供個人資訊，包括共同貸款人的詳細資訊。 使用者可以輸入共同申請者的詳細資訊，此區段可重複。

![表單中的可重複區段](/help/forms/assets/eds-repeatable.png)

## 先決條件

使用AEM範本設定Edge Delivery Service (EDS) GitHub專案，並在本機電腦上複製對應的GitHub存放庫。 若需要詳細資訊，請參閱[開發人員教學課程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/build/tutorial.html) 。

## 邊緣傳遞中的可重複區段

以貸款申請表為例。 此表單可讓使用者提交個人資訊。 您可以使用重複部份來包含共同應徵者詳細資訊，並可選擇新增至少三個共同應徵者部份。

>[!NOTE]
>
> * 您可以在Microsoft Site或SharePoint Drive上撰寫Google Excel，使欄位集在表單中可重複。
> * 在此案例中，我們以Microsoft SharePoint為例。 若要將SharePoint資料夾設為內容來源，請依照中說明的步驟操作 [如何使用Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint).


若要在邊緣傳送中新增可重複區段：

1. [使用Microsoft Excel製作表單](#author-form)
2. [預覽和發佈表單](#preview-form)

### 使用Microsoft Excel製作表單 {#author-form}

1. 前往Microsoft SharePoint帳戶，開啟或建立AEM Edge Delivery專案目錄。
2. 開啟現有的Microsoft Excel檔案或建立新檔案。
在此範例中，我們使用名為的Excel工作表 `loan-application.xlsx` 在Microsoft SharePoint網站中建立。
3. 新增標示為「 」的新欄 `Repeatable`， `Min`、和 `Max` 在Microsoft Excel檔案中。
4. 指定 `Repeatable` 欄為 `True` 用於您要使其可重複的欄位集。
5. 指定 `Min` 和 `Max` 欄。 此 `Min` 值代表面板重複出現的最小次數，而 `Max` 值代表面板重複出現次數的上限。
6. 儲存您的Microsoft Excel檔案。

>[!NOTE]
>
> 以下是 [貸款申請](/help/forms/assets/loan-application.xlsx) excel工作表以供您參考。

### 使用您的Edge Delivery服務預覽/發佈表單

1. 在Microsoft SharePoint網站中開啟或建立新檔案檔案，以使用 `Form Block`. 例如，開啟 `index` 檔案並新增 `Form Block`.
2. 開啟命令提示字元，瀏覽至本機電腦上的AEM Edge Delivery專案目錄，然後以下列方式執行命令 `aem up`.

此表單的存取位置為 `https://localhost:3000`，按一下 `Add` 按鈕新增可重複區段，以輸入共同申請人詳細資訊。 您也可以按一下 `Delete` 按鈕。

>[!NOTE]
>
> 如果您在localhost存取表單時遇到「找不到頁面」錯誤，請在表單所在的URL前新增Microsoft SharePoint網站的目錄名稱。 例如 `http://localhost:3000/<dir-name>/`




