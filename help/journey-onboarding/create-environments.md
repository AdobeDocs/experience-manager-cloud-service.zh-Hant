---
title: 建立環境
description: 瞭解如何使用Cloud Manager建立第一個環境。
role: Admin, User, Developer
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# 建立環境 {#create-environments}

在 [登機之旅，](overview.md) 您將學習如何使用Cloud Manager建立第一個環境。

## 目標 {#objective}

讀完這次登機旅程上的檔案， [建立程式，](create-program.md) 您現在擁有自己的Cloud Manager程式。 現在，您可以瞭解如何使用雲管理器為該程式建立第一個環境。

閱讀此文檔後，您將：

* 瞭解環境是什麼。
* 瞭解不同環境之間的差異。
* 能夠建立自己的環境。

## 什麼是環境？ {#environments}

環境位於雲管理器層次結構中的程式下方。 雖然程式允許您組織解決方案並授予對這些程式的特定團隊成員的訪問權限，但環境屬於特定程式，並且是這些程式中Adobe解決方案的個別實例。 環境用於特定目的，如創作內容或測試新開發。 Cloud Manager的CI/CD管道可方便從Git儲存庫將這些環境中的代碼部署。

如果你回想一下WKND旅遊和冒險企業理論的例子，它們可能有兩個項目：其WKND雜誌部的一個網站方案和WKND媒體部的一個資產方案。 每個程式可能都會有幾個環境，例如一個為站點的實際流量提供服務的生產環境和一個測試新應用程式碼的開發環境。

有三種不同的環境：

* **生產和階段**  — 生產環境和分段環境可作為一對使用，並分別用於生產和測試。
* **開發**  — 開發環境可以為開發和測試目的而建立，並且只能與非生產管道相關聯。

在登機旅程中，您將建立一個開發環境。

## 建立環境 {#creating-environments}

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織。

1. 按一下要為其添加環境的程式。

1. 從 **計畫概述** ，按一下 **添加環境** 的 **環境** 卡以添加環境。

   ![環境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * 的 **添加環境** 的上界 **環境** 頁籤。

      ![「環境」頁籤](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 的 **添加環境** 選項可能由於權限不足或取決於許可的資源而被禁用。

1. 在 **添加環境** 對話框。

   * 選擇 **環境類型**。
      * 可用/已用環境的數量顯示在「開發」環境類型後面的括弧中。
   * 提供 **環境名稱**。
   * 提供 **環境描述**。
   * 選擇 **雲區**。

   ![「添加環境」對話框](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 按一下 **保存** 添加指定的環境。

在環境可用後，您組織的成員將分配給 **開發人員** 產品配置檔案可以登錄到Cloud Manager並管理Cloud Manager git儲存庫。

## 下一步是什麼 {#whats-next}

既然您已閱讀了登機旅程的這一部分，您應：

* 瞭解環境是什麼。
* 瞭解不同環境之間的差異。
* 能夠建立自己的環境。

您的雲資源已建立，並且已準備好由您的團隊訪問。 作為系統管理員，您必須首先將團隊成員分配AEM到Adobe Admin Console的as a Cloud Service產品配置檔案，以便他們訪問這些資源。

因此，您應繼續登機旅程，下次查看文檔 [為as a Cloud Service產品配置AEM檔案分配團隊成員。](assign-profiles-aem.md)  在該文檔中，您將學習如何授予團隊成員訪問新環境所需的權限。

## 其他資源 {#additional-resources}

按照其他資源瞭解：

* [管理環境](/help/implementing/cloud-manager/manage-environments.md)  — 瞭解您可以建立的環境類型以及如何為Cloud Manager項目建立環境
* [使用Adobe雲管理器 — 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) - Cloud Manager環境由創作、發AEM布和調度程式服務組成。 瞭解不同的環境如何支援角色，以及如何使用不同的CI/CD管道參與。
