---
title: 從網站主控台發佈頁面
description: 瞭解如何使用Sites Console發佈和取消發佈您的頁面。
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5ad91a32d705ef61e8b9799bf7fb1e136bb8bfa0
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 5%

---


# 從網站主控台發佈頁面 {#publishing-pages}

在作者環境中建立並檢閱您的內容後，目標就是[讓內容可在您的公用網站](/help/sites-cloud/authoring/author-publish.md) （您的發佈環境）上使用。

這稱為發佈頁面。 從發佈環境中移除頁面時，系統會將其稱為取消發佈。 發佈和取消發佈時，除非您將其刪除，否則頁面仍可在作者環境中用於進一步的變更。

您可以使用&#x200B;[**Sites**&#x200B;主控台](/help/sites-cloud/authoring/sites-console/introduction.md)，立即或在預先定義的未來日期/時間發佈/取消發佈頁面。

>[!TIP]
>
>您可以從Sites主控台以外的位置發佈。
>
>* [來自頁面編輯器](/help/sites-cloud/authoring/page-editor/publishing.md)
>* [來自通用編輯器](/help/sites-cloud/authoring/universal-editor/publishing.md)
>* 從體驗片段[&#128279;](/help/sites-cloud/authoring/fragments/experience-fragments.md)主控台或編輯器
>
>從這些位置發佈會提供不同的選項，但遵循此處說明的類似程式和一般構想。

## 術語 {#terminology}

在使用Adobe Experience Manager (AEM) as a Cloud Service時，您可能會遇到與發佈相關的不同詞語。

* **發佈/取消發佈**
   * 這些是讓您的內容在發佈和/或預覽環境（或不在）中公開可用的動作主要詞語。
   * 這些是AEM檔案中使用的術語。
* **啟用/停用**
   * 這些辭彙與發佈/取消發佈同義。
   * 這些詞語用於舊版AEM。
* **復寫/復寫**
   * 這些是技術術語，說明發佈頁面時（例如從作者到預覽）資料（例如頁面內容、檔案、程式碼、使用者評論）從一項服務移動到另一項服務。
   * 這些詞語主要由開發人員使用。

>[!NOTE]
>
>如果您沒有發佈特定頁面所需的許可權：
>
>* 系統會觸發工作流程，將您要發佈的請求通知給適當人員。
>* 您的開發團隊可能已自訂此工作流程。
>* 系統會顯示簡短的訊息，通知您工作流程已觸發。

>[!NOTE]
>
>如果要保留頁面順序，您必須使用[管理出版物](#manage-publication)，在單一動作中將父頁面與任何子頁面一起發佈。
>
>無法保證頁面順序：
>
>* 如果只選取子頁面以供發佈（因為訂單資訊會保留在父頁面上）
>* 如果父頁面和子頁面是以不同動作發佈

## 從網站主控台發佈頁面 {#publishing-from-the-sites-console}

在&#x200B;**Sites**&#x200B;主控台中，有兩個發佈選項：

* [快速發佈](#quick-publish)
* [管理發佈](#manage-publication)

### 快速發佈 {#quick-publish}

**快速發佈**&#x200B;適用於簡單的情況，並且會立即發佈選取的頁面，而不會進行任何進一步的互動。 因此，任何未發佈的參考也會自動發佈。

若要使用「快速發佈」功能發佈頁面：

1. 在網站主控台中選取一個或多個頁面，然後按一下&#x200B;**快速發佈**&#x200B;按鈕。

   ![選取要發行的頁面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 在[快速發佈]對話方塊中，按一下[發佈]&#x200B;**&#x200B;**&#x200B;以確認發佈，或按一下[取消]&#x200B;**&#x200B;**&#x200B;以取消發佈。 請記住，任何未發佈的參考也會自動發佈。

   ![快速發佈確認](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. 發佈頁面時，畫面會顯示確認發佈的警報。

>[!NOTE]
>
>快速發佈是淺層發佈，也就是說，只會發佈選取的頁面，而不會發佈任何子頁面。

### 管理發佈 {#manage-publication}

**管理出版物**&#x200B;提供比&#x200B;**快速發佈**&#x200B;更多的選項，允許包含子頁面、自訂參考、發佈到預覽服務（如果有的話），以及啟動任何適用的工作流程，並提供在以後發佈的選項。

若要使用「管理發布」來發佈或取消發佈頁面：

1. 在網站主控台中選取一個或多個頁面，然後按一下&#x200B;**管理出版物**&#x200B;按鈕。

   ![選取要發行的頁面](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. 「管 **理出版物** 」嚮導將啟動。第一個步驟&#x200B;**選項**&#x200B;可讓您：

   * **動作**

     選擇發佈或取消發佈選取的頁面。

   * **目的地**

     選擇您要發佈至發佈服務（預設）或預覽服務。 僅當您已設定[預覽服務時可用。](/help/sites-cloud/authoring/sites-console/previewing-content.md)

   * **排程**

     選擇現在或稍後採取該動作。

     稍後發佈會啟動工作流程，以在指定時間發佈選取的一或多個頁面。 相反地，稍後取消發佈會啟動工作流程，以在特定時間取消發佈選取的一個或多個頁面。

     >[!TIP]
     >
     >如果您要稍後再取消發佈/取消發佈，請移至[工作流程主控台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)以終止對應的工作流程。

     >[!TIP]
     >
     >排程發佈內容會複製內容並遵守發佈工作流程。 如果您想要暫時隱藏已發佈的內容而不取消發佈，請考慮在頁面屬性中使用&#x200B;[**開啟時間**&#x200B;和&#x200B;**關閉時間**。](/help/sites-cloud/authoring/sites-console/page-properties.md#basic)

   ![管理出版物選項](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. 按一下[下一步]&#x200B;**&#x200B;**&#x200B;繼續。

1. 在管理發布精靈的下一個步驟&#x200B;**範圍**&#x200B;中，您可以定義發佈/取消發佈的範圍，例如包含子頁面和/或包含參考。

   ![管理發布範圍](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **新增內容**

   您可以使用「新 **增內容** 」按鈕，在要發佈的頁面清單中新增其他頁面，以防您在啟動「管理出版物」精靈之前未選取其中一個頁面。

   選取&#x200B;**新增內容**&#x200B;按鈕會啟動[路徑瀏覽器](/help/sites-cloud/authoring/path-selection.md)以允許選擇內容。

   選取必要的頁面，然後按一下[選取]將內容加入精靈，或按一下[選取]將內容加入精靈，或按一下[取消]取消選取並返回精靈。**&#x200B;**&#x200B;**&#x200B;**

   **移除選取專案**

   回到精靈中，您可以在清單中選取一個專案，將其從選取範圍中移除。

   ![管理出版物選取頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **已發佈的參考**

   您可以檢視並修改某個頁面要發佈或取消發佈的引用，方法是選取該頁面，然後按一下&#x200B;**已發佈引用**&#x200B;按鈕。

   ![管理出版物選項](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   **已發佈的參考**&#x200B;對話方塊會顯示所選內容的參考。 依預設，這些量度會全部選取並發佈/取消發佈，但您可以取消勾選以取消選取，這樣它們就不會包含在動作中。

   按一下&#x200B;**完成**&#x200B;以儲存您的變更，或按一下&#x200B;**取消**&#x200B;以取消選取並返回精靈。

   回到精靈，**參考**&#x200B;欄會更新，以反映您選取的要發佈或取消發佈的參考。

   ![管理出版物選取頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **包含子項**

   >[!NOTE]
   >
   >請參閱[發佈與取消發佈樹狀結構](#publishing-and-unpublishing-a-tree)

   按一下&#x200B;**包含子項**&#x200B;會開啟對話方塊，讓您：

   * **包含子項**
   * **僅包含直接子項**
   * **僅包含已修改的頁面**
   * **僅包含已發佈的頁面**

   啟用必要選項，並按&#x200B;**確定**&#x200B;確認，根據選取選項，將子頁面新增至要發佈或取消發佈的頁面清單。 按一下&#x200B;**取消**&#x200B;以取消選取並返回精靈。

   ![管理包含子項的出版物](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. 按一下&#x200B;**發佈**&#x200B;以完成。

   回到網站主控台，系統會傳送通知訊息確認發佈。

1. 如果發佈的頁面與工作流程相關聯，它們可能會顯示在發佈精靈的最後一個&#x200B;**工作流程**&#x200B;步驟中。

   ![管理出版物選取頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >根據使用者可能擁有也可能沒有的許可權，顯示&#x200B;**工作流程**&#x200B;步驟。 如需詳細資訊，請參閱本頁先前關於發佈許可權和管理工作流程存取權以及[將工作流程套用至頁面](/help/sites-cloud/authoring/workflows/applying.md)的備註。

   資源會依觸發的工作流程分組，每個指定選項用於：

   * 定義工作流程的標題。
   * 保留工作流程封裝，前提是工作流程具有多資源支援。
   * 如果已選擇保留工作流程封裝的選項，則定義工作流程封裝的標題。

1. 按一 **下「發佈** 」或「 **稍後發佈** 」以完成出版。

## 取消發佈頁面 {#unpublishing-pages}

取消發佈頁面會將其從您的發佈或[預覽](/help/sites-cloud/authoring/sites-console/previewing-content.md)環境中移除，因此不再將其提供給您的讀者。

如同您[使用[管理出版物]選項發佈](#manage-publication)一樣，您也可以使用它來取消發佈。

1. 在網站主控台中選取一個或多個頁面，然後按一下&#x200B;**管理出版物**&#x200B;按鈕。
1. 「管 **理出版物** 」嚮導將啟動。在第一個步驟中， **選項**，選擇「取消發佈」(Unpublish **)，而非「發佈」(Publish)的預設** 選項 **&#x200B;**。

   ![取消發佈 — 選項](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   正如稍後發佈會啟動工作流程，以在指定時間發佈此版本的頁面一樣，稍後停用也會啟動工作流程，以在指定時間取消發佈選取的一或多個頁面。

   >[!NOTE]
   >
   >如果您要稍後再取消發佈/取消發佈，請移至[工作流程主控台](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance)以終止對應的工作流程。

   >[!NOTE]
   >如果您有[預覽](/help/sites-cloud/authoring/sites-console/previewing-content.md)環境，您可以在管理發布期間選取&#x200B;**目的地**。

1. 若要完成取消發佈，請繼續完成精靈，就像您要[發佈頁面](#manage-publication)一樣。

   ![取消發佈 — 範圍](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## 發佈和取消發佈樹狀結構 {#publishing-and-unpublishing-a-tree}

當您輸入或更新了相當數量的內容頁面時 — 所有這些頁面都位於同一個根頁面下 — 在一個動作中發佈整個樹狀結構會比較容易。

您可以使用網站主控台上的[管理出版物](#manage-publication)選項來執行此動作。

1. 在網站主控台中，選取您要發佈或取消發佈的樹狀目錄根頁面，然後選取&#x200B;**管理出版物**。
1. 「管 **理出版物** 」嚮導將啟動。選擇發佈或取消發佈，以及應該發生的時間，並選取&#x200B;**下一步**&#x200B;以繼續。
1. 在&#x200B;**領域**&#x200B;步驟中，選取根頁面並選取&#x200B;**包含子項**。

   ![管理出版物選取頁面](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. 在&#x200B;**包含子項**&#x200B;對話方塊中：

   * 選取&#x200B;**包含子項**
   * 取消選取&#x200B;**僅包含直接子項**
   * 取消選取&#x200B;**僅包含已發佈的頁面**
   * 視需要設定&#x200B;**僅包含修改過的頁面**

   這些選項預設為選取，因此您必須記得加以設定。 使用&#x200B;**確定**&#x200B;確認選取範圍，以將內容新增至發佈/取消發佈。

   ![包含樹狀結構發佈的子項](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. 在&#x200B;**管理出版物**&#x200B;精靈中，您可以新增其他頁面或移除選取的頁面，以進一步自訂選取專案。

   請記住，您也可以透過&#x200B;**已發佈的參考**&#x200B;選項檢閱要發佈的參考。

1. [繼續正常的[管理發布]精靈](#manage-publication)，以完成樹狀結構的發佈或取消發佈。

## 決定發佈狀態 {#determining-publication-status}

您可以決定頁面的發佈狀態：

* 在網站主控台[&#128279;](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)的資源概觀資訊中

  ![卡片檢視中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  發佈狀態會顯示在 [網站主控台](/help/sites-cloud/authoring/basic-handling.md#card-view) [的卡片](/help/sites-cloud/authoring/basic-handling.md#column-view)、欄和 [清單檢視中](/help/sites-cloud/authoring/basic-handling.md#list-view) 。

* 在[時間表](/help/sites-cloud/authoring/basic-handling.md#timeline)中

  時間軸檢視中的![發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* 在[頁面資訊功能表](/help/sites-cloud/authoring/page-editor/introduction.md#page-information)中，編輯頁面時

  ![頁面資訊功能表中的發佈狀態](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
