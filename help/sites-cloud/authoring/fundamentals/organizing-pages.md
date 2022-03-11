---
title: 建立及組織頁面
description: 如何建立和組織頁AEM面
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: 93e0eac6e329c7a0c54cf592b097014d39a8eb17
workflow-type: tm+mt
source-wordcount: '2560'
ht-degree: 7%

---

# 建立及組織頁面 {#creating-and-organizing-pages}

本文檔介紹如何使用Adobe Experience ManagerCloud Service建立和管理頁面，以便 [建立內容](/help/sites-cloud/authoring/fundamentals/editing-content.md) 那幾頁。

>[!NOTE]
>
>您的帳戶需要相應的訪問權限和權限才能對頁面執行操作，如建立、複製、移動、編輯和刪除。
>
>如果您遇到任何問題，我們建議您與系統管理員聯繫。

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to take action on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>有 [鍵盤快捷鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 可以從網站控制台使用。

## 組織您的網站 {#organizing-your-website}

作為作者，您需要在中組織您的網AEM站。 這包括建立和命名內容頁，以便：

* 在作者環境中可以輕鬆找到它們
* 訪問您的網站的訪問者可以在發佈環境中輕鬆瀏覽這些網站

您還可以使用 [資料夾](#creating-a-new-folder) 來組織內容。

網站的結構可以視為保存內容頁面的樹。 這些內容頁的名稱用於形成URL，而標題在查看頁面內容時顯示。

下面顯示了 [WKND教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) 地點，那裡有一篇關於滑板的文章( `la-skateparks`)。

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

此結構可從 **站點** 控制台，您可以 [瀏覽網站的頁面](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) 並在頁面上執行操作。 您還可以建立新站點和 [新頁](#creating-a-new-page)。

從任何點上，您都可以在標題欄中看到麵包屑向上的分支：

![使用麵包屑導航](/help/sites-cloud/authoring/assets/organizing-breadcrumbs.png)

### 頁面命名約定 {#page-naming-conventions}

建立新頁面時，有兩個鍵欄位：

* **[標題](#title)**:

   * 這將在控制台中顯示給用戶，並在編輯時顯示在頁面內容的頂部。
   * 此欄位為必填.

* **[名稱](#name)**:

   * 這用於生成URI。
   * 此欄位的用戶輸入是可選的。 如果未指定，則從標題派生名稱。 請參閱以下部分 [頁名限制和最佳做法](#page-name-restrictions-and-best-practices) 的雙曲餘切值。

#### 頁名限制和最佳做法 {#page-name-restrictions-and-best-practices}

頁面 **標題****和名稱可以單獨建立** ，但是是相關的：

* 建立頁面時，僅 **標題** 欄位。 否 **名稱** 在建立頁面時提供，AEM將根據標題的前64個字元生成名稱（按照下面設定的驗證）。 僅使用前64個字元來支援短頁名稱的最佳做法。
* 如果作者手動指定了頁名，則64個字元的限制不適用，但頁名長度上的其他技術限制可能不適用。

>[!TIP]
>
>在定義頁面名稱時，一個很好的經驗法則是保持頁面名稱簡短但盡可能具有表達力和記憶力，以便讓讀者更容易理解。 查看 [W3C樣式指南](https://www.w3.org/Provider/Style/TITLE.html) 為 `title` 的子菜單。
>
>還要記住，某些瀏覽器（如舊版IE）只能接受長度不超過一定的URL，因此，還有技術原因需要縮短頁名。

建立新頁面時AEM, [根據約定驗證頁名](/help/implementing/developing/introduction/naming-conventions.md) 由AEMJCR強加。

允許的最小字元數為：

* `a` 通 `z`
* `A` 通 `Z`
* `0` 通 `9`
* `_` （下划線）
* `-` （連字元/減號）

所有允許字元的完整詳細資訊，請參閱 [命名約定](/help/implementing/developing/introduction/naming-conventions.md)。

>[!NOTE]
>
>頁名限制為150個字元。

#### 標題 {#title}

如果您在建立新頁面時只提供頁面 **Title** ,AEM會從此字串衍生頁面 **Name**[ ，並根據AEM和JCR所強加的慣例來驗證名稱。](/help/implementing/developing/introduction/naming-conventions.md)

A **標題** 將接受包含無效字元的欄位，但派生的名稱將替換無效字元。 例如：

| 標題 | 派生名稱 |
|---|---|
| 捨恩 | `schoen.html` |
| SC%&amp;*ç+ | `sc---c-.html` |

#### 名稱 {#name}

提供頁面時 **名稱** 建立新頁面時，AEM將 [根據約定驗證名稱](/help/implementing/developing/introduction/naming-conventions.md) 和JCRAEM強加的。 無法提交 **名稱** 的子菜單。 當檢AEM測到無效字元時，該欄位將用解釋性消息突出顯示。

![輸入無效頁名的示例](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>您應避免使用ISO-639-1定義的雙字母代碼作為頁名，除非它是語言根。
>
>請參閱 [準備翻譯內容](/help/sites-cloud/administering/translation/preparation.md) 的子菜單。

### 範本 {#templates}

在AEM中，模板指定專用的頁面類型。 模板將用作建立任何新頁面的基礎。

該模板定義包含縮略圖和其它屬性的頁面的結構。 例如，您可能有單獨的產品頁面、模板和聯繫資訊模板。 模板由 [元件](#components)。

附AEM帶了幾個現成的模板。 可用的模板取決於單個網站。 關鍵欄位為：

* **標題**
結果網頁上顯示的標題。

* **名稱**
在命名頁面時使用。

* **模板**
生成新頁時可用的模板清單。

>[!TIP]
>
>如果在實例上配置， [模板作者可以使用模板編輯器建立模板](/help/sites-cloud/authoring/features/templates.md)。

### 元件 {#components}

元件是提供的元AEM素，以便您可以添加特定類型的內容。 AEM附帶一系列提供全面功能的現成元件。 這些包括：

* 文字
* 影像
* 標題
* 傳送
* 還有更多

建立並開啟頁面後，您可以 [使用元件添加內容](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component)，可從 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。

>[!TIP]
>
>的 [元件控制台](/help/sites-cloud/authoring/features/components-console.md) 概述實例上的元件。

## 管理頁面 {#managing-pages}

### 建立新頁面 {#creating-a-new-page}

除非已提前為您建立了所有頁面，否則您必須先建立一個頁面，然後才能開始建立內容：

1. 開啟「站點」控制台(例如， `https://<host>:<port>/sites.html/content`。
1. 導航到要建立新頁面的位置。
1. 使用工具列中的「建立」 **** ，開啟下拉式選取器，然後從清單中選 **取「頁面** 」:

   ![建立頁面](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. 在嚮導的第一階段，您可以執行以下任一操作：

   * 選擇要用於建立新頁面的模板，然後按一下/點擊 **下一個** 繼續。

   * **取消** 中止進程。

   ![為新頁面選擇模板](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. 在嚮導的最後階段，您可以執行以下任一操作：

   * 使用三個頁籤輸入 [頁屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md) 要分配給新頁面，請按一下/點擊 **建立** 的子菜單。

   * 使用 **後退** 返回到模板選擇。

   關鍵欄位為：

   * **標題**:

      * 這將顯示給用戶，並且是強制的。
   * **名稱**:

      * 這用於生成URI。 如果未指定，則從標題派生名稱。
      * 如果您提供頁面 **名稱** 建立新頁面時，AEM將 [根據約定驗證名稱](/help/implementing/developing/introduction/naming-conventions.md) 和JCRAEM強加的。
      * 你 **無法提交無效字元** 的 **名稱** 的子菜單。 檢測AEM到無效字元時，該欄位將突出顯示，並顯示一條說明性消息，指示需要刪除/替換的字元。

   >[!TIP]
   >
   >請參閱 [頁面命名約定](#page-naming-conventions)。

   建立新頁面所需的最低資訊是 **標題**。

   ![提供頁面標題](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. 使用 **建立** 完成該流程並建立新頁面。 確認對話框將詢問您是否要 **開啟** 立即或返回控制台(**完成**):

   ![頁面建立成功](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >如果使用該位置已存在的名稱建立頁面，系統將通過附加數字自動生成名稱的變體。 例如， `beach` 已存在新頁面 `beach1`。

1. 如果返回到控制台，您將看到新頁面：

   ![生成的新頁](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>建立頁面後，其模板將無法更改 — 除非 [使用新模板建立啟動](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)，但這將丟失任何現有內容。

### 開啟頁面進行編輯 {#opening-a-page-for-editing}

在建立頁面或導航到現有頁面（在控制台中）後，可以開啟該頁面進行編輯：

1. 開啟 **站點** 控制台。
1. 導航，直到找到要編輯的頁面。
1. 使用以下任一選項選擇頁面：

   * [快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) 工具欄

   然後選擇 **編輯** 表徵圖：

   ![「編輯」按鈕](/help/sites-cloud/authoring/assets/edit.png)

1. 該頁面將開啟，您可以 [編輯頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md) 按需要。

>[!NOTE]
>
>只有在「預覽」模式下，才能從頁面編輯器導航到其他頁面，因為連結在「編輯」模式下不處於活動狀態。

### 複製和貼上頁面 {#copying-and-pasting-a-page}

您可以將頁面及其所有子頁面複製到新位置：

1. 在 **站點** 控制台，導航直到找到要複製的頁。
1. 使用以下任一選項選擇頁面：

   * [快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) 工具欄

   然後 **複製** 表徵圖：

   ![複製](/help/sites-cloud/authoring/assets/copy.png)

1. 導航到頁面新副本的位置。
1. 點擊或按一下 **貼上** 表徵圖。

   ![貼上](/help/sites-cloud/authoring/assets/paste.png)

1. 「貼上」對話框顯示貼上事務的摘要，並提供以下功能：
   * **新站點名稱：** 更改貼上的頁面的名稱
   * **無子項貼上：** 貼上時忽略所選頁面的子頁面（預設情況下貼上子頁面）

   ![貼上對話框](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. 點擊或按一下 **貼上** 按鈕，確認貼上事務並建立新頁。

>[!NOTE]
>
>如果將頁面複製到與原始頁面具有相同名稱的頁面已存在的位置，則系統將通過附加數字自動生成名稱的變體。 例如， `beach` 已存在一個名為的新頁 `beach` 將 `beach1`。

>[!NOTE]
>
>如果在選擇模式下啟動貼上操作，則複製頁面後會立即自動退出。

### 移動或更名頁面 {#moving-or-renaming-a-page}

移動或更名頁面的過程基本相同，兩個操作都由「移動頁面」嚮導處理。 使用此嚮導，您可以：

* 更名頁面而不移動
* 移動頁面而不更名它
* 同時移動和更名

提AEM供了更新任何引用要更名/移動的頁面的內部連結的功能。 這可以逐頁完成，以提供完全的靈活性。

1. 導航，直到找到要移動的頁面。
1. 使用以下任一選項選擇頁面：

   * [快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) 工具欄

   然後選擇 **移動** 表徵圖：

   ![「移動」按鈕](/help/sites-cloud/authoring/assets/move.png)

   這將開啟移動頁面嚮導。

1. 從 **更名** 嚮導的階段，您可以：

   * 指定移動頁面後希望其具有的名稱，然後按一下/點擊 **下一個** 繼續。
   * **取消** 中止進程。

   ![移動和更名頁面](/help/sites-cloud/authoring/assets/move-page-rename.png)

   如果僅移動頁面，則頁面名稱可保持不變。

   >[!NOTE]
   >
   >如果將頁面移動到已存在同名頁面的位置，系統將通過附加一個數字自動生成名稱的變體。 例如， `beach` 已存在一個名為的新頁 `beach` 將 `beach1`。

1. 從 **選擇目標** 嚮導的階段，您可以：

   * 使用 [列視圖](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) 要導航至頁面的新位置，請執行以下操作：

      * 通過按一下目標的縮略圖來選擇目標。
      * 按一下 **下一個** 繼續。
   * 使用 **後退** 返回頁名規範。

   >[!NOTE]
   >
   >預設情況下，您移動/更名的頁面的父級將被選擇為目標。

   ![選擇頁面移動目標](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >如果將頁面移動到已存在同名頁面的位置，系統將通過附加一個數字自動生成名稱的變體。 例如， `winter` 已存在 `winter` 將 `winter1`。

1. 如果該頁面已連結或引用，或已發佈，則詳細資訊將列在 **調整/重新發佈** 的子菜單。

   您可以指明應根據需要調整和/或重新發佈哪些內容。

   >[!NOTE]
   >
   >如果頁面既未連結也未引用，則此步驟將不可用。

   ![移動時重新發佈頁面](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. 選擇 **移動** 將完成該過程，並根據需要移動/更名頁面。

>[!NOTE]
>
>如果頁面已發佈，移動頁面會自動解除發佈。依預設，移動完成時會重新發佈它，但是這可透過取消勾選「調整/重新發佈」步驟中的「重新發佈 **」欄位來** 變更 **** 。

>[!NOTE]
>
>如果頁面未以任何方式引用，則 **調整/重新發佈** 將跳過步驟。

>[!NOTE]
>
>更名頁面也受 [頁面命名約定](#page-naming-conventions) 指定新頁名時。

>[!NOTE]
>
>只能將頁面移動到允許基於頁面的模板的位置。 請參閱 [模板可用性](/help/implementing/developing/components/templates.md#template-availability) 的子菜單。

#### 非同步操作 {#asynchronous-actions}

通常，頁面移動或更名操作會立即執行。 這被視為同步處理，在操作完成之前，UI中的進一步操作將被阻止。

但是，如果受影響的頁數超過定義的限制，則非同步處理該操作，允許用戶在UI中繼續創作，不受頁面移動或更名操作的阻礙。

* 按一下 **移動** 在上面的最後一步中，檢AEM查配置的限制。
* 如果受影響的頁數低於限制，則執行同步操作。
* 如果受影響的頁數超過限制，則執行非同步操作。
   * 用戶必須定義何時應執行非同步操作
      * **現在** 立即開始執行非同步作業。
      * **稍後** 允許用戶定義非同步作業何時啟動。

         ![非同步頁面移動](/help/sites-cloud/authoring/assets/asynchronous-page-move.png)

可以在中檢查非同步作業的狀態 [**非同步作業狀態** 儀表板](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) 在 **全局導航** -> **工具** -> **操作** -> **作業**

>[!NOTE]
>
>有關非同步作業處理以及如何配置頁面移動/更名操作限制的詳細資訊，請參閱 [非同步作業](/help/operations/asynchronous-jobs.md) 的子菜單。

### 刪除頁面 {#deleting-a-page}

1. 導航，直到您看到要刪除的頁面。
1. 使用 [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 選擇所需頁，然後使用 **刪除** 的下界：

   ![刪除按鈕](/help/sites-cloud/authoring/assets/delete.png)

   >[!NOTE]
   >
   >為了安全起見，「刪 **** 除」頁面圖示不能作為快速動作使用。

1. 對話會要求確認。

   ![刪除對話框](/help/sites-cloud/authoring/assets/delete-page.png)

   * **您要在刪除前先封存頁面嗎?**  — 如果選中，則刪除時將建立選定刪除的頁面版本。
      * [版本可以在以後恢復。](/help/sites-cloud/authoring/features/page-versions.md)
      * 無法還原刪除且沒有以前版本的頁面。
   * **取消**&#x200B;來中止動作
   * **刪除**&#x200B;來確認動作：

      * 如果頁面沒有任何參考，則會刪除頁面。
      * 如果頁面有引用，則消息框將通知您 **引用一個或多個頁面。**&#x200B;您可以選取&#x200B;**強制刪除**&#x200B;或&#x200B;**取消**。

>[!NOTE]
>
>如果已發佈頁面，則在刪除前將自動取消發佈該頁面。

### 鎖定頁面 {#locking-a-page}

你可以 [鎖定/解鎖頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) 從控制台或編輯單個頁面時。 有關頁面是否已鎖定的資訊也顯示在這兩個位置。

![鎖定按鈕](/help/sites-cloud/authoring/assets/lock.png)
![解鎖按鈕](/help/sites-cloud/authoring/assets/unlock.png)

### 建立新資料夾 {#creating-a-new-folder}

您可以建立資料夾以幫助組織檔案和頁面。

1. 開啟 **站點** 控制台並導航到所需位置。
1. 要開啟選項清單，請選擇 **建立** 的子菜單。
1. 選擇 **資料夾** 的子菜單。 在此，您可以輸入 **名稱** 和 **標題**:

   ![建立資料夾](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. 選擇 **建立** 的子菜單。

>[!NOTE]
>
>資料夾也受 [頁面命名約定](#page-naming-conventions) 指定新資料夾名稱時。

>[!CAUTION]
>
>* 只能直接在 **站點** 或其他資料夾下。 無法在頁面下建立它們。
>* 可以對資料夾執行標準操作移動、複製、貼上、刪除、發佈、取消發佈和檢視/編輯屬性。
>* 資料夾在即時副本中無法選擇。

