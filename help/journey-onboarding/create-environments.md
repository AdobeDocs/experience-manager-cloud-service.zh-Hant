---
title: 建立環境
description: 了解如何使用 Cloud Manager 來建立您的首個環境。
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 100%

---

# 建立環境 {#create-environments}

在[到職歷程](overview.md)的這一部分，您將學習如何使用 Cloud Manager 建立您的第一個環境。

## 目標 {#objective}

在閱讀了此上線過程中的上一個文件後，[建立程序，](create-program.md)您現在擁有自己的 Cloud Manager 程序。了解如何使用 Cloud Manager 來建立您的首個環境。

閱讀本文件後，您將了解：

* 了解什麼是環境。
* 了解不同環境之間的區別。
* 能夠建立自己的環境。

## 什麼是環境？ {#environments}

環境位於 Cloud Manager 層次結構中的程序之下。雖然程序允許您組織您的解決方案並授予特定團隊成員對這些程序的存取權限，但環境屬於特定程序並且是這些程序中 Adobe 解決方案的各個實例。環境用於特定目的，例如創作內容或測試新開發。Cloud Manager 的 CI/CD 管道有助於將計劃碼從 git 存放庫部署到這些環境。

如果您回想一下理論上的 WKND Travel and Adventure Enterprises 的範例，他們是一家專注於旅遊相關媒體的租使用者，他們可能有兩個計劃：一個用於 WKND 雜誌部門的 Sites 計劃和一個用於 WKND 媒體部門的 Assets 計劃。每個程序都可能有幾個環境，例如一個為網站的實際流量提供服務的生產環境和一個用於測試新應用程序計劃碼的開發環境。

有三種不同類型的環境：

* **生產與暫存** - 生產環境和暫存環境組成一組使用，分別用於生產和測試目的。
* **開發** - 可以為開發和測試目的建立開發環境，並且只能與非生產管道相關聯。

出於此上線之旅的目的，您將建立一個開發環境。

## 建立環境 {#creating-environments}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要新增環境的方案。

1. 在&#x200B;**計畫總覽**&#x200B;頁面，按一下&#x200B;**環境**&#x200B;卡上的&#x200B;**新增環境**&#x200B;以新增環境。

   ![環境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **新增環境**&#x200B;選項也可在&#x200B;**環境**&#x200B;索引標籤上找到。

      ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 由於缺少權限或根據授權的資源，**新增環境**&#x200B;選項可能會停用。

1. 在出現的&#x200B;**新增環境**&#x200B;對話框中：

   * 選取&#x200B;**環境類型**。
      * 可用/已使用環境的數量會顯示在開發環境類型後面的括號中。
   * 提供&#x200B;**環境名稱**。
   * 提供&#x200B;**環境說明**。
   * 選取&#x200B;**雲端區域**。

   ![新增環境對話框](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 按一下&#x200B;**儲存**，以新增指定的環境。

環境可用後，您組織的成員將指派到&#x200B;**開發商** product profile 可以登入 Cloud Manager 管理 Cloud Manager 的 git 倉庫。

## 下一步 {#whats-next}

您已閱讀此入門歷程部分，您應該：

* 了解什麼是環境。
* 了解不同環境之間的區別。
* 能夠建立自己的環境。

您的雲端資源已建立並可供您的團隊存取。作為系統管理員，您必須首先從 Adobe Admin Console 將您的團隊成員指派給 AEM as a Cloud Service 產品設定檔，以便他們存取這些資源。

因此，您應該透過接下來查看文件來繼續您的上線之旅[將團隊成員指派給 AEM as a Cloud Service 產品設定檔。](assign-profiles-aem.md)在該文件中，您將了解如何授予團隊成員存取新環境所需的權限。

## 其他資源 {#additional-resources}

按照其他資源了解：

* [管理環境](/help/implementing/cloud-manager/manage-environments.md) - 了解您可以建立的環境類型，以及如何為您的 Cloud Manager 專案建立環境類型。
* [使用 Adobe Cloud Manager - 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=zh-Hant)- Cloud Manager 環境由 AEM 創作、發布和調度服務組成。了解不同的環境可支援角色，並使用不同的 CI/CD 管道與其互動。
