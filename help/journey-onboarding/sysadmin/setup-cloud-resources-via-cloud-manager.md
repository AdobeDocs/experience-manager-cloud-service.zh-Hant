---
title: 通過雲管理器設定雲資源
description: 瞭解如何使用雲管理器來設定和管理您自己的雲資源。
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 0db24518610fccf0d2ea5e0620a0c6a5f8009ea8
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---

# 通過雲管理器設定雲資源 {#setup-cloud-resources}

瞭解如何使用雲管理器來設定和管理您自己的雲資源。

## 目標 {#objective}

此文檔可幫助您瞭解雲資源的建立方式以及建立者。 讀完本節後，您應瞭解：

* 分配給 **業務所有者** 角色必須是組織中第一個登錄並訪問雲管理器的角色。
* 如何建立雲程式和環境。

## 簡介 {#introduction}

添加雲資源由分配給 **業務所有者** 產品配置檔案。 此人通常是瞭解業務需求並完成初始雲管理器安裝的人員。

請按照以下部分瞭解如何建立 [雲服務程式](#create-cloud-service-program) 和 [環境。](#create-cloud-environments)

### 必備條件 {#prerequisites}

* 分配給 **業務所有者** 角色必須先登錄到Cloud Manager，然後才能使用 **業務所有者** 角色嘗試訪問雲管理器以執行和本文檔中描述的步驟。

   * 返回到 [將團隊成員分配給Cloud Manager產品配置檔案](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) 詳細資訊。

* 你必須明白 [導航並登錄到Cloud Manager。](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* 你應該熟悉 [Cloud Manager產品配置檔案。](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* 您應該瞭解雲管理器的概念 [方案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 和 [環境。](/help/implementing/cloud-manager/manage-environments.md)

## 以系統管理員和業務所有者身份訪問雲管理器 {#access-sysadmin-bo}

在您分配給 **業務所有者** 角色可以訪問雲管理器並開始建立雲資源，必須為系統管理員分配 **業務所有者** 角色並登錄到雲管理器。

1. 確保作為系統管理員，您 **業務所有者** 已分配角色。

   * 回到前一步， [將團隊成員分配給Cloud Manager產品配置檔案，](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) 的子菜單。 **業務所有者** 角色。

1. 登錄Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並顯示正常登錄頁。

通過以系統管理員身份成功登錄 **業務所有者** 角色，初始化雲管理器，供其他用戶使用 **業務所有者** 角色。 您不會收到此消息或任何消息的確認。 只需登錄即可。

直到您以系統管理員身份登錄Cloud Manager, **業務所有者** 角色，其他用戶 **業務所有者** 角色將無法在雲管理器中建立程式，即使它們被分配了正確的角色。

## 導航到雲管理器 {#navigate-cloud-manager}

具有 **業務所有者** 角色將收到一封歡迎電子郵件，其中包含要開始的連結。 按照以下步驟使用此歡迎電子郵件導航到Cloud Manager。

1. 從歡迎電子郵件中按一下 **開始**，如下圖所示。
   ![電子郵件示例](/help/journey-onboarding/assets/get-started-email.png)

1. 您將導航至Cloud Manager **計畫和產品** 的子菜單。

   >[!TIP]
   >
   >您還可以直接從Cloud Manager的登錄頁導航 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)。 請將此頁面加入書籤以供將來參考。

1. 您將被定向到Cloud Manager的登錄頁。 請參閱 [查看雲管理器的程式](#viewing-programs) 的子菜單。

您還可以導航至Cloud Manager的 **計畫和產品** 按照以下步驟從Adobe Experience Cloud首頁頁面

1. 直接導航到 [Adobe Experience Cloud](https://experience.adobe.com) 用你的Adobe ID登錄。

1. 從Adobe Experience Cloud首頁，選擇 **Experience Manager**。

   ![Experience Cloud首頁](/help/journey-onboarding/assets/setup-resources2.png)

1. 這會帶你到主AEM頁。 從此處，按一下 **啟動** 的 **雲管理器** 平鋪。

   ![AEM首頁](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登錄後，您將被定向到Cloud Manager的登錄頁。 請參閱 [查看雲管理器的程式](#viewing-programs) 的子菜單。

您如何通過雲管理器訪問您的程式和產品取決於您自己，對您如何使用雲管理器或如何管理程式沒有影響。

>[!NOTE]
>
>根據在中分配的角色 [!UICONTROL 雲管理器] 以及應用程式的狀態，在使用 [!UICONTROL 雲管理器] UI。

### 查看程式 {#viewing-programs}

成功訪問雲管理器後，您所看到的內容將取決於您程式的狀態，如以下各節中所詳述。

#### 當不存在程式時 {#no-programs}

如果組織中不存在程式，則登錄頁會指導您建立第一個程式。

![無程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### 當程式已存在時 {#programs-exist}

如果您的組織中已存在程式，則登錄頁將顯示您的現有程式，並提供一個按鈕以添加其他程式。

![程式存在](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### 當程式存在且您是系統管理員時 {#programs-exist-sysadmin}

如果您的組織中已存在程式，並且您是系統管理員，則將顯示登錄頁 **管理訪問** 按鈕 **添加程式** 的雙曲餘切值。

![系統管理員視圖](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## 驗證用戶角色 {#verify-user-roles}

成功登錄雲管理器後，您可以驗證是否已為您分配了 **業務所有者** 產品配置檔案。

1. 從窗口的右上角選擇您的配置檔案。

   ![使用者設定檔](/help/journey-onboarding/assets/setup-resources5.png)

1. 選擇 **用戶角色** 顯示分配給用戶的角色。

   ![用戶角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 確認您的用戶 **業務所有者** 角色。

   ![用戶角色清單](/help/journey-onboarding/assets/setup-resources7.png)

您已以業務所有者身份成功登錄到雲管理器！ 如果未分配 **業務所有者** 角色，請與系統管理員聯繫。

## 建立Cloud Service程式 {#create-cloud-service-program}

既然您已確保您擁有適當的訪問權限，您就可以建立第一個程式。

1. 導航至Cloud Manager登錄頁，地址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 然後登錄。

1. 在Cloud Manager登錄頁上，按一下 **添加程式** 啟動「添加程式」嚮導。

   ![登陸頁面](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >有關如何使用「添加程式」嚮導的逐步說明，請參閱文檔 [建立生產程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) 看這個 [視頻](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) 瞭解如何將您建立AEM為雲程式，並在建立程式之前瞭解重要注意事項。


1. 成功建立雲程式後，您可以從Cloud Manager登錄頁導航到您的程式，以查看 **概述** 頁。

   ![計畫概述](/help/journey-onboarding/assets/setup-resources8.png)

1. 分配給開發人員產品配置檔案的成員可以登錄到Cloud Manager並管理Cloud Manager Git儲存庫。

   * 如果尚未這樣做，現在是將成員分配給 **開發人員** 在雲管理器團隊中的角色。 返回到 [將團隊成員分配給Cloud Manager產品配置檔案](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) 詳細資訊。

現在，您的程式已成功建立，並且您的Cloud Manager Git儲存庫可供開發人員訪問！

## 建立雲環境 {#create-cloud-environments}

成功建立雲程式後，請建立雲環境。

1. 導航至Cloud Manager登錄頁，地址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 選擇 **添加** 從環境卡上。

   ![「添加環境」按鈕](/help/journey-onboarding/assets/setup-resources9.png)

1. 添加環境嚮導將啟動並引導您完成添加環境的過程。 首先添加開發環境以熟悉嚮導。

   >[!TIP]
   >
   >請參閱文檔 [添加環境](/help/implementing/cloud-manager/manage-environments.md#adding-environments) 瞭解更多資訊或觀看 [本快速視頻教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) 瞭解Cloud Manager環境以及如何將其添加到程式。

1. 分配給 **開發人員** 產品配置檔案可以登錄到Cloud Manager並管理Cloud Manager git儲存庫。

現在，您的程式已成功建立，並且您的Cloud Manager Git可供開發人員訪問！

## 下一步是什麼 {#whats-next}

既然您的雲資源已經建立並準備好由您的團隊訪問，系統管理員必須將您的團隊成員分配給Adobe Admin Console的AEMas a Cloud Service產品配置檔案，以便訪問這些資源。

您應通過下次查看文檔來繼續登機旅程 [為as a Cloud Service產品配置AEM檔案分配團隊成員](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md) 您將在其中學習如何授予團隊成員訪問新環境所需的權限。

## 其他資源 {#additional-resources}

按照其他資源瞭解：

* [程式類型和添加程式](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [環境類型和添加環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [管理雲管理器Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [配置對AEMas a Cloud Service的訪問](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
