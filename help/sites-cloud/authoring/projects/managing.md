---
title: 管理專案
description: 專案可讓您將資源分組為一個實體，以便在「專案」主控台中存取和管理，以組織您的專案
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 12%

---


# 管理專案 {#managing-projects}

專案可讓您將資源分組為一個實體，以組織專案。

在&#x200B;**Projects**&#x200B;控制台中，您可以訪問並對項目執行操作：

![專案主控台](/help/sites-cloud/authoring/assets/projects-console-detail.png)

在「項目」中，您可以建立項目、將資源與項目關聯，以及刪除項目或資源連結。 您可能想要開啟圖格來檢視其內容，並新增項目至圖格。 本主題介紹這些過程。

## 建立項目{#creating-a-project}

AEM現成可用，提供下列範本供您在建立專案時選擇：

* 簡單專案
* 媒體專案
* 產品像片拍攝專案
* 翻譯專案

從專案到專案，建立專案的程式都相同。專案類型之間的差異包括可用的使 [用者角色](/help/sites-cloud/authoring/projects/overview.md)[和工作流程](/help/sites-cloud/authoring/projects/workflows.md)。要建立新項目，請執行以下操作：

1. 在「 **專案**」中，點選/按一 **下「建立** 」以開啟「 **** 建立專案」精靈：
1. 選擇模板並按一下&#x200B;**Next**。

   ![建立專案](/help/sites-cloud/authoring/assets/projects-create.png)

1. 定義&#x200B;**Title**&#x200B;和&#x200B;**Description**，並視需要新增&#x200B;**Thumbnail**&#x200B;影像。 您也可以新增或刪除使用者及其所屬的群組。 此外，按一下&#x200B;**Advanced**，新增URL中使用的名稱。

   ![新增專案詳細資料](/help/sites-cloud/authoring/assets/projects-title.png)

1. 點選／按一下&#x200B;**Create**。 確認會詢問您是要開啟新專案，還是要返回主控台。

### 將資源與項目{#associating-resources-with-your-project}關聯

由於項目使您能夠將資源分組到一個實體，因此您希望將資源與項目關聯。 這些資源稱為&#x200B;**Tiles**。 可添加的資源類型在[Project Tiles](/help/sites-cloud/authoring/projects/overview.md#project-tiles)中有說明。

要將資源與您的項目關聯，請執行以下操作：

1. 從&#x200B;**Projects**&#x200B;控制台開啟項目。
1. 點選／按一下「新增圖格」(**Add Tile)**，並選取您要連結至專案的圖格。 您可以選取多種圖格類型。

   ![新增圖格至專案](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >[項目表徵圖中詳細描述了可與項目關聯的項目表徵圖。](/help/sites-cloud/authoring/projects/overview.md#project-tiles)

1. 點選／按一下&#x200B;**Create**。 您的資源會連結至您的專案，從現在起，您就可以從專案存取它。

### 刪除項目或資源連結{#deleting-a-project-or-resource-link}

從控制台刪除項目或從項目中刪除連結資源的方法相同：

1. 導覽至適當的位置：

   * 要刪除項目，請轉至&#x200B;**Projects**&#x200B;控制台的頂級。
   * 要刪除項目中的資源連結，請在&#x200B;**項目**&#x200B;控制台中開啟項目。

1. 按一下&#x200B;**選擇**&#x200B;並選擇項目或資源連結，進入選擇模式。
1. 點選／按一下&#x200B;**Delete**。

1. 您必須在對話方塊中確認刪除。 如果確認，項目或資源連結將被刪除。 點選／按一下「**取消選取**」以退出選擇模式。

>[!NOTE]
>
>當您建立專案並將使用者新增至各種角色時，系統會自動建立與專案相關的群組，以管理相關的權限。例如，名為Myproject的專案會有三個群組 **Myproject Owners**、 **Myproject Editors**、 **Myproject Obsertors**。不過，如果刪除專案，這些群組不會自動刪除。管理員需要手動刪除「工具 **>安全** 性 **>** 群組 ****」。

### 新增項目至圖格{#adding-items-to-a-tile}

在某些圖格中，您可能想要新增多個項目。 例如，您可能同時執行多個工作流程或多個體驗。

若要新增項目至圖格：

1. 在&#x200B;**Projects**&#x200B;中，導覽至專案，然後按一下您要新增項目的方塊上的「新增+」圖示。

   ![新增項目至圖格](/help/sites-cloud/authoring/assets/projects-workflows-1.png)

1. 新增項目至圖格，就像建立新圖格時一樣。 項目表徵圖在[這裡](/help/sites-cloud/authoring/projects/overview.md#project-tiles)有說明。 在此範例中，新增了另一個工作流程。

   ![新增至圖格的另一個項目](/help/sites-cloud/authoring/assets/projects-workflows-2.png)

### 開啟表徵圖{#opening-a-tile}

您可能想要查看目前圖格中包含哪些項目，或修改或刪除圖格中的項目。

若要開啟圖格，以便檢視或修改項目：

1. 在「專案」主控台中，點選／按一下省略號(...)

   ![開啟磚](/help/sites-cloud/authoring/assets/projects-open-tile.png)

1. AEM會列出該方塊中的項目。 您可以進入選擇模式來修改或刪除項目。

   ![已開啟的圖格](/help/sites-cloud/authoring/assets/projects-opened-tile.png)

## 查看項目統計資訊{#viewing-project-statistics}

要查看項目統計資訊，請在&#x200B;**項目**&#x200B;控制台中按一下&#x200B;**顯示統計資訊視圖**。 會顯示每個專案的完成層級。 再次按一下「顯示統計視圖」以轉至「項目」控制台。********

![專案統計資料](/help/sites-cloud/authoring/assets/projects-stats.png)

### 查看項目時間軸{#viewing-a-project-timeline}

專案時間軸提供上次使用專案中資產的資訊。 若要檢視專案時間軸，請按一下／點選&#x200B;**時間軸**，然後進入選擇模式並選取專案。 資產會顯示在左窗格中。 按一下／點選&#x200B;**時間軸**&#x200B;以返回至&#x200B;**Projects**&#x200B;主控台。

![專案時間軸](/help/sites-cloud/authoring/assets/projects-timeline.png)

### 查看活動／非活動項目{#viewing-active-inactive-projects}

要在活動項目和非活動項目之間切換，請在&#x200B;**Projects**&#x200B;控制台中按一下&#x200B;**Toggle Active Projects**。 如果圖示旁有複選標籤，則會顯示作用中的專案。

![切換作用中專案按鈕](/help/sites-cloud/authoring/assets/projects-active.png)

如果圖示旁有x，則會顯示非作用中專案。

![切換非作用中專案按鈕](/help/sites-cloud/authoring/assets/projects-inactive.png)

## 將項目設定為非活動或活動{#making-projects-inactive-or-active}

如果您已完成項目，但仍想保留項目的資訊，則可能希望將其設定為非活動項目。

要將項目設定為非活動（或活動），請執行以下操作：

1. 在&#x200B;**Projects**&#x200B;控制台中，開啟您的項目，然後查找&#x200B;**Project information**&#x200B;表徵圖。

   >[!NOTE]
   如果您的專案中尚未加入此圖格，您可能需要加入它。 請參閱[添加拼貼](#adding-items-to-a-tile)。

1. 點選／按一下&#x200B;**編輯**。
1. 將選擇器從&#x200B;**Active**&#x200B;更改為&#x200B;**Inactive**（反之亦然）。

   ![啟動專案](/help/sites-cloud/authoring/assets/projects-activate.png)

1. 點選／按一下&#x200B;**Done**&#x200B;以儲存變更。
