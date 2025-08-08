---
title: 建立環境
description: 了解如何使用 Cloud Manager 來建立您的首個環境。
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
feature: Onboarding
source-git-commit: 9c5838a01ceecf094aea19578e6560a5e5ca8c4c
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 62%

---

# 建立環境 {#create-environments}

在這部分的[上線歷程](overview.md)中，您會了解如何使用 Cloud Manager 建立您的第一個環境。

## 目標 {#objective}

在閱讀了此上線歷程中的上一份文件「[建立程序](create-program.md)」後，您現在擁有自己的 Cloud Manager 程序。現在，您可以瞭解如何使用Cloud Manager來建立您的首個環境。

閱讀本文件後，您將了解：

* 了解什麼是環境。
* 了解不同環境之間的區別。
* 能夠建立自己的環境。

## 什麼是環境？ {#environments}

環境位於 Cloud Manager 層次結構中的程序之下。雖然程序允許您組織您的解決方案並授予特定團隊成員對這些程序的存取權限，但環境屬於特定程序並且是這些程序中 Adobe 解決方案的各個實例。環境用於特定目的，例如創作內容或測試新開發。Cloud Manager的CI/CD管道有助於將計畫碼從Git存放庫部署到這些環境。

如果您回想一下理論上的WKND Travel and Adventure Enterprises的範例，他們是一個專注於旅遊相關媒體的租使用者。 他們可能有兩個方案。亦即，WKND Magazine部門的一個Sites計畫，以及WKND Media部門的一個Assets計畫。 每個程序都可能有幾個環境，例如一個為網站的實際流量提供服務的生產環境和一個用於測試新應用程式程式碼的開發環境。

有五種不同型別的環境：

* **生產與暫存** - 生產環境和中繼環境組成一組使用，分別用於生產和測試目的。
* **開發** - 可以為開發和測試目的建立開發環境，也可以只與非生產管道相關聯。
* **快速開發** — 快速開發環境(RDE)可讓開發人員快速部署及檢閱變更。 如此一來，測試經證實可在本機開發環境中運作的功能所花費的時間便得以縮減。
* **專業測試環境** — 提供專屬的空間，在接近生產的條件下驗證功能，非常適合壓力測試和進階預先部署檢查。

基於此歷程的目的，為了讓您從最基本開始，您將建立可用來探索 AEM as a Cloud Service 功能的開發環境。

## 建立環境 {#creating-environments}

>[!NOTE]
>
>系統會將建立環境的使用者記錄為其建立者。 因為刪除的使用者有時可以還原，所以請謹慎選擇環境建立者。

**若要建立環境：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 選取要新增環境的程序。

1. 若要新增環境，請從&#x200B;**方案總覽**&#x200B;頁面，在&#x200B;**環境**&#x200B;卡片上，選取&#x200B;**新增環境**&#x200B;選項。

   ![環境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **新增環境**&#x200B;選項也可在&#x200B;**環境**&#x200B;索引標籤上找到。

     ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 由於缺少權限或根據授權的資源，**新增環境**&#x200B;選項可能會停用。

1. 在&#x200B;**新增環境**&#x200B;對話方塊中，執行下列動作：

   * 選取&#x200B;**環境類型**。
      * 可用/已使用環境的數量會顯示在開發環境類型後面的括號中。
   * 提供&#x200B;**環境名稱**。
   * 提供&#x200B;**環境說明**。
   * 選取&#x200B;**雲端區域**。

   ![新增環境對話框](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 按一下&#x200B;**儲存**，以新增指定的環境。

環境可用後，您組織的成員將指派到&#x200B;**開發人員**&#x200B;產品設定檔可以登入Cloud Manager並管理Cloud Manager Git存放庫。

## 後續步驟 {#whats-next}

您已閱讀此上線歷程部分，您應該：

* 了解什麼是環境。
* 了解不同環境之間的區別。
* 能夠建立自己的環境。

您的團隊現在可以存取您建立的雲端資源。 作為系統管理員，首先，您必須從 Adobe Admin Console 將您的團隊成員指派給 AEM as a Cloud Service 產品設定檔，以便他們存取這些資源。

因此，您應該透過接下來檢視檔案[將團隊成員指派給AEM as a Cloud Service產品設定檔](assign-profiles-aem.md)來繼續您的上線之旅。 在該檔案中，您將瞭解如何授予團隊成員對新環境的許可權。

## 其他資源 {#additional-resources}

如果您想了解上線歷程以外的內容，以下是其他選用資源。

* [管理環境](/help/implementing/cloud-manager/manage-environments.md) - 了解您可以建立的環境類型，以及如何為您的 Cloud Manager 專案建立環境。
* [使用 Adobe Cloud Manager - 環境](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/cloud-manager/environments)- Cloud Manager 環境由 AEM 編寫、發佈和 Dispatcher 服務組成。瞭解不同的環境如何支援角色，並使用不同的CI/CD管道與其互動。
* [快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md) - 請參閱此文件以詳細了解如何使用 RDE
<!-- ERROR: Not Found (HTTP error 404) FIND AN ALTERNATE RESOURCE? * [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Watch this video for an overview of Cloud Manager environment types from an AEM champion. -->

