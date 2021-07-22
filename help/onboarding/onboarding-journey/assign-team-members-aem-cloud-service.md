---
title: '將團隊成員指派給AEM作為Cloud Service產品設定檔 '
description: 請參照本頁面，了解如何將團隊成員指派給AEM as a Cloud Service產品設定檔
hide: true
hidefromtoc: true
index: false
source-git-commit: 6046b29408a9bd61c8bbd809b73f2ba6e5a339da
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---


# 將團隊成員指派給AEM作為Cloud Service產品設定檔 {#assign-team-members-cloud-service}

## 目標 {#objective}

本檔案可協助您了解系統管理員必須執行哪些步驟，才能將您的團隊成員指派給AEM as a Cloud Service產品設定檔，以及為何讓AEM作者能夠透過AEM開始其歷程至關重要。

閱讀本小節後，您應：

* 了解為何及如何將團隊成員指派給AEM作為Cloud Service產品設定檔
* 了解如何將團隊成員新增至AEM User產品設定檔
* 了解如何將團隊成員新增至AEM管理員產品設定檔


## 簡介 {#introduction}

若要以Cloud Service的身分授予AEM的存取權，使用者必須屬於「AEM使用者」或「AEM管理員」這兩個產品設定檔之一。 您的團隊成員必須獲得AEM例項的權限，因為管理Cloud Manager的權限不足。 了解更多.

>[!NOTE]
>系統管理員指派給AEM User產品設定檔的每位使用者都擁有（唯讀）Cloud Manager的存取權。

## 先決條件 {#prerequisites}

* 了解AEM作為Cloud Service產品設定檔
* 熟悉Admin Console
* Cloud Manager產品設定檔已視情況指派給您的團隊成員，且雲端資源已設定
* 有關您的團隊成員的詳細資訊：系統管理員必須擁有需要以Cloud Service方式存取AEM的團隊成員的姓名和電子郵件地址，以及角色和責任。 為了上線，建議您先新增將參與即時工作的使用者，例如管理員、開發人員和內容作者。 您可以繼續上線的其餘部分，而不需新增所有使用者。 上線完成後，您稍後可以擴充至更多使用者。


1. 登入Admin Console
（與之前相同）

1. 檢閱AEM as a Cloud Service產品設定檔
從Admin Console中，您可以看到Cloud Manager設定檔清單。 要執行此操作：

1. 登入Adobe Admin Console後，請從「產品與服務」卡片中選取「Adobe Experience Manager as a Cloud Service」 :

1. 導覽並選取例項（開發環境的製作例項），如下圖所示。



   現在，您將能夠看到AEM的清單，它是Cloud Service產品設定檔，需要根據使用者的角色指派給使用者。 若要深入了解，請前往AEM as a Cloud Service產品設定檔。




## 將團隊成員新增至AEM使用者或AEM管理員產品設定檔 {#add-team-members}

若要授與AEMaaCS例項使用者的存取權，使用者必須屬於「AEM使用者」或「AEM管理員」這兩個產品設定檔之一。

>[!NOTE]
>您必須獲得執行個體的權限，但管理Cloud Manager的權限不足。 了解更多.

下列步驟必須由同時處於業務所有者角色的系統管理員執行。

1. 從Cloud Manager，導覽至Cloud Manager，並從感興趣的環境內容中選取管理存取按鈕，如下所示：

1. 按一下「管理存取」後，新的索引標籤會導覽至您可存取環境製作例項的Admin Console。 根據此個人需要授予的權限，選取「AEM管理員」或「AEM使用者」。 進一步了解AEM as a Cloud Service產品設定檔。

1. 選擇添加用戶（如下所示），並提交完成添加團隊成員所需的詳細資訊：


1. 如果您有需要存取權之團隊成員的資訊，您將想對所有環境（包括開發、預備和生產）重複執行這些步驟。

   您新增的使用者現在可以存取AEM作為Cloud Service作者服務！


## 下一步 {#whats-next}

您指派給AEMaaCS產品設定檔的使用者現在已準備好學習如何存取「作者」，以及熟悉AEM as aCloud Service中的編寫頁面。 了解更多.

## 其他資源 {#additional-resources}

設定AEM的存取權（影片逐步說明）
製作頁面的快速入門手冊
