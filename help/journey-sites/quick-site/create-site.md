---
title: 使用範本建立網站
description: 了解如何使用網站範本快速建立新的 AEM 網站。
exl-id: 31bb04c2-b3cc-44ca-b517-5b0d66d9b1fa
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: ht
source-wordcount: '1485'
ht-degree: 100%

---

# 使用範本建立網站 {#create-site-from-template}

{{traditional-aem}}

了解如何使用網站範本快速建立新的 AEM 網站。

## 目前進度 {#story-so-far}

在 AEM 快速建立網站歷程的上一份文件「[了解 Cloud Manager 和快速建立網站工作流程](cloud-manager.md)」中，您已了解 Cloud Manager 以及它如何與快速建立網站的新流程連結在一起，而您現在應該：

* 了解 AEM Sites 和 Cloud Manager 如何共同運作以促進前端開發
* 了解前端自訂步驟如何與 AEM 完全分離並且不需要瞭解 AEM 亦可操作。

本文章以這些基礎知識為基礎，協助您執行第一個設定步驟並使用範本建立一個網站，而您之後可以使用前端工具進行自訂。

## 目標 {#objective}

本文件協助您了解如何使用網站範本快速建立 AEM 網站。閱讀本文件後，您應該：

* 了解如何取得 AEM 網站範本。
* 了解如何使用範本建立網站。
* 了解如何從新網站下載範本以提供給前端開發人員。

## 負責角色 {#responsible-role}

歷程的這個部分適用於 AEM 管理員。

## 網站範本 {#site-templates}

網站範本是將基本網站內容結合成方便且可重複使用的套件之一種方法。網站範本通常包含基本網站內容和結構以及網站樣式資訊，以便快速啟動新網站。實際結構如下所示：

* `files`：包含 UI 套件、XD 檔案及可能有其他檔案的資料夾
* `previews`：包含網站範本螢幕擷圖的資料夾
* `site`：使用這個範本建立的每個網站的複製內容之內容包，例如頁面範本、各個頁面等。
* `theme`：修改網站外觀的範本主題來源，包括 CSS、JavaScript 等。

範本的功能強大，因為它們可以重複使用，您的內容作者可以快速建立網站。由於您安裝的 AEM 中可以有多個可用範本，因此您可以靈活地滿足各種業務需求。

>[!NOTE]
>
>網站範本與頁面範本不同，請勿混淆二者。此處所述的網站範本是指網站的整體結構。頁面範本定義單一頁面的結構和初始內容。

## 取得網站範本 {#obtaining-template}

開始使用的最簡單方法是[從 GitHub 存放庫下載最新版本的 AEM 標準網站範本](https://github.com/adobe/aem-site-template-standard/releases)。

下載後，您可以將其上傳到您的 AEM 環境，就像上傳任何其他套件一樣。若您想要此一主題的更多資訊，請參閱[「其他資源」區段](#additional-resources)了解如何使用套件的詳細資訊。

>[!TIP]
>
>您可以按照專案需求自訂 AEM 標準網站範本，也可以不需要進一步自訂。不過這個主題超出本歷程的範圍。如需更多資訊，請參閱標準網站範本的 GitHub 文件。

>[!TIP]
>
>您也可以在專案工作流程當中選擇使用來源來建立範本。不過這個主題超出本歷程的範圍。如需更多資訊，請參閱標準網站範本的 GitHub 文件。

## 安裝網站範本 {#installing-template}

使用範本可以輕鬆建立網站。

1. 登入您的 AEM 製作環境並導覽至 Sites 主控台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 選取畫面右上角的「**建立**」並從下拉式清單選取「**來自範本的網站**」。

   ![使用範本建立新網站](assets/create-site-from-template.png)

1. 在「建立網站」精靈中，選取左欄頂端的「**匯入**」。

   ![網站建立精靈](assets/site-creation-wizard.png)

1. 在檔案瀏覽器中，找到[您之前下載的](#obtaining-template)範本並選取「**上傳**」。

1. 上傳後，它會出現在可用範本清單中。選取該範本 (這也會在右欄中顯示範本相關資訊)，然後選取「**下一步**」。

   ![選取範本](assets/select-site-template.png)

1. 提供您的網站標題。如果省略的話，可以提供網站名稱或從標題產生。

   * 網站標題顯示在瀏覽器標題列中。
   * 網站名稱成為 URL 的一部分。

1. 選取「**建立**」然後使用網站範本建立新網站。

   ![新網站的詳細資訊](assets/create-site-details.png)

1. 在出現的確認對話框中，選取「**完成**」。

   ![成功對話框](assets/success.png)

1. 在Sites 主控台中，可以看見新網站，也可以進行導覽來探索其由範本定義的基本結構。

   ![新網站結構](assets/new-site.png)

內容作者現在可以開始製作。

## 是否需要進一步自訂？ {#customization-required}

網站範本功能極強大又靈活，而且一個專案可以建立任意數量的範本，可以輕鬆建立各種網站變體。根據您使用的網站範本上已執行的自訂程度，您甚至可能不需要額外自訂網站前端。

* 如果您的網站不需要額外自訂，恭喜您！您的歷程到此結束！
* 如果您仍然需要額外自訂網站前端，或者您只是想了解完整流程以備未來自訂之需求，請繼續閱讀。

## 範例頁面 {#example-page}

如果您確實需要額外自訂網站前端，請記住前端開發人員可能不熟悉您的內容的詳細資訊。因此，您可以為開發人員提供了解典型內容的路徑，以便在自訂主題時用作參考基礎。典型的例子是網站主語言的首頁。

1. 在網站瀏覽器中，導覽至網站主語言的首頁，然後選擇該頁面並在選單列選取「**編輯**」。

   ![典型首頁](assets/home-page-in-console.png)

1. 在編輯器中，在工具列選取「**頁面資訊**」按鈕，然後選取「**如發佈時檢視**」。

   ![編輯首頁](assets/home-page-edit.png)

1. 在開啟的標籤中，複製網址列中的內容路徑。它看起來像`/content/<your-site>/en/home.html?wcmmode=disabled`。

   ![首頁](assets/home-page.png)

1. 儲存該路徑，以便稍後提供給前端開發人員。

## 下載主題 {#download-theme}

現在已經建立網站，可以下載使用範本產生的網站主題並提供給前端開發人員進行自訂。

1. 在 Sites 主控台上，顯示「**網站**」邊欄。

   ![顯示網站邊欄](assets/show-site-rail.png)

1. 選擇新網站的根目錄，然後在網站邊欄中選取「**下載主題來源**」。

   ![下載主題來源](assets/download-theme-sources.png)

現在，您的下載檔案中有主題來源檔案的副本。

## 設定 Proxy 使用者 {#proxy-user}

為了讓前端開發人員能夠使用網站中實際的 AEM 內容來預覽自訂內容，您必須設定 Proxy 使用者。

1. 在 AEM 中，從主導航前往「**工具**」>「**安全**」>「**使用者**」。
1. 在使用者管理主控台中，選取「**建立**」。

   ![使用者管理主控台](assets/user-management-console.png)
1. 在「**建立新使用者**」視窗中，您必須至少提供：
   * **ID** - 記下此值，因為您必須將此值提供給前端開發人員。
   * **密碼** - 將此值安全地保存在密碼庫中，因為您必須將其提供給前端開發人員。

   ![新使用者詳細資訊](assets/new-user-details.png)

1. 在「**群組**」標籤中，將 Proxy 使用者新增至 `contributors` 群組。
   * 輸入字詞 `contributors` 觸發 AEM 的自動完成功能，可以輕鬆選取群組。

   ![新增到群組](assets/add-to-group.png)

1. 選取「**儲存並關閉**」。

您現在已經完成設定。內容作者現在可以在網站上建立內容，為歷程下一步的前端自訂做好準備。

## 下一步 {#what-is-next}

現在您已完成 AEM 快速建立網站歷程的這個部分，您應該：

* 了解如何取得 AEM 網站範本。
* 了解如何使用範本建立網站。
* 了解如何從新網站下載範本以提供給前端開發人員。

以此知識為基礎並接著檢閱文件「[設定您的管道](pipeline-setup.md)」，以繼續您的 AEM 快速建立網站歷程，您將會建立前端管道來管理網站主題的自訂內容。

## 其他資源 {#additional-resources}

雖然建議您檢閱文件「[設定您的管道](pipeline-setup.md)」以繼續快速建立網站歷程的下一部分，但下列是一些其他選用資源，深入探究了本文件提到的一些概念，不過這些資源並非繼續該歷程的必要條件。

* [AEM 標準網站範本](https://github.com/adobe/aem-site-template-standard) - 這是 AEM 標準網站範本的 GitHub 存放庫。
* [組織頁面](/help/sites-cloud/authoring/sites-console/organizing-pages.md)  - 本指南詳細介紹如何組織 AEM 網站的頁面。
* [建立頁面](/help/sites-cloud/authoring/sites-console/creating-pages.md)  - 本指南詳細介紹如何為您的網站新增頁面。
* [管理頁面](/help/sites-cloud/authoring/sites-console/managing-pages.md) - 本指南詳細介紹如何管理網站頁面，包括移動、複製和刪除。
* [如何使用套件](/help/implementing/developing/tools/package-manager.md) - 套件允許匯入和匯出存放庫內容。本文件說明如何使用 AEM 6.5 的套件，同樣適用於 AEMaaCS。
* [網站管理文件](/help/sites-cloud/administering/site-creation/create-site.md) - 查看關於建立網站的技術文件，了解快速建立網站工具功能的更多詳細資訊。
* [建立或新增表單至 AEM Sites 頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md) - 學習將表單與網站整合的逐步操作技巧和最佳實務，最佳化您的數位體驗以發揮最大影響。
