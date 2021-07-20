---
title: 透過Cloud Manager設定雲端資源
description: 請依照本頁所述了解如何透過Cloud Manager設定雲端資源
hide: true
hidefromtoc: true
index: false
source-git-commit: 021146e4e1d65c7fe81ed3dba70b32daf34b9704
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# 透過Cloud Manager設定雲端資源 {#setup-cloud-resources}

指派給「業務擁有者」角色的系統管理員應存取並登入Cloud Manager。 之後，指派給「業務擁有者」產品設定檔的團隊成員必須登入Cloud Manager並建立雲端方案和環境，才能開始使用您的專家團隊。

## 目標 {#objective}

本檔案可協助您了解雲端資源的建立方式，以及由誰執行。

閱讀本小節後，您應：

* 了解指派給「業務擁有者」角色的系統管理員必須是第一個存取及登入Cloud Manager的管理員
* 了解雲端程式和環境的建立方式。

## 簡介 {#introduction}

新增雲端資源是由指派給Cloud Manager業務擁有者產品設定檔的團隊成員透過Cloud Manager完成。 此人通常了解業務需求，並完成初始Cloud Manager設定。

請依照以下各節了解如何建立您的[雲端服務程式](#create-cloud-service-program)和[environments](#create-cloud-environments)。

### 先決條件 {#prerequisites}

* 指派給「業務擁有者」角色的系統管理員應存取並登入Cloud Manager。

* 了解如何導覽及登入Cloud Manager

* 熟悉Cloud Manager產品設定檔

* 了解建立方案時的考量事項。 請觀看此影片以深入了解。

* 了解Cloud Manager程式和環境的概念

## 導覽至Cloud Manager {#navigate-cloud-manager}

1. 「業務擁有者」使用者會收到歡迎電子郵件，歡迎您從這裡開始使用，或如果找不到，請直接前往experience.adobe.com並使用您的Adobe ID登入。

1. 從Experience Cloud首頁，選擇Experience Manager:


1. 這會帶您前往AEM首頁。 在此選取Cloud Manager:


1. 這會帶您前往Cloud Manager登陸頁面，如下所示：


1. 現在，請確認您已獲派「業務擁有者產品設定檔」。 若要這麼做，請選取右上角的設定檔，如下所示：


1. 現在，選擇「用戶角色」並確保已將您分配給「業務所有者」。


   幹得好！ 您已成功以業務擁有者身分登入Cloud Manager!

## 建立Cloud Service方案 {#create-cloud-service-program}


1. 導覽至Cloud Manager登陸頁面，如下所示。

   >[!NOTE]
   >您必須是指派給Cloud Manager業務擁有者產品設定檔的團隊成員，才能成功完成此步驟。

1. 從此處，選擇添加程式以啟動添加程式嚮導。 觀看影片，了解如何建立您的AEMaaCS計畫，以及在建立計畫前的重要考量。

1. 有關如何使用「添加程式」嚮導的逐步說明，請轉至此處。

   >[!CAUTION]
   >請記住，建立後無法更改程式名。 建議您確定要提供程式的名稱。

   如果您必須變更方案名稱，則需要開啟Adobe支援的案例，或聯絡您的Adobe代表。 他們將協助您有效刪除程式。 你必須重新開始，因為你的團隊可能會失去工作。

1. 成功建立雲端方案後，您可以導覽至方案，查看方案的概觀頁面，如下所示：

1. 如果您尚未這麼做，現在是將開發人員成員新增至Cloud Manager團隊的最佳時機，請前往「將使用者新增至開發人員產品設定檔」，並遵循概述的步驟。

1. 指派給開發人員產品設定檔的成員可登入Cloud Manager和Manage Cloud Manager Git。


   幹得好！ 現在程式已成功建立，您的Cloud Manager Git可供開發人員存取！


## 建立雲端環境 {#create-cloud-environments}

1. 成功建立雲端程式後，請導覽至Cloud Manager概觀頁面並從環境卡片中選取「新增」 ，以建立雲端環境。

   >[!NOTE]
   >必須登入業務擁有者或部署管理員角色中的Cloud Manager使用者，才能成功完成此步驟。

   此外，請觀看快速影片教學課程，以了解Cloud Manager環境，以及如何將其新增至您的方案。

1. 這會啟動「新增環境」精靈，引導您新增環境。 先新增您的開發環境，以熟悉。

1. 如果您尚未這麼做，可以立即將開發人員成員新增至您的Cloud Manager團隊，前往「將使用者新增至開發人員產品設定檔」，並遵循概述的步驟。 如此一來，您的開發人員就能開始導覽至Cloud Manager及管理Cloud Manager Git。


   恭喜！ 現在，您的雲端程式環境已建立完畢，且您的開發人員已新增至團隊中！

## 下一步 {#whats-next}

現在，您的團隊成員必須獲得執行個體的權限，因為管理Cloud Manager的權限是不夠的。 現在，您的雲資源已建立完畢且可供您的團隊存取，系統管理員必須從Admin Console將您的團隊成員指派給AEM作為Cloud Service產品設定檔。

>[!NOTE]
>若要以Cloud Service的身分授與AEM的存取權，使用者必須屬於「AEM使用者」或「AEM管理員」這兩個產品設定檔中的一個。 了解更多.

## 其他資源 {#additional-resources}

請依照其他資源了解：

* 程式類型和添加程式
* 環境類型和新增環境
* 管理Cloud Manager Git
* 將AEM的存取權設為來自Admin Console的Cloud Service
