---
title: 管理專案
description: 項目允許您通過將資源分組到一個實體中來組織項目，該實體可在「項目」控制台中訪問和管理
exl-id: be4616e7-18bc-4b2d-89f6-d04178ac7f3a
source-git-commit: 54a098d8986c8bbd740bed50f8625c1025d2f6f4
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 12%

---

# 管理專案 {#managing-projects}

項目允許您通過將資源分組到一個實體來組織項目。

在 **項目** 控制台：訪問並對項目執行操作：

![項目控制台](/help/sites-cloud/authoring/assets/projects-console.png)

在「項目」中，您可以建立項目、將資源與項目關聯，還可以刪除項目或資源連結。 您可能希望開啟磁貼以查看其內容，並將項目添加到磁貼。 本主題介紹了這些過程。

## 建立項目 {#creating-a-project}

開箱即用，提AEM供了以下模板以在建立項目時進行選擇：

* 簡單專案
* 媒體專案
* 翻譯專案

<!-- Hiding product photoshoot via cqdoc-18072 as it is not available in Skyline.
* Product Photo Shoot Project 
-->

從專案到專案，建立專案的程式都相同。專案類型之間的差異包括可用的使 [用者角色](/help/sites-cloud/authoring/projects/overview.md)[和工作流程](/help/sites-cloud/authoring/projects/workflows.md)。要建立新項目，請執行以下操作：

1. 在「 **專案**」中，點選/按一 **下「建立** 」以開啟「 **** 建立專案」精靈：
1. 選擇模板並按一下 **下一個**。

   ![建立項目](/help/sites-cloud/authoring/assets/projects-create.png)

1. 定義 **標題** 和 **說明** 並添加 **縮略圖** 影像。 您還可以添加或刪除用戶及其所屬的組。 此外，按一下 **高級** 的子菜單。

   ![添加項目詳細資訊](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. 點擊/按一下 **建立**。 確認會詢問您是要開啟新項目還是要返回控制台。

### 將資源與項目關聯 {#associating-resources-with-your-project}

由於項目使您能夠將資源分組到一個實體中，因此您希望將資源與項目關聯。 這些資源稱為 **磁貼**。 可添加的資源類型在中介紹 [項目磁貼](/help/sites-cloud/authoring/projects/overview.md#project-tiles)。

要將資源與項目關聯，請執行以下操作：

1. 從 **項目** 控制台。
1. 點擊/按一下 **添加磁貼** 並選擇要連結到項目的磁貼。 可以選擇多種類型的磁貼。

   ![向項目添加磁貼](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >可與項目關聯的項目磁貼在中詳細描述 [項目磁貼。](/help/sites-cloud/authoring/projects/overview.md#project-tiles)

1. 點擊/按一下 **建立**。 您的資源已連結到您的項目，從現在開始，您可以從您的項目訪問它。

### 刪除項目或資源連結 {#deleting-a-project-or-resource-link}

同一方法用於從控制台中刪除項目或從項目中刪除連結的資源：

1. 定位至相應位置：

   * 要刪除項目，請轉至 **項目** 控制台。
   * 要刪除項目中的資源連結，請在 **項目** 控制台。

1. 通過按一下進入選擇模式 **選擇** 選擇項目或資源連結。
1. 點擊/按一下 **刪除**。

1. 您需要在對話框中確認刪除。 如果確認，則刪除項目或資源連結。 點擊/按一下 **取消選擇** 的子菜單。

>[!NOTE]
>
>當您建立專案並將使用者新增至各種角色時，系統會自動建立與專案相關的群組，以管理相關的權限。例如，名為Myproject的專案會有三個群組 **Myproject Owners**、 **Myproject Editors**、 **Myproject Obsertors**。不過，如果刪除專案，這些群組不會自動刪除。管理員需要手動刪除「工具 **>安全** 性 **>** 群組 ****」。

### 將項目添加到磁貼 {#adding-items-to-a-tile}

在某些磁貼中，您可能想添加多個項。 例如，您可能同時運行多個工作流或多次運行一次。

要將項目添加到磁貼：

1. 在 **項目**，導航到項目，然後點擊或按一下要添加項目的磁貼上的向下雪形。

   ![將項添加到磁貼](/help/sites-cloud/authoring/assets/project-workflows.png)

1. 向磁貼添加項目，如同建立新磁貼時一樣。 描述了項目磁貼 [這裡](/help/sites-cloud/authoring/projects/overview.md#project-tiles)。 在此示例中，添加了另一個工作流。

### 開啟磁貼 {#opening-a-tile}

您可能希望查看當前磁貼中包含哪些項目，或修改或刪除磁貼中的項目。

要開啟磁貼，以便查看或修改項目：

1. 在「項目」控制台中，按一下/按一下卡底部的省略號(...)表徵圖。

   ![開啟磁貼](/help/sites-cloud/authoring/assets/project-links.png)

1. 列AEM出該磁貼中的項。 您可以進入選擇模式以修改或刪除項目。

   ![已開啟磁貼](/help/sites-cloud/authoring/assets/projects-add-link.png)

## 查看項目統計資訊 {#viewing-project-statistics}

您可以在 **項目** 控制台。

### 查看項目時間線 {#viewing-a-project-timeline}

項目時間表提供有關上次使用項目中資產的時間的資訊。 要查看項目時間線，請按一下/點擊 **時間軸**，然後進入選擇模式並選擇項目。 資產顯示在左窗格中。 按一下/點擊 **時間軸** 返回 **項目** 控制台。

![項目時間表](/help/sites-cloud/authoring/assets/projects-timeline.png)

### 查看活動/非活動項目 {#viewing-active-inactive-projects}

要在活動項目和非活動項目之間切換， **項目** 控制台，按一下 **切換活動項目**。 如果表徵圖旁邊有複選標籤，則它將顯示活動項目。

![切換活動項目按鈕](/help/sites-cloud/authoring/assets/projects-active.png)

如果表徵圖旁邊有x，則它將顯示非活動項目。

![切換非活動項目按鈕](/help/sites-cloud/authoring/assets/projects-inactive.png)

## 使項目處於非活動狀態或活動狀態 {#making-projects-inactive-or-active}

如果已完成項目，您可能希望使其處於非活動狀態，但仍希望保留有關該項目的資訊。

要使項目處於非活動狀態（或活動狀態），請執行以下操作：

1. 在 **項目** 控制台，開啟項目，然後查找 **項目資訊** 平鋪。

   >[!NOTE]
   如果此磁貼尚未在項目中，則可能需要添加它。 請參閱 [添加磁貼](#adding-items-to-a-tile)。

1. 點擊/按一下 **編輯**。
1. 更改選擇器 **活動** 至 **非活動** （反之亦然）。

   ![激活項目](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. 點擊/按一下 **完成** 的子菜單。
