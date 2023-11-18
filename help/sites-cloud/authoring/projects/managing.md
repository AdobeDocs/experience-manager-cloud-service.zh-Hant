---
title: 管理專案
description: 專案可讓您將資源分組到一個實體中，以便在「專案」主控台中存取和管理該實體，藉此組織您的專案
exl-id: be4616e7-18bc-4b2d-89f6-d04178ac7f3a
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 11%

---

# 管理專案 {#managing-projects}

專案可讓您將資源分組為一個實體，以組織您的專案。

在 **專案** 主控台，您可以存取專案並採取行動：

![專案主控台](/help/sites-cloud/authoring/assets/projects-console.png)

在「專案」中，您可以建立專案、將資源與專案建立關聯，也可以刪除專案或資源連結。 您可能想要開啟圖磚，以檢視其內容並將專案新增至圖磚。 本主題說明這些程式。

## 建立專案 {#creating-a-project}

AEM提供這些立即可用的範本，供您在建立專案時選擇：

* 簡單專案
* 媒體專案
* 翻譯專案

<!-- Hiding product photoshoot via cqdoc-18072 as it is not available in Skyline.
* Product Photo Shoot Project 
-->

從專案到專案，建立專案的程式都相同。專案類型之間的差異包括可用的使 [用者角色](/help/sites-cloud/authoring/projects/overview.md)[和工作流程](/help/sites-cloud/authoring/projects/workflows.md)。若要建立專案：

1. 在 **專案**，選取 **建立** 以開啟 **建立專案** 精靈：
1. 選取範本並按一下 **下一個**.

   ![建立專案](/help/sites-cloud/authoring/assets/projects-create.png)

1. 定義 **標題** 和 **說明** 並新增 **縮圖** 影像（如有需要）。 您也可以新增或刪除使用者，以及使用者所屬的群組。 此外，按一下 **進階** 以新增在URL中使用的名稱。

   ![新增專案詳細資料](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. 選擇 **建立**。確認會詢問您是要開啟新專案，還是返回主控台。

### 將資源與專案建立關聯 {#associating-resources-with-your-project}

由於專案可讓您將資源分組到一個實體中，因此您想要將資源與專案相關聯。 這些資源稱為 **圖磚**. 您可以新增的資源型別在中說明 [專案動態磚](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

若要將資源與專案產生關聯，請執行下列動作：

1. 從開啟您的專案 **專案** 主控台。
1. 選取 **新增圖磚** 並選取您要連結至專案的圖磚。 您可以選取多種型別的圖磚。

   ![將圖磚新增至專案](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >有關可與專案關聯的專案拼貼的詳細說明，請參閱 [專案動態磚](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

1. 選擇 **建立**。您的資源已連結至專案，從現在開始，您就可以從專案存取該資源。

### 刪除專案或資源連結 {#deleting-a-project-or-resource-link}

使用相同的方法從主控台刪除專案，或從專案刪除連結的資源：

1. 導覽至適當位置：

   * 若要刪除專案，請移至 **專案** 主控台。
   * 若要刪除專案中的資源連結，請在以下位置開啟您的專案： **專案** 主控台。

1. 按一下以進入選擇模式 **選取** 並選取您的專案或資源連結。
1. 選取&#x200B;**刪除**。

1. 您需要在對話方塊中確認刪除。 若已確認，則會刪除專案或資源連結。 選取 **取消選取** 以結束選取模式。

>[!NOTE]
>
>當您建立專案並將使用者新增至各種角色時，系統會自動建立與專案相關的群組，以管理相關的權限。例如，名為Myproject的專案會有三個群組 **Myproject Owners**、 **Myproject Editors**、 **Myproject Obsertors**。不過，如果刪除專案，這些群組不會自動刪除。管理員必須手動刪除中的群組 **工具** > **安全性** > **群組**.

### 將專案新增至圖磚 {#adding-items-to-a-tile}

在某些圖磚中，您可能想要新增多個專案。 例如，您可能會同時執行多個工作流程或多個體驗。

若要將專案新增至圖磚：

1. 在 **專案**，導覽至專案，並在您要新增專案的方塊上選取向下V形。

   ![將專案新增至圖磚](/help/sites-cloud/authoring/assets/project-workflows.png)

1. 新增專案至圖磚，就像建立圖磚時一樣。 專案拼貼已說明 [此處](/help/sites-cloud/authoring/projects/overview.md#project-tiles). 在此範例中，已新增另一個工作流程。

### 開啟拼貼 {#opening-a-tile}

您可能想要檢視目前圖磚中包含哪些專案，或修改或刪除圖磚中的專案。

若要開啟圖磚，以便檢視或修改專案：

1. 在「專案」主控台中，選取卡片底部的省略符號(...)圖示。

   ![開啟圖磚](/help/sites-cloud/authoring/assets/project-links.png)

1. AEM會列出該圖磚中的專案。 您可以進入選取模式來修改或刪除專案。

   ![圖磚已開啟](/help/sites-cloud/authoring/assets/projects-add-link.png)

## 檢視專案統計資料 {#viewing-project-statistics}

您可以在下列位置檢視專案統計資料： **專案** 主控台。

### 檢視專案時間表 {#viewing-a-project-timeline}

專案時間表提供有關專案中資產上次使用時間的資訊。 若要檢視專案時間表，請選取 **時間表**，然後進入選擇模式並選取專案。 資產會顯示在左窗格中。 選取 **時間表** 以返回 **專案** 主控台。

![專案時間表](/help/sites-cloud/authoring/assets/projects-timeline.png)

### 檢視作用中/非作用中的專案 {#viewing-active-inactive-projects}

若要在使用中或非使用中專案之間切換，請在 **專案** 主控台，按一下 **切換使用中的專案**. 如果該圖示旁邊有勾號，則顯示的是作用中的專案。

![切換作用中專案按鈕](/help/sites-cloud/authoring/assets/projects-active.png)

如果圖示旁邊有x，表示它顯示的是非使用中專案。

![切換非作用中專案按鈕](/help/sites-cloud/authoring/assets/projects-inactive.png)

## 讓專案非作用中或作用中 {#making-projects-inactive-or-active}

如果您已完成專案，但仍想保留專案上的資訊，您可能會想要讓專案停用。

若要使專案非作用中（或作用中），請執行下列動作：

1. 在 **專案** 主控台，開啟您的專案，然後找到 **專案資訊** 圖磚。

   >[!NOTE]
   >
   如果您的專案中尚未包含此圖磚，您可能需要新增此圖磚。 另請參閱 [新增圖磚](#adding-items-to-a-tile).

1. 選取&#x200B;**編輯**。
1. 變更選擇器從 **作用中** 至 **非使用中** （反之亦然）。

   ![啟用專案](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. 選取 **完成** 以儲存變更。
