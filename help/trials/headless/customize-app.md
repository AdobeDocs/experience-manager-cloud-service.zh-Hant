---
title: 在範例 React 應用程式中自訂內容
description: 使用範例 React 應用程式，了解如何使用 AEM as a Cloud Service 中的 Headless 功能集來自訂內容。
hidefromtoc: true
index: false
exl-id: 32290ad4-d915-41b7-a073-2637eb38e978
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 38%

---


# 在範例 React 應用程式中自訂內容 {#customize-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app"
>title="在範例 React 應用程式中自訂內容"
>abstract="您的AEM無頭試用版整合了範例React應用程式，供您自訂。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide"
>title="啟動內容片段編輯器"
>abstract="您的AEM無頭式試用版已與範例React應用程式整合，讓您了解在無需開發時間的情況下，任何人獨立管理內容有多簡單。<br><br>按一下下方的，然後依照本指南在新標籤中啟動此模組。"
>additional-url="https://video.tv.adobe.com/v/328618" text="自訂應用程式簡介影片"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide_footer"
>title="在本模式中，您已了解如何自訂範例 React 應用程式。 <br><br>上市時間：加速！<br>開發週期：縮小！<br><br>現在，您已了解對於採用AEM無頭功能技術的網站和應用程式而言，無頭內容的管理有多簡單。"
>abstract=""

## 預覽應用程式 {#preview}

按一下 **啟動內容片段編輯器** 按鈕會在新索引標籤中開啟內容片段編輯器。

![內容片段編輯器](assets/customize-app/content-fragment-editor.png)

隨AEM無頭試用版提供的範例應用程式，由透過GraphQL傳送的內容片段提供技術支援。 使用內容片段編輯器來預覽範例以熟悉內容。

1. 在編輯器畫面的右上方，點選或按一下「**預覽**」按鈕。

1. 示範應用程式會在新標籤中開啟。這款應用面向虛構的WKND戶外生活風格品牌。 按一下不同內容，以導覽範例內容。

   ![示範應用程式預覽](assets/customize-app/preview-demo-app.png)

1. 返回內容片段編輯器的瀏覽器索引標籤以繼續。

## 在應用程式中編輯標題 {#edit-app}

內容片段編輯器會將應用程式的基本版面顯示為頁面內容片段。 **面版**&#x200B;代表應用程式的不同頁面，每個頁面都是自己的內容片段。 透過修訂這些片段，您可以變更應用程式的內容。

1. 點選或按一下「**峽谷中的越野騎士**」，在「**面版**」區段中。

   ![點選「峽谷中的越野騎士」片段](assets/customize-app/mtn-biker-in-canyon.png)

1. 編輯器會開啟山地摩托車應用程式的標題面板。 每個面板都由圖層組成，分別代表構成體驗的不同影像和文字。

   ![面板](assets/customize-app/panels.png)

1. 選取文字層「**峽谷中的越野騎士文字層**」。 這將在編輯器中開啟內容層的詳細資訊。 圖層由多個內容片段組成，可控制應用程式此面板中顯示的文字。

   ![選取「峽谷中的越野騎士」標題](assets/customize-app/mtn-biker-in-canyon-text-layer.png)

1. 選取「**峽谷中的越野騎士標題**」文字項目。 這會開啟內容片段編輯器。

   ![選取「峽谷中的越野騎士標題」文字項目](assets/customize-app/mtn-biker-in-canyon-title.png)

1. 將文字從 `Your next great adventure is calling` 變更為 `Choose your own adventure`。 此變更會由編輯器自動儲存。

1. 點選或按一下 **預覽** ，查看您的更改。 示範應用程式的預覽會在新索引標籤中開啟。

   ![示範應用程式預覽](assets/customize-app/preview-demo-app-text.png)

這就是整合至AEM無頭CMS時，更新React應用程式內容的簡易性。

## 在應用程式中交換影像 {#change-image}

現在您已修改應用程式中的標題，請嘗試變更影像。

1. 返回內容片段編輯器的瀏覽器標籤。

1. 您必須回到內容片段編輯器中的正確位置。 編輯器左上方的階層連結顯示您在內容層次結構中的位置。 在階層連結中，點選或按一下「**峽谷中的越野騎士**」，可返回該頁面。

   ![階層連結](assets/customize-app/breadcrumbs.png)

1. 選取「**騎越野車 - 騎士**」影像層。 這會開啟內容片段編輯器

   ![編輯影像片段](assets/customize-app/mtn-biking-biker.png)

1. 點選或按一下 **X** 以刪除騎士的影像。 影像會消失且編輯器會顯示錯誤，因為影像是此內容片段模式所需的資料。

   ![從片段移除的影像](assets/customize-app/mtn-biking-biker-no-image.png)

1. 點選或按一下 **新增資產**.

1. 此 **選取資產** 對話框開啟，路徑 **sample-wknd-app** > **en** > **影像檔案** 會自動為您選取。

1. 選取影像 `biker-yellow.png` 然後點選或按一下 **選擇**.

   ![選取資產](assets/customize-app/select-asset.png)

1. 腳踏車的影像被選定影像替換。 編輯器會自動儲存這些變更。

   ![騎士影像的已編輯片段](assets/customize-app/mtn-biking-biker-edited.png)

1. 點選或按一下 **預覽** ，查看您的更改。 示範應用程式的預覽會在新索引標籤中開啟。 按一下瀏覽器上的重新整理，應用程式中應該會看到新的腳踏車車影像，內含黃色短褲。

使用AEM無頭CMS即可輕鬆更新應用程式中的影像和資產。

## 將參考新增至應用程式中的新內容片段 {#create-moment}

現在您已更新摩托車手的影像，接下來讓我們逐步說明如何建立並參考新的內容片段，以新增內容至應用程式。 您會將由「可購買時刻」內容片段管理的產品呼叫新增至應用程式的第二個面板。

![可購買的時刻示例](assets/customize-app/example-shoppable-moment.png)

1. 返回內容片段編輯器的瀏覽器標籤。

1. 您必須回到內容片段編輯器中的正確位置。 編輯器左上方的階層連結顯示您在內容層次結構中的位置。 在階層連結中，點選或按一下「**WKND 首頁**」，可返回該頁面。

   ![導覽回到版面螢幕](assets/customize-app/breadcrumbs-2.png)

1. 選取「**在 WKND 黃色的越野騎士**」面板。

   ![建立一個「可購物機會」](assets/customize-app/mtn-biker-on-wknd-yellow.png)

1. 選取 **Mtn騎腳踏車 — 可購買** 圖層。

   ![選取「可購物機會」圖層](assets/customize-app/mtn-biking-shoppable.png)

1. 若要在此面板上建立新的呼叫，您必須建立新的可購買時間內容片段。 點選或按一下 **+建立新片段** 按鈕。

   ![新增一個「可購物機會」](assets/customize-app/create-new-fragment.png)

1. 您必須先選擇新內容片段的基礎模型。 選取「**可購機會商品**」模式 (從「**內容片段模式**」下拉式清單)。

1. 為內容片段命名。 例如，在欄位中輸入 `Shorts` (在「**名稱**」欄位中)。

   ![為可購物機會命名](assets/customize-app/new-content-fragment.png)

1. 點選或按一下「**建立並開啟**」。

1. 編輯器會為您的新內容片段開啟。

1. 在「**文字**」欄位內為可購物機會命名，例如命名為 `Yellow shorts`。

1. 設定 **X** 和 **Y**. 此區域應覆蓋在面板上。 編輯器會自動儲存片段的變更
   * **X**: `-18`
   * **Y**: `-28`

   ![編輯可購物機會](assets/customize-app/edit-shoppable-moment.png)

1. 點選或按一下 **預覽** ，查看您的更改。 示範應用程式的預覽會在新索引標籤中開啟。 按一下瀏覽器上的重新整理，以測試定位，並視需要在編輯器中進行調整。

現在您已了解如何在應用程式中建立新內容並以內容片段形式加以參照，而不需任何開發週期。
