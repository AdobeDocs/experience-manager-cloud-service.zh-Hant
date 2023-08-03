---
title: 建立及組織頁面
description: 瞭解如何使用AEM建立和管理頁面，以組織您的網站。
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: 31e6ec8e9977c8787e14481ee3a94df767262aec
workflow-type: tm+mt
source-wordcount: '2544'
ht-degree: 4%

---

# 建立及組織頁面 {#creating-and-organizing-pages}

本檔案說明如何使用Adobe Experience ManagerCloud Service建立和管理頁面，以便您可以 [建立內容](/help/sites-cloud/authoring/fundamentals/editing-content.md) 這些頁面上的。

>[!NOTE]
>
>若要在頁面上執行建立、複製、移動、編輯和刪除等動作，您的帳戶需要適當的存取許可權和許可權。
>
>如果您遇到任何問題，我們建議您連絡系統管理員。

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to take action on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>有許多種 [鍵盤快速鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 您可從網站主控台使用，以便更有效率地組織頁面。

## 組織您的網站 {#organizing-your-website}

身為作者，您需要在AEM中組織您的網站。 這涉及建立和命名內容頁面，以便：

* 您可以在作者環境中輕鬆找到他們
* 您網站的訪客可在發佈環境中輕鬆瀏覽這些專案

您也可以使用 [資料夾](#creating-a-new-folder) 協助組織您的內容。

網站的結構可視為儲存內容頁面的樹狀結構。 這些內容頁面的名稱會用於組成URL，而標題則會在檢視頁面內容時顯示。

以下範例將來自 [WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant) 網站，其中有一篇關於滑板場( `la-skateparks`)已存取：

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

此結構可從下列位置檢視： **網站** 主控台，您可以 [瀏覽您網站的各個頁面](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) 並在頁面上執行動作。 您也可以建立新網站和 [新頁面](#creating-a-new-page).

從任何點開始，您都可以從標頭列的階層連結看到向上分支：

![使用階層連結進行導覽](/help/sites-cloud/authoring/assets/organizing-breadcrumbs.png)

### 頁面命名慣例 {#page-naming-conventions}

建立新頁面時，有兩個索引鍵欄位：

* **[標題](#title)**:

   * 主控台會向使用者顯示這項資訊，並在編輯時顯示在頁面內容的頂端。
   * 此欄位為必填.

* **[名稱](#name)**:

   * 這會用來產生URI。
   * 此欄位的使用者輸入為選用。 如果未指定，則會從標題衍生名稱。 請參閱下節 [頁面名稱限制和最佳實務](#page-name-restrictions-and-best-practices) 以取得詳細資訊。

#### 頁面名稱限制和最佳實務 {#page-name-restrictions-and-best-practices}

頁面 **標題****和名稱可以單獨建立** ，但是是相關的：

* 建立頁面時，僅 **標題** 欄位為必填。 若否 **名稱** 在建立頁面時提供，AEM會從標題的前64個字元產生名稱（觀察以下列出的驗證）。 僅前64個字元用於支援短頁面名稱的最佳做法。
* 如果作者手動指定頁面名稱，64字元限制不適用，但頁面名稱長度的其他技術限制可能適用。

>[!TIP]
>
>定義頁面名稱時，一個好的經驗法則是保持頁面名稱簡短，但儘可能表達到位且容易記憶，讓讀者容易理解。 請參閱 [W3C風格指南](https://www.w3.org/Provider/Style/TITLE.html) 針對 `title` 元素以取得詳細資訊。
>
>也請記住，某些瀏覽器（例如舊版的IE）只能接受一定長度的URL，因此還有技術原因需縮短頁面名稱。

建立新頁面時，AEM會 [根據慣例驗證頁面名稱](/help/implementing/developing/introduction/naming-conventions.md) 由AEM和JCR所強制。

允許的最小字元為：

* `a` 到 `z`
* `A` 到 `Z`
* `0` 到 `9`
* `_` （底線）
* `-` （連字型大小/減號）

所有允許字元的完整詳細資訊可在以下連結中找到： [命名慣例](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>頁面名稱長度上限為150個字元。

#### 標題 {#title}

如果您在建立新頁面時只提供頁面 **Title** ,AEM會從此字串衍生頁面 **Name**[ ，並根據AEM和JCR所強加的慣例來驗證名稱。](/help/implementing/developing/introduction/naming-conventions.md)

A **標題** 接受包含無效字元的欄位，但衍生的名稱會以無效的字元取代。 例如：

| 標題 | 衍生名稱 |
|---|---|
| Schon | `schoen.html` |
| SC%&amp;&#42;c+ | `sc---c-.html` |

#### 名稱 {#name}

當您提供頁面時 **名稱** 建立新頁面時，AEM會 [根據慣例驗證名稱](/help/implementing/developing/introduction/naming-conventions.md) 由AEM和JCR所強制。 您無法在中提交無效的字元 **名稱** 欄位。 當AEM偵測到無效字元時，此欄位會以說明訊息強調顯示。

![輸入無效頁面名稱的範例](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>除非是語言根，否則應避免使用ISO-639-1定義的雙字母代碼作為頁面名稱。
>
>另請參閱 [準備翻譯內容](/help/sites-cloud/administering/translation/preparation.md) 以取得詳細資訊。

### 範本 {#templates}

在AEM中，範本會指定特殊型別的頁面。 範本會用作任何建立新頁面的基礎。

範本定義包含縮圖影像和其他屬性的頁面結構。 例如，您可以為產品頁面、Sitemap和聯絡資訊使用不同的範本。 範本包括 [元件](#components).

AEM隨附幾個現成可用的範本。 可用的範本視個別網站而定。 主要欄位包括：

* **標題**
在產生的網頁上顯示的標題。

* **名稱**
用於命名頁面。

* **範本**
可在產生新頁面時使用的範本清單。

>[!TIP]
>
>如果您已在執行個體上設定， [範本作者可以使用範本編輯器建立範本](/help/sites-cloud/authoring/features/templates.md).

### 元件 {#components}

元件是AEM提供的元素，可供您新增特定型別的內容。 AEM隨附一系列現成可用的元件，提供完善的功能。 這些類別包括：

* 文字
* 影像
* 標題
* 傳送
* 以及更多功能

建立並開啟頁面後，您可以 [使用元件新增內容](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component)，可從取得 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

>[!TIP]
>
>此 [元件主控台](/help/sites-cloud/authoring/features/components-console.md) 提供執行個體上元件的概述。

## 管理頁面 {#managing-pages}

### 建立新頁面 {#creating-a-new-page}

除非所有頁面都已預先為您建立，否則您必須先建立頁面，然後才能開始建立內容：

1. 開啟Sites主控台(例如 `https://<host>:<port>/sites.html/content`.
1. 導覽至您要建立新頁面的位置。
1. 使用開啟下拉式選擇器 **建立** 在工具列中選取「 」 **頁面** 從清單：

   ![建立頁面](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. 從精靈的第一階段，您可以：

   * 選取您要用來建立新頁面的範本，然後按一下/點選 **下一個** 以繼續進行。

   * **取消** 以中止程式。

   ![為新頁面選取範本](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. 在精靈的最後階段，您可以：

   * 使用三個索引標籤來輸入 [頁面屬性](/help/sites-cloud/authoring/fundamentals/page-properties.md) 您要指派給新頁面，然後按一下/點選 **建立** 以實際建立頁面。

   * 使用 **返回** 以返回範本選取。

   主要欄位包括：

   * **標題**:

      * 這會向使用者顯示，且是強制性的。

   * **名稱**:

      * 這會用來產生URI。 如果未指定，則會從標題衍生名稱。
      * 如果您提供頁面 **名稱** 建立新頁面時，AEM會 [根據慣例驗證名稱](/help/implementing/developing/introduction/naming-conventions.md) 由AEM和JCR所強制。
      * 您 **無法提交無效的字元** 在 **名稱** 欄位。 當AEM偵測到無效字元時，該欄位會醒目顯示，並顯示說明訊息，指出需要移除/取代的字元。

   >[!TIP]
   >
   >另請參閱 [頁面命名慣例](#page-naming-conventions).

   建立新頁面所需的最低資訊為 **標題**.

   ![提供頁面標題](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. 使用 **建立** 以完成程式並建立您的新頁面。 確認對話方塊會詢問您是否要執行 **開啟** 立即頁面或返回主控台(**完成**)：

   ![頁面建立成功](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >如果您使用該位置已存在的名稱來建立頁面，系統將藉由附加一個編號來自動產生名稱的變體。 例如，如果 `beach` 已存在，則新頁面會變成 `beach1`.

1. 如果您返回主控台，則會看到新頁面：

   ![產生的新頁面](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>建立頁面後，無法變更其範本，除非您 [使用新範本建立啟動項](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)，但會遺失任何現有內容。

### 開啟頁面進行編輯 {#opening-a-page-for-editing}

建立頁面或（在主控台中）導覽至現有頁面後，您可以開啟頁面進行編輯：

1. 開啟 **網站** 主控台。
1. 導覽至找到您要編輯的頁面為止。
1. 使用下列任一專案選取您的頁面：

   * [快速動作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) 和工具列

   然後選取 **編輯** 圖示：

   ![編輯按鈕](/help/sites-cloud/authoring/assets/edit.png)

1. 頁面隨即開啟，您可以 [編輯頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md) 視需要。

>[!NOTE]
>
>只有在「預覽」模式中才能從頁面編輯器導覽至其他頁面，因為連結在「編輯」模式中無效。

### 複製和貼上頁面 {#copying-and-pasting-a-page}

您可以將頁面及其所有子頁面複製到新位置：

1. 在 **網站** 主控台，導覽至找到要複製的頁面為止。
1. 使用以下其中一種方式選取您的頁面：

   * [快速動作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) 和工具列

   然後 **複製** 頁面圖示：

   ![複製](/help/sites-cloud/authoring/assets/copy.png)

1. 導覽至頁面新復本的位置。
1. 點選或按一下 **貼上** 圖示可用。

   ![貼上](/help/sites-cloud/authoring/assets/paste.png)

1. 「貼上」對話方塊會顯示貼上交易的摘要，以及執行下列功能的功能：
   * **新網站名稱：** 變更已貼上頁面的名稱
   * **貼上（不含子系）：** 貼上時省略所選頁面的子頁面（預設會貼上子頁面）

   ![貼上對話方塊](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. 點選或按一下 **貼上** 按鈕以確認貼上交易並建立新頁面。

>[!NOTE]
>
>如果您將頁面複製到某個位置，而該位置已經存在名稱與原始名稱相同的頁面，則系統將藉由附加一個編號來自動產生名稱的變體。 例如，如果 `beach` 已存在，已存在名稱為的新頁面 `beach` 變為 `beach1`.

>[!NOTE]
>
>如果您在選擇模式中啟動貼上動作，這會在頁面複製後立即自動結束。

### 移動或重新命名頁面 {#moving-or-renaming-a-page}

移動或重新命名頁面的程式基本相同，這兩個動作都由「移動頁面」精靈處理。 使用此精靈，您可以：

* 重新命名頁面而不移動頁面
* 移動頁面而不重新命名
* 同時移動和重新命名

AEM提供可更新任何內部連結的功能，這些連結會參照正在重新命名/移動的頁面。 您可以逐頁進行，提供完整的彈性。

1. 導覽，直到找到您要移動的頁面為止。
1. 使用以下其中一種方式選取您的頁面：

   * [快速動作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) 和工具列

   然後選取 **移動** 頁面圖示：

   ![移動按鈕](/help/sites-cloud/authoring/assets/move.png)

   這將會開啟移動頁面精靈。

1. 從 **重新命名** 精靈的階段您可以：

   * 指定移動頁面後您希望頁面使用的名稱，然後按一下/點選 **下一個** 以繼續進行。
   * **取消** 以中止程式。

   ![移動和重新命名頁面](/help/sites-cloud/authoring/assets/move-page-rename.png)

   如果您只移動頁面，頁面名稱可以維持不變。

   >[!NOTE]
   >
   >如果您將頁面移至相同名稱的頁面已經存在的位置，系統將藉由附加編號來自動產生名稱的變體。 例如，如果 `beach` 已存在，已存在名稱為的新頁面 `beach` 變為 `beach1`.

1. 從 **選取目的地** 精靈的階段您可以：

   * 使用 [欄檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) 若要導覽至頁面的新位置：

      * 按一下目的地的縮圖，以選取目的地。
      * 按一下 **下一個** 以繼續。

   * 使用 **返回** 以返回頁面名稱規格。

   >[!NOTE]
   >
   >依照預設，您正在移動或重新命名的頁面的父頁面會選取為目的地。

   ![選取頁面移動目的地](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >如果您將頁面移至相同名稱的頁面已經存在的位置，系統將藉由附加編號來自動產生名稱的變體。 例如，如果 `winter` 已存在， `winter` 變為 `winter1`.

1. 如果頁面已連結至或參考，或已發佈，則詳細資訊會列在 **調整/重新發佈** 步驟。

   您可以指出哪些頁面應適當地調整及/或重新發佈。

   >[!NOTE]
   >
   >如果頁面既未連結也未參考，則無法使用此步驟。

   ![移動時重新發佈頁面](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. 選取 **移動** 將會完成程式，並視需要移動/重新命名頁面。

>[!NOTE]
>
>如果頁面已發佈，移動頁面會自動將其取消發佈。 依預設，移動完成時會重新發佈它，但取消勾選即可變更此設定。 **重新發佈** 中的欄位 **調整/重新發佈** 步驟。

>[!NOTE]
>
>如果頁面未經任何引用，則 **調整/重新發佈** 已略過步驟。

>[!NOTE]
>
>重新命名頁面也必須遵循 [頁面命名慣例](#page-naming-conventions) 指定新頁面名稱時。

>[!NOTE]
>
>只能將頁面移至允許該頁面所依據的範本位置。 另請參閱 [範本可用性](/help/implementing/developing/components/templates.md#template-availability) 以取得詳細資訊。

#### 非同步動作 {#asynchronous-actions}

通常，頁面移動或重新命名動作會立即執行。 這將視為同步處理，在動作完成之前，會封鎖UI中的進一步動作。

但是，如果受影響的頁數超過定義的限制，系統會以非同步方式處理動作，讓使用者能夠不受頁面移動或重新命名動作的阻礙，繼續在UI中編寫。

* 按一下 **移動** 在上述最後一個步驟中，AEM會檢查設定的限制。
* 如果受影響的頁數低於限制，會執行同步作業。
* 如果受影響的頁數超過限制，系統就會執行非同步作業。
   * 使用者必須定義何時應執行非同步操作
      * **現在** 會立即開始執行非同步作業。
      * **稍後** 可讓使用者定義非同步作業何時開始。

        ![非同步頁面移動](/help/sites-cloud/authoring/assets/asynchronous-page-move.png)

您可在以下位置檢查非同步作業的狀態： [**非同步工作狀態** 儀表板](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) 在 **全域導覽** -> **工具** -> **作業** -> **工作**

>[!NOTE]
>
>如需有關非同步作業處理以及如何設定頁面移動/重新命名動作限制的詳細資訊，請參閱 [非同步作業](/help/operations/asynchronous-jobs.md) 檔案。

### 刪除頁面 {#deleting-a-page}

1. 導覽，直到您可以看見要刪除的頁面為止。
1. 使用 [選擇模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 以選取所需頁面，然後使用 **刪除** 從工具列：

   ![刪除按鈕](/help/sites-cloud/authoring/assets/delete.png)

   >[!NOTE]
   >
   >為了安全起見，「刪 **** 除」頁面圖示不能作為快速動作使用。

1. 對話方塊將會要求確認。

   ![刪除對話方塊](/help/sites-cloud/authoring/assets/delete-page.png)

   * **您要在刪除前先封存頁面嗎?**  — 如果勾選，刪除時會建立選取要刪除之頁面的版本。
      * [日後可以還原這些版本](/help/sites-cloud/authoring/features/page-versions.md).
      * 沒有舊版刪除的頁面無法還原。
   * **取消** 中止動作
   * **刪除** 若要確認動作：

      * 如果頁面沒有參考，則會刪除頁面。
      * 如果頁面含有參考，則會出現訊息方塊通知您 **一個或多個頁面被引用。** 您可以選取 **強制刪除** 或 **取消**.

>[!NOTE]
>
>如果頁面已發佈，則在刪除前會自動取消發佈。

### 鎖定頁面 {#locking-a-page}

您可以 [鎖定/解鎖頁面](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) 從主控台或編輯個別頁面時。 有關頁面是否已鎖定的資訊也會顯示在這兩個位置。

![「鎖定」按鈕](/help/sites-cloud/authoring/assets/lock.png)
![解鎖按鈕](/help/sites-cloud/authoring/assets/unlock.png)

### 建立新資料夾 {#creating-a-new-folder}

您可以建立資料夾來協助組織您的檔案和頁面。

1. 開啟 **網站** 主控台並導覽至所需位置。
1. 若要開啟選項清單，請選取 **建立** 從工具列
1. 選取 **資料夾** 以開啟對話方塊。 您可在此輸入 **名稱** 和 **標題**：

   ![建立資料夾](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. 選取 **建立** 以建立資料夾。

>[!NOTE]
>
>資料夾也必須遵守 [頁面命名慣例](#page-naming-conventions) 指定新資料夾名稱時。

>[!CAUTION]
>
>* 資料夾只能直接建立在 **網站** 或位於其他資料夾下。 無法在頁面下建立縮圖。
>* 您可以在資料夾上執行移動、複製、貼上、刪除、發佈、取消發佈和檢視/編輯屬性的標準動作。
>* 無法在即時副本中選取資料夾。
