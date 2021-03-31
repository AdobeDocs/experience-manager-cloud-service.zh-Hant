---
title: '系統管理員任務 '
description: 請依照本頁瞭解如何新增使用者，並將他們指派為系統管理員的Cloud Manager角色
translation-type: tm+mt
source-git-commit: f1f5766a41763634e0aaba44e55471ac2ea5dc8f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 系統管理員任務{#add-users-assign}

系統管理員管理其使用者的所有方面，從存取到權限。 此使用者是第一個可以開始在Admin Console和雲端管理員中執行工作的使用者。
系統管理員執行下列組織任務：

* 新增使用者
* 指派使用者至Cloud Manager角色和權限

## 添加用戶{#add-users}

>[!NOTE]
>您必須是系統管理員才能新增使用者。

1. 如果您是系統管理員，請導航至[Admin Console](https://adminconsole.adobe.com)。 或者，您也可以導覽至Cloud Manager，您會看到&#x200B;**管理存取**&#x200B;按鈕，如下所述。

1. 按一下位於Cloud Manager登陸頁面右上方的&#x200B;**管理存取**&#x200B;按鈕，在新標籤中開啟Admin Console。

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

   在&#x200B;**Admin Console**&#x200B;中，您可以將用戶添加到Cloud Manager中，並將其分配給角色，即Admin Console中的產品配置檔案。

1. 從&#x200B;**產品與服務**&#x200B;卡中選擇&#x200B;**Adobe Experience Manager作為Cloud Service**，如下所示。

   ![](/help/onboarding/what-is-required/assets/admin-console-1.png)

1. 從操作欄中選擇&#x200B;**Users**&#x200B;頁籤，然後選擇&#x200B;**Add User**。

   ![](/help/onboarding/what-is-required/assets/admin-console-2.png)

1. 選擇用戶並為用戶分配適當的Cloud Manager角色或產品配置檔案，如下所示。

   ![](/help/onboarding/what-is-required/assets/admin-console-3.png)

   >[!NOTE]
   >請參閱以上各節[「用戶角色和權限」](#user-roles)和[與「角色定義」相關的「權限」](#permissions)，以確保在&#x200B;**Admin Console**&#x200B;中為正確的用戶分配了正確的角色。

   現在，您已將使用者新增至Adobe Experience Manager做為Cloud Service產品內容，並設定了正確的角色或產品設定檔。

   例如，如果您是：

   * ***Business Owner***，則您擁有「新增程式」或「編輯程式」、新增或更新環境、新增／編輯／刪除管道並執行任何管道，以及將程式碼部署至環境或程AEM式碼品質的權限。

   * ***Deployment Manager***，則您有權添加或更新環境、運行任何管線，以及將代碼部署到環AEM境或代碼質量。

   * ***開發人員***，您擁有產生個人存取Token以存取Git的權限。

      >[!NOTE]
      > 用戶可以被指派給多個角色。 例如，將「業務所有者」和「部署管理員」角色分配給用戶時，會為用戶提供這些權限的組合或總和。
