---
title: 建立環境
description: 了解如何使用Cloud Manager建立您的第一個環境。
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# 建立環境 {#create-environments}

在 [入門旅程，](overview.md) 您將學習如何使用Cloud Manager建立您的第一個環境。

## 目標 {#objective}

閱讀入門歷程的上一份檔案後， [建立方案，](create-program.md) 您現在擁有自己的Cloud Manager計畫。 現在，您可以了解如何使用Cloud Manager為該計畫建立第一個環境。

閱讀本檔案後，您將：

* 了解環境是什麼。
* 了解不同環境之間的差異。
* 能夠建立您自己的環境。

## 什麼是環境？ {#environments}

環境位於Cloud Manager階層中的程式下方。 雖然方案可讓您組織解決方案，並授予特定團隊成員對這些方案的存取權，但環境屬於特定方案，且是這些方案中Adobe解決方案的個別例項。 環境會用於特定用途，例如製作內容或測試新開發。 Cloud Manager的CI/CD管道可協助從Git存放庫將程式碼部署至這些環境。

如果您回想一下WKND Travel and Adventure Enterprises（WKND Travel and Adventure Enterprises，該企業是專注於旅遊相關媒體的租戶）的理論範例，他們可能會有兩個計畫：WKND雜誌部的一個網站項目和WKND媒體部的一個資產項目。 每個程式可能會有兩個環境，例如一個生產環境（可提供網站的實際流量）和一個開發環境（可測試新應用程式程式碼）。

環境有三種類型：

* **生產與預備**  — 生產和測試環境可分別以對的形式提供，並用於生產和測試用途。
* **開發**  — 可建立開發環境以供開發及測試之用，且僅能與非生產管道相關聯。

為了進行此入門歷程，您將建立開發環境。

## 建立環境 {#creating-environments}

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 按一下要為其添加環境的程式。

1. 從 **計畫概述** 頁面，按一下 **新增環境** 在 **環境** 卡片來新增環境。

   ![環境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * 此 **新增環境** 選項 **環境** 標籤。

      ![環境標籤](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 此 **新增環境** 選項可能會因為缺少權限或取決於授權資源而停用。

1. 在 **新增環境** 對話方塊中顯示：

   * 選取 **環境類型**.
      * 可用/使用的環境數量會以括弧顯示在「開發」環境類型後面。
   * 提供 **環境名稱**.
   * 提供 **環境說明**.
   * 選取 **雲區域**.

   ![「添加環境」對話框](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 按一下 **儲存** 添加指定環境。

環境可用後，組織的成員即會指派給 **開發人員** 產品設定檔可登入Cloud Manager並管理Cloud Manager git存放庫。

## 下一步 {#whats-next}

您已閱讀入門歷程的這一部分，您應：

* 了解環境是什麼。
* 了解不同環境之間的差異。
* 能夠建立您自己的環境。

您的雲資源已建立，且可供您的團隊存取。 身為系統管理員，您必須先將團隊成員指派給Adobe Admin Console中的AEMas a Cloud Service產品設定檔，才能讓他們存取這些資源。

因此，您應繼續進行上線歷程，繼續檢閱此檔案 [指派團隊成員給AEMas a Cloud Service產品設定檔。](assign-profiles-aem.md)  在該文檔中，您將學習如何授予團隊成員訪問新環境所需的權限。

## 其他資源 {#additional-resources}

請依照其他資源了解：

* [管理環境](/help/implementing/cloud-manager/manage-environments.md)  — 了解您可建立的環境類型，以及如何為Cloud Manager專案建立環境
* [使用AdobeCloud Manager — 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) - Cloud Manager環境由AEM製作、發佈和Dispatcher服務組成。 了解不同環境如何支援角色，以及如何使用不同的CI/CD管道參與。
