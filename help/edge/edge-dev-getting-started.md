---
title: 使用 Edge Delivery Services 進行 AEM 製作的開發人員快速入門指南
description: 本指南將協助您啟動並執行新的 Adobe Experience Manager 網站，以使用 Edge Delivery Services 和 Universal Editor 進行內容製作
feature: Edge Delivery Services
source-git-commit: 224cfe9853e8974c33b0e53e961a02d54f875a35
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 96%

---


# 使用 Edge Delivery Services 進行 AEM 製作 {#edge-dev-getting-started}

本指南將協助您啟動並執行新的 Adobe Experience Manager 網站，以使用 Edge Delivery Services 和 Universal Editor 進行內容製作。

{{aem-authoring-edge-early-access}}

## 先決條件 {#prerequisites}

在開始執行本指南之前，您應該要熟悉 Edge Delivery Services 的基礎知識並有權存取 Edge Delivery Services，其內容包括：

* 您已完成 [Edge Delivery Service 教學課程。](/help/edge/developer/tutorial.md)
* 您有權存取 [AEM Cloud Service 沙箱。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
* 您已[在同一沙箱環境中啟用 Universal Editor。](/help/implementing/universal-editor/getting-started.md)

## 選擇正確的編輯器 {#editor-choice}

AEM 提供兩種不同的內容編輯器，請您根據情況選擇要使用的編輯器。

* **Universal Editor** - 這是新網站的預設選項。
* **AEM 頁面編輯器** - 應選擇此編輯器將現有 AEM Sites 移轉到 Edge Delivery Services。

本指南重點在於使用 Universal Editor 的 Edge Delivery Services 上的 AEM 專案。請參閱文件「[Edge Delivery Services 開發](/help/edge/developing.md)」，以進一步了解有關選擇正確編輯器以及將現有 AEM Sites 移轉到 Edge Delivery Services 的詳細資訊。

## AEM Authoring 和 Edge Delivery Services 快速入門 {#getting-started}

滿足[先決條件](#prerequisites)並選擇[使用Universal Editor](#editor-choice) 後，您就可以開始製作自己的專案。

### 建立您的 GitHub 專案 {#create-github-project}

首先，您需要根據 Adobe 範本在 GitHub 上建立一個新專案。

1. 瀏覽至 [`https://github.com/adobe-rnd/aem-boilerplate-xwalk`](https://github.com/adobe-rnd/aem-boilerplate-xwalk)，然後按一下「**使用此範本**」並選取「**建立新存放庫**。

   * 您需要登入 GitHub 才能看到此選項。

   ![複製存放庫專案](assets/edge-dev-getting-started/use-template-project.png)

1. 預設情況下，將會指派存放庫給您。請根據需要進行變更，並提供存放庫名稱和說明，然後按一下「**建立存放庫**」。

   ![建立存放庫](assets/edge-dev-getting-started/create-repo.png)

1. 在同一瀏覽器的新標籤中，瀏覽至 [`https://github.com/apps/aem-code-sync`](https://github.com/apps/aem-code-sync)，然後按一下「**設定**」。

   ![Code Sync](assets/edge-dev-getting-started/configure-code-sync.png)

1. 請對您在上一個步驟中建立新存放庫的組織，按一下「**設定**」。

   ![選擇組織以同步程式碼](assets/edge-dev-getting-started/code-sync-org.png)

1. 在 AEM Code Sync GitHub 頁面的「**存放庫存取權**」底下，選取「**僅選取存放庫**」，選取您在上一個步驟中建立的存放庫，然後按一下「**儲存**」。

   ![授予 AEM Code Sync 存取權](assets/edge-dev-getting-started/grant-code-sync-acces.png)

1. 安裝 AEM Code Sync 後，您會收到確認畫面。返回新存放庫的瀏覽器標籤。

   ![Code Sync 安裝確認](assets/edge-dev-getting-started/confirmation.png)

1. 按一下「`fstab.yaml`」檔案將其打開，然後按一下「**編輯此檔案**」圖示進行編輯。

   ![fstab.yaml](assets/edge-dev-getting-started/fstab.png)

1. 編輯 `fstab.yaml` 檔案以更新專案的掛載點。將預設的 Google 文件 URL 替換為 AEM as a Cloud Service 製作執行個體的 URL，然後按一下「**提交變更...**」。

   * `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`
   * 變更掛載點會告訴 Edge Delivery Services 在哪裡可以找到網站的內容。

   ![更新 fstab](assets/edge-dev-getting-started/fstab-update.png)

1. 根據需要新增提交訊息，然後按一下「**提交變更**」，將其直接提交到 `main` 分支。

   ![提交變更](assets/edge-dev-getting-started/commit-fstab-changes.png)

1. 返回存放庫的根目錄，按一下「`paths.yaml`」，然後按一下「**編輯此檔案**」圖示。

   ![paths.yaml](assets/edge-dev-getting-started/paths.png)

1. 將預設對應替換為 `/content/<site-name>/:/`，然後按一下「**提交變更...**」。

   * 提供您自己的 `<site-name>`。後續步驟中還會需要它。
   * 對應會告訴 Edge Delivery Services 如何將 AEM 存放庫中的內容對應到網站 URL。

   ![更新 paths.yaml](assets/edge-dev-getting-started/paths-update.png)

1. 根據需要新增提交訊息，然後按一下「**提交變更**」，將其直接提交到 `main` 分支。

   ![提交變更](assets/edge-dev-getting-started/commit-fstab-changes.png)

### 建立和編輯新的 AEM 網站 {#create-aem-site}

現在您已擁有 GitHub 專案，接著必須建立該專案可以使用的新 AEM 網站。

>[!NOTE]
>
>若要使用 Universal Editor 編輯您的網站，您必須使用 Chromium 式瀏覽器。

1. 透過您的「[專案 Slack 管道](/help/edge/docs/slack.md)」向 Adobe Engineering 要求最新的「使用 Edge Delivery Services 進行 AEM 製作」網站範本。

1. 登入您的 AEM as a Cloud Service 製作執行個體，並瀏覽至 Sites 主控台，然後點選或按一下「**建立** -> **根據範本的網站**」。

   ![從主控台建立新網站](assets/edge-dev-getting-started/create-site-console.png)

1. 在建立網站精靈的「**選取網站範本**」標籤上，按一下「**匯入**」按鈕以匯入新範本。

   ![匯入範本](assets/edge-dev-getting-started/site-templates.png)

1. 上傳 Adobe Engineering 為您提供的「使用 Edge Delivery Services 進行 AEM 製作」網站範本。

1. 匯入範本後，該範本將出現在精靈中。點選或按一下以選取該範本，然後點選或按一下「**下一步**」。

   ![選取範本](assets/edge-dev-getting-started/select-template.png)

1. 提供以下欄位，然後點選或按一下「**建立**」。

   * **網站標題** - 為網站新增描述性標題。
   * **網站標題** - 使用您在[上一個步驟](#create-github-project)中定義的 `<site-name>`。
   * **GitHub URL** - 使用您在上一個步驟中建立的 GitHub 專案的 URL。

   ![網站詳細資訊](assets/edge-dev-getting-started/create-site-details.png)

1. AEM 會透過對話方塊確認建立網站。點選或按一下「**確認**」以關閉對話方塊。

   ![網站建立確認](assets/edge-dev-getting-started/site-creation-confirmation.png)

1. 在網站主控台上，瀏覽到新建立網站的 `index.html`，然後在工具列中點選或按一下「**編輯**」。

   ![編輯新網站](assets/edge-dev-getting-started/new-site.png)

1. Universal Editor 會在新標籤中開啟。您可能需要點選或按一下「**使用 Adobe 登入**」進行身分驗證以編輯您的頁面。

   ![Universal Editor](assets/edge-dev-getting-started/universal-editor.png)

現在您可以使用 Universal Editor 編輯您的網站。如需詳細資訊，請參閱 [Universal Editor 文件](/help/implementing/universal-editor/authoring.md)。

### 發佈您的新網站 {#publishing}

使用 Universal Editor 編輯完新網站後，您就可以發佈內容。

1. 在網站主控台上，選取所有您為新網站建立的頁面，然後點選或按一下工具列中的「**快速發佈**」。

   ![選取要發佈的頁面](assets/edge-dev-getting-started/publishing.png)

1. 點選或按一下確認對話方塊中的「**發佈**」以啟動該程序。

   ![發佈對話方塊](assets/edge-dev-getting-started/publish-confirmation.png)

1. 在同一瀏覽器中開啟一個新標籤並瀏覽到新網站的 URL。

   * `https://main--<site-name>--<owner>.hlx.page`

1. 查看您發佈的內容。

   ![已發佈的內容](assets/edge-dev-getting-started/published-site.png)

## 後續步驟 {#next-steps}

現在您已擁有使用Edge Delivery Services專案的AEM編寫功能，可以開始建立自己的區塊並設定樣式。

請參閱指南 [建立可搭配通用編輯器使用的區塊](/help/edge/create-block.md) 以取得詳細資訊。
