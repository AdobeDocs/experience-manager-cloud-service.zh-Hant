---
title: 內容片段主控台
description: 瞭解如何從內容片段控制台管理內容片段。
landing-page-description: 瞭解如何從內容片段控制台管理內容片段，該控制台側重於無頭使用情形中大量使用內容片段，但在頁面創作時也使用。
feature: Content Fragments
role: User
exl-id: 0e6e3b61-a0ca-44b8-914d-336e29761579
source-git-commit: cdc86e5661ec90f96f670e777a9c98b3dcd4a7ac
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 6%

---

# 內容片段主控台  {#content-fragments-console}

瞭解內容片段控制台如何優化對內容片段的訪問，幫助您通過執行諸如發佈、取消發佈、複製等管理操作來建立、搜索和管理內容片段。

內容片段控制台專用於管理、搜索和建立內容片段。 它已優化為在無頭上下文中使用，但在建立內容片段以用於頁面創作時也使用。

>[!NOTE]
>
>此控制台僅顯示內容片段。 它不顯示影像和視頻等其他資產類型。

>[!NOTE]
>
>當前可通過以下方式訪問您的內容片段：
>
>* 這個 **內容片段** 控制台
>* 這樣 **資產** 控制台 — 請參見 [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)


>[!NOTE]
>
>選擇 [鍵盤快捷鍵可在此控制台中使用](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md)。

>[!NOTE]
>
>如果需要，您的項目團隊可以自定義控制台。 請參閱 [自定義內容片段控制台](/help/implementing/developing/extending/content-fragment-console-customizing.md) 的上界。

可以從全局導航的頂級直接訪問「內容片段」控制台：

![全局導航 — 內容片段控制台](assets/cfc-global-navigation.png)

## 控制台的基本結構及處理 {#basic-structure-handling-content-fragments-console}

選擇 **內容片段** 將在新頁籤中開啟控制台。

![內容片段控制台 — 概述](assets/cfc-console-overview.png)

這裡你可以看到有三個主要領域：

* 頂部工具欄
   * 提供標準功AEM能
   * 還顯示您的IMS組織
* 左面板
   * 在此可隱藏或顯示資料夾樹
   * 可以選擇樹的特定分支
   * 可以調整此大小以顯示嵌套資料夾
* 主/右面板 — 您可以從此處：
   * 請參閱樹的選定分支中所有內容片段的清單：
      * 該位置由麵包屑表示；這些也可用於更改位置
      * 將顯示所選資料夾中的內容片段，並顯示所有子資料夾：
         * [各種資訊領域](#selectuse-available-columns) 關於內容片段提供連結；根據欄位的不同，這些可以：
            * 在編輯器中開啟相應的片段
            * 顯示有關引用的資訊
            * 顯示有關片段語言版本的資訊
      * 通過在列標題上使用滑鼠移動，將顯示下拉操作選擇器和寬度滑塊。 這些允許您：
         * 排序 — 為升序或降序選擇適當的操作。這將根據該列對整個表進行排序。 排序僅對相應的列可用。
         * 調整列大小 — 使用操作或寬度滑塊

## 動作 {#actions}

在控制台中，可以直接使用或選擇特定片段後使用的操作範圍：

* 各種操作都直接 [可從控制台獲得](#available-actions)
* 你可以 [選擇一個或多個內容片段以顯示相應操作](#actions-selected-content-fragment)

### 操作（未選定） {#actions-unselected}

某些操作可從控制台獲得 — 不選擇特定內容片段：

* **[建立](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)** 新內容片段
* [篩選](#filtering-fragments) 根據謂詞的選擇保存內容片段，並保存篩選器以供將來使用
* [搜索](#searching-fragments) 內容片段
* [自定義表視圖以顯示選定的資訊列](#select-available-columns)
* 使用 **在資產中開啟** 直接開啟 **資產** 控制台

   >[!NOTE]
   >
   >的 **資產** 控制台用於訪問資產，如影像、視頻等。  可以訪問此控制台：
   >
   >* 使用 **在資產中開啟** 連結（在「內容片段」控制台中）
   >* 直接從全局導航窗格


### （選定）內容片段的操作 {#actions-selected-content-fragment}

選擇特定片段將開啟一個工具欄，該工具欄集中於該片段的可用操作。 您也可以選擇多個片段 — 操作的選擇將相應調整。

![內容片段控制台 — 所選片段的工具欄](assets/cfc-fragment-toolbar.png)

* **開啟**
* **發佈** (和&#x200B;**取消發佈**)
* **複製**
* **移動**
* **重新命名**
* **刪除**

>[!NOTE]
>
>發佈、取消發佈、刪除、移動、重新命名、複製等動作觸發非同步作業。可以透過 AEM 非同步作業 UI 監視該作業的進度。

## 提供的有關內容片段的資訊 {#information-content-fragments}

控制台的主/右面板（表視圖）提供了有關內容片段的一系列資訊。 一些項目還提供了指向進一步行動和/或資訊的直接連結：

* **名稱**
   * 提供在編輯器中開啟片段的連結。
* **模型**
   * 提供在編輯器中開啟片段的連結。
* **資料夾**
   * 提供在控制台中開啟資料夾的連結。
將游標停留在資料夾名稱上將顯示 JCR 路徑。
* **狀態**
   * 僅資訊
* **修改時間**
   * 僅資訊
* **修改者:**
   * 僅資訊
* **發佈於**
   * 僅資訊
* **發佈者**
   * 僅資訊
* **引用者**

   * 提供一個連結，該連結開啟一個對話框，列出該片段的所有父引用；包括引用內容片段、體驗片段和頁面。 要開啟特定參照，請按一下 **標題** 的子菜單。

      ![「內容片段」控制台 — 「引用」對話框](assets/cfc-console-references-dialog.png)

* **語言**

   * 指示內容片段的區域設定，以及與內容片段關聯的區域設定/語言副本的總數。

      ![內容片段控制台 — 語言指示器](assets/cfc-console-language-indicator.png)

      * 按一下/點擊計數以開啟顯示所有語言副本的對話框。 要開啟特定語言副本，請按一下 **標題** 的子菜單。

         ![內容片段控制台 — 語言對話框](assets/cfc-console-languages-dialog.png)

## 選擇可用列 {#select-available-columns}

與其他控制台一樣，您可以配置可見且可用於操作的列：

![內容片段控制台 — 列配置](assets/cfc-console-column-icon.png)

這將顯示可隱藏或顯示的列清單：

![內容片段控制台 — 列配置](assets/cfc-console-column-selection.png)

## 篩選片段 {#filtering-fragments}

「篩選器」面板提供：

* 選擇謂語；可以選擇一個或多個謂語並組合以建立篩選器
* 有機會 **保存** 配置
* 用於檢索已保存的搜索篩選器以供重新使用的選項

![內容片段控制台 — 篩選](assets/cfc-console-filter.png)

### 快速篩選 {#fast-filtering}

也可以通過按一下清單中的特定列值來選擇謂詞。 您可以選擇一個或多個值來組合謂語。

例如，選擇 **已發佈** 的 **狀態** 列：

>[!NOTE]
>
>僅支援 **模型**。 **狀態**。 **修改者**, **發佈者** 的子菜單。

![內容片段控制台 — 篩選](assets/cfc-console-fast-filter-01.png)

選中後，此清單將顯示為篩選器謂詞，並相應地篩選清單：

![內容片段控制台 — 篩選](assets/cfc-console-fast-filter-02.png)

## 搜索片段 {#searching-fragments}

搜索框支援全文搜索。 在搜索框中輸入搜索詞：

![內容片段控制台 — 搜索](assets/cfc-console-search-01.png)

將提供所選結果：

![內容片段控制台 — 搜索結果](assets/cfc-console-search-02.png)

搜索框還提供對 **最近的內容片段** 和 **保存的搜索**:

![內容片段控制台 — 最近和已保存](assets/cfc-console-search-03.png)
