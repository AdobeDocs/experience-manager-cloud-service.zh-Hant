---
title: 在 Cloud Manager 中使用您自己的 GitHub 存放庫
description: 了解如何設定 Cloud Manager 以搭配使用您自己的 GitHub 存放庫。
feature: Release Information
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 70%

---


# 在 Cloud Manager 中使用您自己的 GitHub 存放庫 {#byo-github}

透過設定 Cloud Manager 以搭配使用您自己的 GitHub 存放庫，您可以透過 Cloud Manager 直接在 GitHub 存放庫中驗證程式碼，無需始終將程式碼與 Adobe 存放庫保持同步。

>[!NOTE]
>
>此功能僅適用於[早期採用者方案。](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## 設定 {#configuration}

設定包括兩個主要步驟：

1. [新增存放庫](#add-repo)
1. [私人存放庫所有權驗證](#validate-ownership)

### 新增存放庫 {#add-repo}

1. 在Cloud Manager中，從 **計畫總覽** 頁面，選取 **存放庫** 標籤以切換至 **存放庫** 頁面並按一下 **新增存放庫**.

1. 在&#x200B;**新增存放庫**&#x200B;對話框，選取&#x200B;**私人存放庫**&#x200B;作為存放庫類型。

1. 提供存放庫的詳細資訊

   * **存放庫名稱** - 讓人易懂的名稱
   * **存放庫 URL** - 存放庫的 URL，必須以 `.git` 結尾
   * **說明** (選擇性) - 必要時提供存放庫更長的說明

   ![新增自己的存放庫](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. 選取&#x200B;**儲存**。

>[!TIP]
>
>如需有關在Cloud Manager中管理存放庫的詳細資訊，請參閱 [Cloud Manager存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

### 私人存放庫所有權驗證 {#validate-ownership}

Cloud Manager 現在知道您的 GitHub 存放庫，但仍然需要存取它。若要授予存取權，您需要安裝 Adobe GitHub 應用程式並驗證您擁有指定的存放庫。

1. 新增您自己的存放庫後， **私人存放庫所有權驗證** 對話方塊開啟。

   ![私人存放庫所有權驗證](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

1. Cloud Manager 使用 GitHub 應用程式與您的存放庫安全地互動。
   * 您 GitHub 組織的擁有者必須安裝位於 `https://github.com/apps/cloud-manager-for-aem-stage` 的應用程式，並授予存放庫的存取權。
   * 如需有關如何執行此動作的詳細資訊，請參閱GitHub的檔案。

1. 為了提高安全性，您必須在存放庫的預設分支中建立密碼檔案。選取 **產生**.

1. 點選或按一下&#x200B;**確認**&#x200B;來確認產生密碼檔案。

   ![確認密碼產生](/help/implementing/cloud-manager/assets/repos/confirm-generation.png)

1. 回到&#x200B;**私人存放庫所有權驗證**&#x200B;視窗中，Cloud Manager 已在&#x200B;**密碼檔案內容**&#x200B;欄位產生私人檔案內容。複製該欄位中的內容。

   * 密碼檔案的內容只會顯示一次。如果您在關閉此視窗之前未複製內容，請重新產生密碼。

   ![複製密碼檔案內容](/help/implementing/cloud-manager/assets/repos/new-secret.png)

1. 在 GitHub 存放庫的預設分支中建立一個名為 `.well-known/adobe/cloud-manager-challenge` 的新檔案，並將密碼檔案內容貼到該檔案並儲存。

1. 安裝應用程式且存放庫中存在機密檔案後，您可以選取 **驗證** 在 **私人存放庫所有權驗證** 對話方塊。

可以按任何順序安裝應用程式並建立密碼檔案。但是，必須先完成這兩個步驟才能進行驗證。

在驗證之前，存放庫將以紅色圖示列出，表示它尚未驗證且尚無法使用。

![未經驗證的存放庫](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

此 **型別** 欄可輕鬆識別Adobe提供的存放庫(**Adobe**)和您自己的GitHub存放庫(**GitHub**)。

如果您日後需要返回存放庫完成驗證，請在 **存放庫** 頁面上，選取代表您剛才新增GitHub存放庫之列中的省略符號按鈕，然後選取 **所有權驗證** （從下拉式功能表）。

## 將您自己的 GitHub 存放庫搭配 Cloud Manager 使用 {#using}

在 Cloud Manager 中驗證 GitHub 存放庫後，整合即完成，您可以在 Cloud Manager 中使用該存放庫。

1. 當您建立提取要求時，GitHub 檢查將自動啟動。

   ![GitHub 檢查](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. 對於每個提取要求，[全端程式碼品質管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)將自動建立。此管道在每次提取要求更新時啟動。

1. GitHub 檢查保持運作狀態，直到程式碼品質檢查完成。然後程式碼品質結果將傳播到 GitHub 檢查。

   ![GitHub 程式碼品質檢查](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

當提取要求關閉或合併時，建立的全端程式碼品質管道將自動刪除。

## 限制 {#limitations}

搭配Cloud Manager使用您自己的GitHub存放庫時的限制。

* 您不能使用GitHub存放庫作為您管理的管道的直接存放庫來源。
   * 此功能規劃中。
* 您無法使用Cloud Manager中的GitHub檢查來暫停提取請求驗證。
   * 如果 GitHub 存放庫在 Cloud Manager 已經過驗證，為該存放庫建立的提取要求，Cloud Manager 將一律進行驗證。
如果您的 GitHb 組織已移除 Adobe GitHub 應用程式，這將移除所有存放庫的提取要求驗證。
