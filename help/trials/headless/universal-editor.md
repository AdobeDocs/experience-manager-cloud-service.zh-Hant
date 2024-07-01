---
title: 使用 Universal Editor 進行內容編輯
description: 探索如何使用 Universal Editor 在任何實作中對內容的任何層面進行就地和內容編輯。
hidefromtoc: true
index: false
exl-id: a4854a56-9434-4d15-a56a-f1798f27263a
feature: Headless
role: Admin, User, Developer
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: ht
source-wordcount: '886'
ht-degree: 100%

---


# 使用 Universal Editor 進行內容編輯 {#editing-in-context}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_edit_inline_universal_editor"
>title="使用 Universal Editor 進行內容編輯"
>abstract="了解 Headless 應用程式如何使用 Universal Editor 為作者帶來低摩擦且符合上下文的編輯體驗。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_edit_inline_universal_editor_guide"
>title="啟動 Universal Editor"
>abstract="在本指南中，您將深入瞭解 Universal Editor，以及它如何讓所有人都能在任何實施中編輯各種內容，從而提高內容速度。<br><br>點選下方，在新標籤中啟動此單元，然後按照本指南進行操作。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_edit_inline_universal_editor_guide_footer"
>title="在本單元中，您已了解如何使用 Universal Editor 自訂符合上下文且原地出現的內容。"
>abstract=""

## 在內容中編輯文字 {#edit-text}

進行原處和內容中編輯通常會比您在之前的模組中看過的結構化 Headless 內容編輯 (如使用內容片段編輯器) 更具優勢。

>[!NOTE]
>
>若要在此試用版中使用 Universal Editor，您必須使用 Chrome 作為瀏覽器，並且不能使用無痕模式。這是試用體驗的限制，並非 Universal Editor 的問題。

使用 Universal Editor 可讓您靈活地進行內容中和原處的文字編輯，實現簡單且直覺的內容製作。

1. 按兩下以選取最新文章的標題即可進行編輯。

   ![Universal Editor](assets/do-not-localize/ue-component-mode.png)

1. 選取的元件會以藍色邊框顯示，且會附上註明其為文字元件的標籤。游標會位於邊框中，等待文字輸入。將文字變更為 `Aloha Spirit in Lofoten`。

   ![在 Universal Editor 中編輯文字](assets/do-not-localize/ue-edit-text-2.png)

1. 選取文字元件以外的地方，您的變更就會自動儲存。

Universal Editor 在製作環境中會自動儲存您的變更。您仍然需要發佈變更內容，讀者才能看到，我們將在稍後的步驟中進行這部分。

## 在內容中編輯媒體 {#edit-media}

使用 Universal Editor，您還可以在將影像交換出去的同時仍停留在內容中。

1. 選取衝浪者的影像將其選取。

1. 在元件邊欄中，您可以查看資產的詳細資料。選擇「**精選影像**」縮圖。

   ![選取要編輯的影像](assets/do-not-localize/ue-edit-media.png)

1. 在「**選取資產**」視窗中，向下捲動並選取 `surfer-wave-02.JPG` 影像。

1. 選取「**選取**」，在「**選取資產**」視窗。

   ![使用「選取資產」視窗選取影像](assets/do-not-localize/ue-select-asset.png)

該影像會以您選取的影像取代。

## 像讀者一樣體驗您的內容 {#emulators}

Universal Editor 可讓您在其中與內容互動、查看傳遞到使用者裝置上的內容。

1. 根據預設，編輯器會呈現內容的桌面版本。選取 Universal Editor 工具列右上角的模擬器按鈕，即可變更目標裝置。

   ![模擬器選單項目](assets/do-not-localize/ue-emulator-1.png)

1. 讀者可能使用外觀比例不同的不同裝置，因此編輯器會提供模擬模式，以便查看頁面呈現在使用者面前的樣子。例如，選取直向模式的行動裝置選項。

   ![模擬器選單項目](assets/do-not-localize/ue-emulator-2.png)

1. 在編輯器中查看內容變更。模擬器的圖示也會變更，以反映其所處的模式。選取模擬器選單以外的任意位置可以關閉模擬器並與您的內容進行互動。

1. 讓模擬器返回桌面模式。

您也可以指定模擬器的實際尺寸並旋轉模擬的裝置，以便在任何可能的目標裝置上檢視您的內容。

## 預覽和發佈 {#preview}

由於您必須選取內容才能在編輯器進行修改，因此編輯器不允許透過點選或按一下來進入連結或與內容互動。使用預覽模式的話，您可以在發佈之前使用內容中的連結，像使用者一樣進行體驗。

1. 在 Universal Editor 工具列中，選取「**預覽**」。

1. 現在選取主要文章的「**閱讀更多**」連結。

   ![預覽模式](assets/do-not-localize/ue-preview-publish-1.png)

1. 瀏覽文章，然後使用&#x200B;**返回**&#x200B;連結，返回主要頁面。

   ![使用返回連結返回主要頁面](assets/do-not-localize/ue-preview-publish-3.png)

1. 現在選取編輯器右上角的「**發佈**」按鈕來發佈您的內容。

   ![預覽和發佈選單項目](assets/do-not-localize/ue-preview-publish-4.png)

您的內容已發佈。

## 編輯內容片段 {#editing-fragments}

當 Headless 內容的結構化編輯比原處編輯更具優勢時，為了加速您的內容製作體驗，Universal Editor 還會讓您快速存取內容片段編輯器。

1. 點選 Universal Editor 工具列上的「**預覽**」按鈕關閉預覽模式。

   ![關閉預覽模式](assets/do-not-localize/ue-toggle-off-preview.png)

1. 在頁面上進一步向下捲動到「**冒險**」區段。

1. 選取其中一項冒險，例如「**峇里島衝浪營**」來完成選取。

   * 請注意已選取元件的藍色輪廓。選取內容片段時，標籤應顯示內容片段的名稱。在此例中為&#x200B;**峇里島衝浪營**。
   * 由於 Universal Editor 允許選取頁面上的任何物件，因此也可以個別選取組成內容片段的元件。選取插圖中標示的位置，即可選取整個內容片段元件。

1. 在元件邊欄上顯示「**編輯**」圖示。選取「**編輯**」圖示，在新標籤上開啟內容片段編輯器。

![在 Universal Editor 中選取內容片段](assets/do-not-localize/ue-content-fragments.png)

您現在可以在新的索引標籤上編輯在 Universal Editor 中選取的內容片段。
