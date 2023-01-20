---
title: 在範例 React 應用程式中自訂內容
description: 使用範例 React 應用程式，了解如何使用 AEM as a Cloud Service 中的 Headless 功能集來自訂內容。
hidefromtoc: true
index: false
exl-id: 32290ad4-d915-41b7-a073-2637eb38e978
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: ht
source-wordcount: '1070'
ht-degree: 100%

---


# 在範例 React 應用程式中自訂內容 {#customize-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app"
>title="在範例 React 應用程式中自訂內容"
>abstract="您的 AEM Headless 試用版整合了範例 React 應用程式，您可以對其進行自訂。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide"
>title="啟動內容片段編輯器"
>abstract="您的 AEM Headless 試用版與範例 React 應用程式整合在一起，因此大家無需開發時間即可獨立管理內容，這一切就是如此簡單。<br><br>點選下方，在新標籤中啟動此單元，然後按照本指南進行操作。"
>additional-url="https://video.tv.adobe.com/v/328618" text="自訂應用程式介紹影片"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide_footer"
>title="在本模式中，您已瞭解如何自訂範例 React 應用程式。 <br><br>上市時間：加速！<br>開發週期：減少！<br><br>現在您已瞭解對於由 AEM Headless 功能提供支援的網站和應用程式來說，管理 Headless 內容是多麼容易。"
>abstract=""

## 預覽應用程式 {#preview}

按一下上面的「**啟動內容片段編輯器**」按鈕，在新標籤中打開內容片段模式編輯器。

![內容片段編輯器](assets/customize-app/content-fragment-editor.png)

AEM Headless 試用版隨附的範例應用程式，由透過 GraphQL 提供的內容片段提供支援。使用內容片段編輯器透過預覽範例來熟悉內容。

1. 在編輯器畫面的右上方，點選或按一下「**預覽**」按鈕。

1. 示範應用程式會在新標籤中開啟。該應用程式適用於虛構的 WKND 戶外生活方式品牌。按一下不同內容，以導覽範例內容。

   ![示範應用程式預覽](assets/customize-app/preview-demo-app.png)

1. 返回內容片段編輯器的瀏覽器標籤，並且繼續。

## 在應用程式中編輯標題 {#edit-app}

內容片段編輯器會將應用程式的基本版面顯示為頁面內容片段。 **面版**&#x200B;代表應用程式的不同頁面，每個頁面都是自己的內容片段。 透過修訂這些片段，您可以變更應用程式的內容。

1. 點選或按一下「**峽谷中的越野騎士**」，在「**面版**」區段中。

   ![點選「峽谷中的越野騎士」片段](assets/customize-app/mtn-biker-in-canyon.png)

1. 編輯器會開啟越野車的應用程式標題面板。 每個面板都由圖層組成，代表構成體驗的不同影像和文字。

   ![面板](assets/customize-app/panels.png)

1. 選取文字層「**峽谷中的越野騎士文字層**」。 這將在編輯器中開啟內容層的詳細資訊。 該圖層由多個內容片段組成，這些片段控制應用程式面板中顯示的文字。

   ![選取「峽谷中的越野騎士」標題](assets/customize-app/mtn-biker-in-canyon-text-layer.png)

1. 選取「**峽谷中的越野騎士標題**」文字項目。 如此將可開啟內容片段編輯器。 

   ![選取「峽谷中的越野騎士標題」文字項目](assets/customize-app/mtn-biker-in-canyon-title.png)

1. 將文字從 `Your next great adventure is calling` 變更為 `Choose your own adventure`。 此變更會由編輯器自動儲存。

1. 在視窗的右上方，點選或按一下「**預覽**」按鈕，查看您所做的變更。示範應用程式預覽會在新標籤中開啟。

   ![示範應用程式預覽](assets/customize-app/preview-demo-app-text.png)

整合到 AEM Headless CMS 後，更新 React 應用程式中的內容就是這麼容易。

## 在應用程式中交換影像 {#change-image}

現在您已經修改了應用程式中的標題，請嘗試變更影像。 

1. 返回內容片段編輯器的瀏覽器標籤。

1. 您需要返回到內容片段編輯器中的正確位置。編輯器左上方的階層連結顯示您在內容層次結構中的位置。 在階層連結中，點選或按一下「**峽谷中的越野騎士**」，可返回該頁面。

   ![階層連結](assets/customize-app/breadcrumbs.png)

1. 選取「**騎越野車 - 騎士**」影像層。 如此將可開啟內容片段編輯器

   ![編輯影像片段](assets/customize-app/mtn-biking-biker.png)

1. 點選或按一下 **X** 以刪除騎士的影像。 影像會消失且編輯器會顯示錯誤，因為影像是此內容片段模式所需的資料。

   ![從片段移除的影像](assets/customize-app/mtn-biking-biker-no-image.png)

1. 點選或按一下&#x200B;**新增資產**。

1. **選取資產** 對話框隨即開啟，路徑 **sample-wknd-app** > **en** > **image-files** 會自動選取。

1. 選取 `biker-yellow.png` 影像，然後點選或按一下「**選取**」。

   ![選取資產](assets/customize-app/select-asset.png)

1. 騎士影像會更換為所選影像。 編輯器會自動儲存這些變更。

   ![騎士影像的已編輯片段](assets/customize-app/mtn-biking-biker-edited.png)

1. 在視窗的右上方，點選或按一下「**預覽**」按鈕，查看您所做的變更。示範應用程式預覽會在新標籤中開啟。 在瀏覽器上按一下重新整理，您應該會在應用程式中看到穿著黃色短褲騎士的新影像。

使用 AEM Headless CMS 可以輕鬆更新應用程式中的影像和資產。

## 在應用程式中新增對新內容片段的參考 {#create-moment}

現在您已經更新了騎士的影像，讓我們來看看如何透過建立和參考新的內容片段，來將內容新增到應用程式。您將把由「可購物機會」內容片段管理的產品標註，新增到應用程式的第二個面板。

![可購物機會範例](assets/customize-app/example-shoppable-moment.png)

1. 返回內容片段編輯器的瀏覽器標籤。

1. 您需要返回到內容片段編輯器中的正確位置。編輯器左上方的階層連結顯示您在內容層次結構中的位置。 在階層連結中，點選或按一下「**WKND 首頁**」，可返回該頁面。

   ![導覽回到版面螢幕](assets/customize-app/breadcrumbs-2.png)

1. 選取「**在 WKND 黃色的越野騎士**」面板。

   ![建立一個「可購物機會」](assets/customize-app/mtn-biker-on-wknd-yellow.png)

1. 選取「**騎越野車 - 可購物**」圖層。 

   ![選取「可購物機會」圖層](assets/customize-app/mtn-biking-shoppable.png)

1. 為了在此面板上建立新的標註，您必須建立一個新的可購物機會內容片段。點選或按一下「**+ 建立新片段**」按鈕。

   ![新增一個「可購物機會」](assets/customize-app/create-new-fragment.png)

1. 您必須首先選擇新內容片段所根據的模式。選取「**可購機會商品**」模式 (從「**內容片段模式**」下拉式清單)。

1. 為內容片段命名。例如，在欄位中輸入 `Shorts` (在「**名稱**」欄位中)。

   ![為可購物機會命名](assets/customize-app/new-content-fragment.png)

1. 點選或按一下「**建立並開啟**」。

1. 編輯器會為您的新內容片段開啟。

1. 在「**文字**」欄位內為可購物機會命名，例如命名為 `Yellow shorts`。

1. 設定 **X** 和 **Y** 的值。這是此標註應覆蓋在面板上的位置。編輯器會自動儲存片段的變更
   * **X**: `-18`
   * **Y**: `-28`

   ![編輯可購物機會](assets/customize-app/edit-shoppable-moment.png)

1. 在視窗的右上方，點選或按一下「**預覽**」按鈕，查看您所做的變更。示範應用程式預覽會在新標籤中開啟。 按一下瀏覽器上的重新整理以測試位置，並根據需要在編輯器中進行調整。

現在您已瞭解如何在沒有任何開發週期的情況下完成建立新內容，並將其作為應用程式中的內容片段進行參考。
