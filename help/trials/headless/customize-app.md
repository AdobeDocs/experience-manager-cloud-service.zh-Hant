---
title: 自訂範例React應用程式中的內容
description: 使用範例React應用程式，了解如何使用AEM as a Cloud Service中的無頭功能集來自訂內容。
hidefromtoc: true
index: false
source-git-commit: 62c8be81d0d46e69b44cc803419fafcce2e93d33
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 0%

---


# 自訂範例React應用程式中的內容 {#customize-app}

無頭的AEM試用預先載入簡單的React應用程式，以展示無頭內容。 在此模組中，您將學習如何透過交換影像和為其建立可購買的時刻來預覽該應用程式並修改其內容。

應用程式本身以內容片段的結構為基礎。 您可以使用AEM中的內容片段編輯器，修改應用程式內容。 為協助您了解如何完成此作業，此AEM Trials模組會透過快速互動導覽，帶您完成此程式。 本檔案是互動式導覽的補充，涵蓋相同步驟，並視需要連結至其他資源。

## 內容片段編輯器 {#fragment-editor}

您從範例應用程式的內容片段編輯器中開始。

![內容片段編輯器](assets/customize-app/content-fragment-editor.png)

如果您想自行導覽至應用程式內指引以外的內容片段編輯器，請使用頁面左上角的Adobe圖示找到。 這會開啟AEM的全域導覽。 從這裡，您選擇 **導覽** 標籤，然後 **內容片段**.

![在內容片段主控台中導覽至應用程式](assets/customize-app/navigate-to-app.png)

這會開啟內容片段主控台。 從那裡，您可以使用左側面板的內容樹狀結構，導覽至應用程式內容的位置。 在此案例中， **內容片段** -> **範例WKND應用程式** -> **英文** -> **內容片段** -> **頁面**.

點選或按一下 **WKND首頁** 顯示在內容樹狀結構右側的主控台中的頁面片段，以啟動應用程式內容的編輯器。

>[!TIP]
>
>如果您想進一步了解AEM中的導覽，請參閱 [「其他資源」部分](#additional-resources) ，以取得AEM基本處理的詳細資訊。

## 預覽應用程式 {#preview}

開始修改應用程式之前，請先透過預覽其目前狀態來熟悉應用程式。 點選或按一下 **預覽** 按鈕。

示範應用程式會在新標籤中開啟。

![示範應用程式預覽](assets/customize-app/preview-demo-app.png)

這款應用本身是一款簡單的電子商務應用，適用於虛構的WKND戶外生活風格品牌，在React中實現。 按一下以導覽範例內容。

返回內容片段編輯器的索引標籤以繼續。

## 編輯應用程式中的文字 {#edit-app}

如前所述，應用程式本身由內容片段組成。 這些片段在結構中連結在一起，以建立應用程式。

內容片段編輯器會將應用程式的基本版面顯示為頁面。 此頁面是內容片段，其本身是其他片段的集合。 此 **面板** 代表應用程式的不同頁面，每個頁面都是其專屬的內容片段。 您可以修改這些片段，以變更應用程式的內容。

1. 點選或按一下 **美恩峽谷腳踏車** 在 **面板** 區段。

   ![在峽谷碎片中點擊Mtn腳踏車](assets/customize-app/mtn-biker-in-canyon.png)

1. 編輯器會開啟山地摩托車手的標題面板。 每個面板都由圖層組成，代表應用程式頁面內的不同內容。

   ![面板](assets/customize-app/panels.png)

1. 選取文字層 **峽谷文本層中的Mtn腳踏車**. 這會開啟編輯器中圖層的詳細資訊。 圖層由多個內容片段組成。

   ![在峽谷標題中選擇Mtn摩托車](assets/customize-app/mtn-biker-in-canyon-text-layer.png)

1. 選取 **峽谷標題中的Mtn摩托車手** 文字項目。 這會開啟內容片段編輯器，顯示此片段的內容並允許您修改它。

   ![在「峽谷標題」(Canyon Title)文本項中選擇Mtn騎行者](assets/customize-app/mtn-biker-in-canyon-title.png)

1. 將文字從 `Your next great adventure is calling` to `Choose your own adventure`. 編輯器會自動儲存變更。

1. 按一下預覽以查看變更。 示範應用程式會在新標籤中開啟。

   ![示範應用程式預覽](assets/customize-app/preview-demo-app-text.png)

返回內容片段編輯器的索引標籤以繼續模組。

## 變更應用程式的主影像 {#change-image}

現在您已修改應用程式中的文字，請嘗試變更應用程式的主影像。 首先，您需要找到該內容。

編輯器左上角的階層連結會顯示您在內容階層中的位置。

1. 點選或按一下 **美恩峽谷腳踏車** 以返回該頁面。

   ![階層連結](assets/customize-app/breadcrumbs.png)

1. 使用應用程式的各種圖層返回面板。 圖層不僅表示文本內容。 它們代表您應用程式中的所有內容。 因此，您也可以使用內容片段編輯器交換影像。

   ![面板](assets/customize-app/panels.png)

1. 選取 **Mtn騎腳踏車 — 腳踏車** 影像層。 這會開啟內容片段編輯器，顯示此片段的內容並允許您修改它。

   ![編輯影像片段](assets/customize-app/mtn-biking-biker.png)

1. 點選或按一下 **X** 移除摩托車手影像。 影像會消失，而編輯器會顯示錯誤，因為影像是此內容片段模型的必要資料。

   ![從片段中移除的影像](assets/customize-app/mtn-biking-biker-no-image.png)

1. 點選或按一下 **新增資產** 並在 **sample-wknd-app** > **en** > **影像檔案**. 使用 **選取資產** 對話框，導航內容層次結構。

   ![選取資產對話方塊](assets/customize-app/select-assets.png)

1. 篩選文字 `yellow`. 使用 **搜尋所有資產** 欄位 **選取資產** 窗口，搜索影像。 輸入搜索文本，然後按Enter鍵或返回搜索。

   ![搜尋資產](assets/customize-app/search-assets.png)

1. 點選或按一下以選取 `biker-yellow.png` 影像，然後點選或按一下 **選擇**.

   ![選取資產](assets/customize-app/select-asset.png)

1. 腳踏車的影像已被選定影像替換。 編輯器會自動儲存變更。

   ![編輯的腳踏車影像片段](assets/customize-app/mtn-biking-biker-edited.png)

## 建立可購買的時刻 {#create-moment}

現在你更新了摩托車手的影像，你可以為摩托車手的黃色短褲添加一個可購買的時刻。

1. 首先，返回頁面片段的內容片段編輯器。 編輯器左上角的階層連結會顯示您在內容階層中的位置。 點選或按一下 **WKND首頁** 以返回該頁面。

   ![導覽回版面畫面](assets/customize-app/breadcrumbs-2.png)

1. 選取 **WKND黃色的Mtn摩托車手** 中。

   ![建立可購買的時刻](assets/customize-app/mtn-biker-on-wknd-yellow.png)

1. 你現在可以看到構成摩托車手影像的圖層。 選取 **Mtn騎腳踏車 — 可購買** 圖層。

   ![選擇可購買的矩層](assets/customize-app/mtn-biking-shoppable.png)

1. 若要建立可購買的時刻，您必須建立代表該時刻的新內容片段。 點選或按一下 **+建立新片段** 為腳踏車的短褲增加可購買的時刻。

   ![添加可購買的時刻](assets/customize-app/create-new-fragment.png)

1. 因為內容片段代表結構化無頭資料，每當您建立內容片段時，您必須先選擇要為其建立的模型。 選取 **可購買矩形項** 從 **內容片段模型** 下拉式清單。

   ![選擇內容片段模型](assets/customize-app/new-content-fragment.png)

1. 為將代表這個新可購買瞬間的內容片段命名。 例如，輸入 `Shorts` 進入 **名稱** 欄位。

   ![為可購買的時刻命名](assets/customize-app/new-content-fragment.png)

1. 點選或按一下 **建立和開啟**.

1. 會針對您的新內容片段開啟編輯器。
   * 在中為可購買的時刻命名 **文字** 欄位，例如 `Yellow shorts`.
   * 設定X和Y，以覆蓋此可購物瞬間的位置。
      * **X**: `-18`
      * **Y**: `-28`
   * 編輯器會自動儲存對片段的變更

   ![編輯可購買的時刻](assets/customize-app/edit-shoppable-moment.png)

1. 點選或按一下 **預覽** 測試此定位並視需要進行調整。

   ![預覽您的新可購買時刻](assets/customize-app/preview-demo-app-shoppable.png)

## 您已學會自訂範例React應用程式！ {#conclusion}

在本模組中，您已學會如何自訂範例React應用程式。 首先，您學會了如何編輯現有文字。 接著，影像會與該影像的另一個例項交換。 最後，您看到了如何建立和定位可購買的力矩項。

請務必查看 [「其他資源」部分](#additional-resources) 以取得有關使用AEM及其內容片段的其他資源。

如果您想要了解如何建立內容片段和無標題內容以供自訂應用程式使用，您可以先檢閱模組 [建立應用程式的內容結構。](content-structure.md)

您可以按一下，返回試用主螢幕 **解決方案** 按鈕，然後選擇 **Experience Manager**.

![導覽首頁](assets/customize-app/home.png)

## 其他資源 {#additional-resources}

如需內容片段和AEM的詳細資訊，請考慮檢閱此額外檔案。

* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 內容片段模型的完整檔案
* [內容片段](/help/assets/content-fragments/content-fragments.md)  — 內容片段的概觀和內容片段完整檔案的連結
* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 如何為新使用者導覽和使用AEM的檔案
