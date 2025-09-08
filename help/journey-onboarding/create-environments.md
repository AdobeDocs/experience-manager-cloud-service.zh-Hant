---
title: 建立環境
description: 了解如何使用 Cloud Manager 來建立您的首個環境。
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
feature: Onboarding
source-git-commit: 9c5838a01ceecf094aea19578e6560a5e5ca8c4c
workflow-type: ht
source-wordcount: '775'
ht-degree: 100%

---

# 建立環境 {#create-environments}

在這部分的[上線歷程](overview.md)中，您會了解如何使用 Cloud Manager 建立您的第一個環境。

## 目標 {#objective}

在閱讀了此上線歷程中的上一份文件「[建立程序](create-program.md)」後，您現在擁有自己的 Cloud Manager 程序。現在，您可以了解如何使用 Cloud Manager 為該方案建立您的第一個環境。

閱讀本文件後，您將了解：

* 了解什麼是環境。
* 了解不同環境之間的區別。
* 能夠建立自己的環境。

## 什麼是環境？ {#environments}

環境位於 Cloud Manager 層次結構中的程序之下。雖然程序允許您組織您的解決方案並授予特定團隊成員對這些程序的存取權限，但環境屬於特定程序並且是這些程序中 Adobe 解決方案的各個實例。環境用於特定目的，例如創作內容或測試新開發。透過 Cloud Manager 的 CI/CD 管道，將程式碼從 Git 存放庫部署至這些環境變得更容易。

如果您還記得虛構的 WKND 旅遊與冒險企業的範例，他們是一家專注於旅遊相關媒體的租用戶。他們可能有兩個方案。一個用於 WKND 雜誌部門的 Sites 方案，和一個用於 WKND 媒體部門的 Assets 方案。每個方案都可能有數個環境，例如一個處理網站實際流量的生產環境，和一個用於測試新應用程式程式碼的開發環境。

有五種不同類型的環境：

* **生產與暫存** - 生產環境和中繼環境組成一組使用，分別用於生產和測試目的。
* **開發** - 可以為開發和測試目的建立開發環境，也可以只與非生產管道相關聯。
* **快速開發** - 快速開發環境 (RDE) 讓開發人員能夠快速部署及審閱變更。這個環境用最少的時間來測試那些已經在本機開發環境中證實可以運作的功能。
* **專門的測試環境** - 提供專用空間以便在接近生產環境的條件下驗證各項功能，非常適合壓力測試和進階的部署前檢查。

為了達成此上線歷程的目的，讓您從最基本的內容開始，您需要建立可用於探索 AEM as a Cloud Service 功能的開發環境。

## 建立環境 {#creating-environments}

>[!NOTE]
>
>系統會將建立環境的使用者記錄為其建立者。因為已刪除的使用者有時候可以還原，因此請謹慎選擇環境建立者。

**若要建立環境：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 選取要新增環境的程序。

1. 若要新增環境，在「**方案概觀**」頁面的「**環境**」卡片中，選取「**新增環境**」選項。

   ![環境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **新增環境**&#x200B;選項也可在&#x200B;**環境**&#x200B;索引標籤上找到。

     ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 由於缺少權限或根據授權的資源，**新增環境**&#x200B;選項可能會停用。

1. 在「**新增環境**」對話框中，執行下列操作：

   * 選取&#x200B;**環境類型**。
      * 可用/已使用環境的數量會顯示在開發環境類型後面的括號中。
   * 提供&#x200B;**環境名稱**。
   * 提供&#x200B;**環境說明**。
   * 選取&#x200B;**雲端區域**。

   ![新增環境對話框](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 按一下&#x200B;**儲存**，以新增指定的環境。

待環境一旦可用，組織中指派至&#x200B;**開發人員**&#x200B;產品設定檔的成員便可以登入 Cloud Manager，及管理 Cloud Manager 的 Git 存放庫。

## 後續步驟 {#whats-next}

您已閱讀此上線歷程部分，您應該：

* 了解什麼是環境。
* 了解不同環境之間的區別。
* 能夠建立自己的環境。

您的團隊現在可以存取您所建立的雲端資源。做為系統管理員，您首先必須從 Adobe Admin Console 將您的團隊成員指派至 AEM as a Cloud Service 的產品設定檔，以們他們能夠存取這些資源。

因此，您接下來應該檢閱[將團隊成員指派至 AEM as a Cloud Service 產品設定檔](assign-profiles-aem.md)文件，然後繼續您的上線歷程。在該文件中，您會了解如何授予團隊成員存取新環境的權限。

## 其他資源 {#additional-resources}

如果您想了解上線歷程以外的內容，以下是其他選用資源。

* [管理環境](/help/implementing/cloud-manager/manage-environments.md) - 了解您可以建立的環境類型，以及如何為您的 Cloud Manager 專案建立環境。
* [使用 Adobe Cloud Manager - 環境](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/cloud-manager/environments)- Cloud Manager 環境由 AEM 編寫、發佈和 Dispatcher 服務組成。了解不同的環境如何支援各種角色，並可以使用不同的 CI/CD 管道進行互動。
* [快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md) - 請參閱此文件，詳細了解如何使用 RDE
<!-- ERROR: Not Found (HTTP error 404) FIND AN ALTERNATE RESOURCE? * [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Watch this video for an overview of Cloud Manager environment types from an AEM champion. -->

