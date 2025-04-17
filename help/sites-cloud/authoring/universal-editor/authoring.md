---
title: 使用 Universal Editor 編寫內容
description: 了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: da14ed18b786c1f19d76926ed027d13a53275af3
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 30%

---


# 使用 Universal Editor 編寫內容 {#authoring}

了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。

## 簡介 {#introduction}

通用編輯器可讓您編輯任何實作中任何內容的任何方面，因此您可以提供卓越的體驗並提高內容速度。

為此，Universal Editor 為內容作者提供直觀的 UI，只需要最基本的培訓就能立即進入狀況並開始編輯內容。本文件說明了 Universal Editor 的編寫體驗。

>[!NOTE]
>
>本檔案假設您已熟悉如何存取和導覽通用編輯器。 如果沒有，請參閱[存取及導覽通用編輯器](/help/sites-cloud/authoring/universal-editor/navigation.md)。

>[!TIP]
>
>如需Universal Editor的詳細介紹，請參閱[Universal Editor簡介](/help/implementing/universal-editor/introduction.md)。

## 編輯內容 {#editing-content}

編輯內容很簡單又直覺。當您將滑鼠移至編輯器中的內容上時，可編輯的內容會以淡藍色外框反白顯示。

![可編輯的內容會以藍色框醒目顯示](assets/editable-content.png)

>[!TIP]
>
>依預設，點選或按一下內容會選取內容以進行編輯。 如果您想透過下列連結導覽內容，請切換至[預覽模式](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)。

根據您選取的內容，您可能有不同的就地編輯選項，而且您可能會在[屬性面板](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)中針對內容提供額外的資訊和選項。

### 編輯純文字 {#edit-plain-text}

您可以按兩下或點兩下元件，就地編輯文字。

![編輯內容](assets/editing-content.png)

薄的藍色輪廓會變成粗的藍色輪廓來指示選取，並且會出現游標。 進行變更，然後按下Enter/Return或在文字方塊外選取，以儲存變更。

當您選取選取文字元件時，其詳細資料會顯示在[屬性面板](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)中。 您也可以在面板中編輯文字。

![正在編輯屬性面板中的文字](assets/ue-editing-text-component-rail.png)

此外，「屬性」面板中也提供您文字的詳細資料。 一旦焦點離開屬性面板中已編輯的欄位，變更會自動儲存。

### 編輯 RTF 文字 {#edit-rich-text}

您可以按兩下或點兩下元件，就地編輯文字。

![編輯 RTF 文字元件](assets/rich-text-editing.png)

為方便起見，您可在兩個位置找到文字的格式選項和詳細資訊。

#### 內容功能表 {#context-menu}

快顯選單會在RTF區塊上方開啟，並在快顯選單中提供基本的格式選項。 由於空間限制，某些選項可能會隱藏在省略符號按鈕後面。

![ RTF內容功能表](assets/rich-text-context-menu.png)

一旦焦點離開已編輯的欄位，變更會自動儲存。

#### 屬性面板 {#properties-rail}

[屬性面板](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)會顯示所選文字的專案。 點選專案以開啟對話方塊，顯示較大的畫布以編輯文字。

![RTF編輯對話方塊](assets/rich-text-canvas.png)

點選或按一下「**取消**」或「**完成**」，分別捨棄或儲存變更。

### 編輯媒體 {#edit-media}

您可以在[屬性面板](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)中檢視其詳細資料。

![編輯媒體](assets/ue-edit-media.png)

1. 在屬性面板中，點選或按一下所選影像的預覽。
1. [資產選擇器](/help/assets/overview-asset-selector.md#using-asset-selector)視窗會開啟，讓您可選取資產。
1. 選取「 」以選取新資產。
1. 選取&#x200B;**選取**&#x200B;以返回取代資產的屬性面板。

變更會自動儲存到您的內容中。

### 編輯內容片段 {#edit-content-fragment}

如果您選取[內容片段](/help/sites-cloud/administering/content-fragments/overview.md)，您可以在[屬性面板](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)中編輯其詳細資料。

![編輯內容片段](assets/ue-edit-cf.png)

在所選內容片段的內容模型中定義的欄位會在屬性面板中顯示和編輯。

如果您選取與內容片段相關的欄位，內容片段會載入元件面板中，且欄位會自動捲動到。

一旦焦點離開屬性面板中已編輯的欄位，變更會自動儲存。

如果您想改用[內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md)編輯您的內容片段，請點選或按一下屬性面板中的&#x200B;[**在CF編輯器中開啟**&#x200B;按鈕](/help/sites-cloud/authoring/universal-editor/navigation.md#edit)。

>[!TIP]
>
>使用快速鍵`e`在內容片段編輯器中編輯選取的內容片段。

根據工作流程的需求，您可能會想要在通用編輯器中或直接在內容片段編輯器中編輯內容片段。

>[!NOTE]
>
>通用編輯器[根據其模型](/help/assets/content-fragments/content-fragments-models.md#validation)驗證內容片段欄位，可讓您強制執行資料完整性規則，例如規則運算式模式和唯一性限制。
>
>這可在發佈之前確保您的內容符合特定業務要求。

### 新增元件到容器中 {#adding-components}

1. 在[內容樹狀結構](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)或編輯器中選取容器元件。

   ![選取要新增到容器的元件](assets/ue-add-component.png)

1. 然後，在「屬性」面板中選取「新增」圖示。

   ![選取新增圖示](assets/add-icon.png)

該元件會被插入到容器中並可在編輯器中對其進行編輯。

>[!TIP]
>
>使用快速鍵 `a` 將元件新增到選取的容器中。

### 在容器中複製元件 {#duplicating-components}

1. 使用[內容樹狀結構](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)或編輯器選取容器中的元件。
1. 然後在屬性面板中選取&#x200B;**複製**&#x200B;圖示。

   ![選取要新增到容器的元件](assets/ue-duplicate-component.png)
1. 元件會複製並插入選取元件的下方。

該元件會被插入到容器中並可在編輯器中對其進行編輯。

### 從容器中刪除元件 {#deleting-components}

1. 在[內容樹狀結構](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)或編輯器中選取容器元件。
1. 選取容器的>形箭號圖示，展開內容樹狀結構中的內容。
1. 然後，在內容樹中，選取容器內的元件。
1. 在「屬性」面板中選取「刪除」圖示。

   ![刪除元件](assets/ue-delete-component.png)

選取的元件已刪除。

>[!TIP]
>
>使用快速鍵 `Shift+Backspace` 從容器中刪除選取的元件。

### 重新排序元件 {#reordering-components}

1. 如果尚未處於[內容樹狀結構模式](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)，請切換至該模式。
1. 在內容樹或編輯器中選取容器元件。
1. 選取容器的>形箭號圖示，展開內容樹狀結構中的內容。
1. 拖曳容器內的元件旁的手柄圖示證明您可以將它們重新排序。拖曳元件，在容器內將它們重新排序。

   ![重新排序元件](assets/ue-reordering-components.png)

1. 拖曳的元件在內容樹狀結構中會變成灰色，而您的插入點會以藍線表示。 將元件鬆開並放在新位置中。

元件會在內容樹和編輯器中重新排序。

>[!NOTE]
>
>如果目標容器[元件篩選器](/help/implementing/universal-editor/filtering.md)允許選取的元件，則元件只能在容器之間移動。

### 使用GenAI建立變化並產生變化 {#generate-variations-ai}

使用Generative Variations來利用Generative AI加速內容建立。

開啟「通用編輯器」以尋找「產生變化」的進入點。

如需瞭解詳細資訊，請參閱[產生變數 — 整合至AEM編輯器](/help/generative-ai/generate-variations-integrated-editor.md)。

## 預覽內容 {#previewing-content}

內容編輯完成後，您通常會希望瀏覽其內容，以查看它在其他頁面內容中的樣子。在[預覽模式](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)中，您可以點選連結，像讀者一樣瀏覽您的內容。內容在編輯器中呈現的樣子就是將會發佈的樣子。

在預覽模式中，點選或按一下內容的反應就像對內容的讀者一樣。 若要選取要編輯的內容，請切換出[預覽模式](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)。

## 其他資源 {#additional-resources}

若要瞭解如何使用通用編輯器發佈內容，請參閱本檔案。

* [使用通用編輯器發佈內容](publishing.md) — 瞭解通用編輯器如何發佈內容，以及您的應用程式如何處理已發佈的內容。

若要深入瞭解通用編輯器的技術細節，請參閱這些開發人員檔案。

* [通用編輯器簡介](/help/implementing/universal-editor/introduction.md) — 瞭解通用編輯器如何在任何實作中啟用編輯任何內容的任何方面，以便您提供卓越的體驗並提高內容速度。
* [AEM 中 Universal Editor 快速入門](/help/implementing/universal-editor/getting-started.md) - 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
* [Universal Editor 架構](/help/implementing/universal-editor/architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [屬性和類型](/help/implementing/universal-editor/attributes-types.md) - 了解 Universal Editor 需要的資料屬性和類型。
* [Universal Editor 驗證](/help/implementing/universal-editor/authentication.md) - 了解 Universal Editor 如何進行驗證。

## 編輯元件繼承 {#inheritance}

繼承是可連結內容的機制，如此一來變更一個會自動變更另一個。

使用通用編輯器，您只需更新內容即可取消內容的繼承。 編輯器會自動停用該頁面上作者所做所有變更的繼承，以確保在從Blueprint同步更新時保留修改的內容。

如需有關使用通用編輯器繼承如何運作的詳細資訊，請參閱[通用編輯器中的內容繼承](/help/sites-cloud/authoring/universal-editor/inheritance.md)。
