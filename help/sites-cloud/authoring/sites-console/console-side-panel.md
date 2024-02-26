---
title: 網站主控台側面板
description: 瞭解如何使用AEM Sites主控台中的側邊面板，以更加瞭解並導覽您的內容。
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 5%

---


# 網站主控台側面板 {#side-panel}

瞭解如何使用AEM中的側面板 **網站** 主控台，以更加瞭解並導覽您的內容。

## 方向 {#orientation}

依預設，當您輸入 **網站** 主控台。 如此一來，畫面就會完全專用於您的內容。

點選或按一下 **側面板** 圖示於 **網站** 控制檯工具列以啟動側面板並選擇您的內容檢視。

* [僅限內容](#content-only)
* [內容樹狀結構](#content-tree)
* [時間軸](#timeline)
* [參考](#references)
* [網站](#site)
* [篩選條件](#filter)
* [設定 Analytics](#setup-analytics)

![Sites主控台的側面板檢視](assets/sites-console-side-panel-views.png)

目前選取的檢視在下拉式清單中以藍色核取記號表示，而工具列中的側面板圖示會以所選檢視的名稱更新。

## 僅限內容 {#content-only}

這個側面板的檢視實際上是關閉它，也就是它只會顯示您網站的內容。

>[!TIP]
>
>使用抑音符號/反勾號 `´` 鍵盤快速鍵可切換至側面板的「僅限內容」檢視。

## 內容樹狀結構 {#content-tree}

側面板的這個檢視以樹狀階層顯示您的內容。 內容樹可用來快速導覽側面板中的網站階層，並檢視目前資料夾中頁面的許多相關資訊。

![側面板的內容樹狀檢視](assets/console-side-panel-content-tree.png)

樹狀結構中專案旁的右側V形箭號表示可以展開以顯示其子項的節點。 點選或按一下>形箭號以顯示子系。

主控台會顯示內容樹中目前選取專案的內容。

使用內容樹側面板搭配清單檢視或卡片檢視，您可以輕鬆檢視專案的階層結構，並使用內容樹側面板輕鬆瀏覽內容結構，並在清單檢視中檢視詳細的頁面資訊。

>[!TIP]
>
>* 使用 `Alt+1` 切換至側面板內容樹檢視的鍵盤快速鍵。
>* 選取階層檢視中的專案後，可使用方向鍵來快速瀏覽階層。
>* 另請參閱 [鍵盤快速鍵](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) 以取得詳細資訊。

## 時間軸 {#timeline}

時間軸可用於檢視影響所選資源的事件。 您也可以用它來啟動某些事件，例如工作流程或版本。

![時間表詳細資訊](/help/sites-cloud/authoring/assets/timeline-detail.png)

此 **時間表** 側面板可讓您檢視與所選專案相關的各種事件，這些所選專案可從下拉式清單中選取為型別：

* 評論
* [註解](/help/sites-cloud/authoring/page-editor/annotations.md)
* [活動](/help/sites-cloud/authoring/personalization/activities.md)
* [啟動](/help/sites-cloud/authoring/launches/overview.md)
* [版本](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [工作流程](/help/sites-cloud/authoring/workflows/overview.md)
   * 請注意，不會顯示暫時性工作流程的任何資訊，因為不會儲存這些工作流程的歷史記錄資訊。<!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
* 顯示全部

此外，您可以使用來新增/檢視有關所選專案的註解 **註解** 方塊顯示在事件清單的底部。 輸入評論後接 `Return` 將註冊註解。 當選取「注 **釋** 」或「 **全部顯示** 」時顯示。

在 **網站** 主控台您也可以透過旁邊的省略符號按鈕存取其他功能 **註解** 欄位。

* [儲存版本](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [啟動工作流程](/help/sites-cloud/authoring/workflows/applying.md)

![網站主控台註解欄位](assets/sites-console-comment-ellipsis.png)

>[!TIP]
>
>* 使用 `Alt+2` 切換至側面板之時間軸檢視的鍵盤快速鍵。
>* 另請參閱 [鍵盤快速鍵](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) 以取得詳細資訊。

## 參考 {#references}

此 **引用** 檢視顯示在主控台中選取之資源的參照型別清單。

![參考詳細資料](assets/console-side-panel-references-detail.png)

選取適當的參照型別以取得詳細資訊。 在某些情況下，當您選取特定參照時，可使用進一步的動作，包括：

* **傳入連結**，提供參照頁面的頁面清單，並可直接存取 **編輯** 其中一個頁面。
   * 這只能顯示靜態連結，而不能顯示動態產生的連結，例如來自清單元件的連結。
* [啟動](/help/sites-cloud/authoring/launches/overview.md)，提供相關啟動項的存取權
* [即時副本](/help/sites-cloud/administering/msm/overview.md) 顯示以所選資源為基礎之所有即時副本的路徑。
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md)，提供詳細資訊和各種動作
* [語言副本](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel)，提供詳細資訊和各種動作

## 網站 {#site}

此 **網站** 側面板的檢視會顯示網站的詳細資訊 [使用網站範本建立。](/help/sites-cloud/administering/site-creation/create-site.md)

![網站面板](assets/console-side-panel-site-paenl.png)

檢視檔案 [使用網站面板管理您的網站主題](/help/sites-cloud/administering/site-creation/site-rail.md) 以進一步瞭解如何使用面板管理 [您的網站主題。](/help/sites-cloud/administering/site-creation/site-themes.md).

如果您尚未設定前端管道以啟用主題型網站建立，側面板將提供該選項。

![啟用側面板中前端管線的選項](assets/sites-console-side-panel-site.png)

>[!TIP]
>
>從範本建立網站並自訂其主題的程式的端對端說明可在以下連結中找到： [快速網站建立歷程。](/help/journey-sites/quick-site/overview.md)

## 篩選條件 {#filter}

此 **篩選** 面板類似於 [搜尋功能](/help/sites-cloud/authoring/search.md) 並設定適當的位置篩選器，讓您進一步篩選想要檢視的內容。

![篩選器範例](assets/console-side-panel-filter.png)

不同於側面板的其他檢視，若要切換到另一個檢視，請點選或按一下 `X` 在搜尋欄位中。

## 設定 Analytics {#setup-analytics}

此檢視可讓您為選取的網站快速設定Adobe Analytics。

![設定Analytics](assets/sites-console-side-panel-setup-analytics.png)
