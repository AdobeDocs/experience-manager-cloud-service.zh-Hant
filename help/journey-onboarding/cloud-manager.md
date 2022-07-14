---
title: 訪問雲管理器
description: 瞭解如何訪問雲管理器，以便設定項目資源。
role: Admin, User, Developer
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---


# 訪問雲管理器 {#cloud-resources}

在 [登機之旅，](overview.md) 您將學習如何訪問雲管理器，以便設定項目資源。

## 目標 {#objective}

在上篇登機旅程中， [為Cloud Manager產品配置檔案分配團隊成員，](assign-profiles-cloud-manager.md) 您授予了您的AEMaaCS團隊適當的角色。 現在，瞭解如何訪問雲管理器，以便您可以設定您的團隊將使用的項目資源。

由於您完成了此過程中的上一步，因此您的團隊可以訪問雲管理器。 雲管理器用於建立和管理您的項目資源，如程式和環境。

閱讀完此文檔後，您應該瞭解：

* 系統管理員分配給 **業務所有者** 角色必須是組織中第一個登錄並訪問雲管理器的角色。
* 如何登錄雲管理器。

## Cloud Manager {#cloud-manager}

雲管理器是as a Cloud Service的AEM重要元件，是您團隊的單一入口點。 它通過專門構建的CI/CD管道支援具有企業開發機構的客戶，這些管道可確保徹底的測試和最高的代碼質量，以提供卓越的體驗。 Cloud Manager以自助方式提供啟動所需的一切，包括建立雲資源和環境的能力。

通常指派給 **業務所有者** 產品配置檔案負責添加雲資源，如程式和環境。 此人瞭解業務需要以及完成初始雲管理器安裝的人員。

在登機旅程中，作為系統管理員，您已將自己分配給 **業務所有者** 產品配置檔案，並將設定雲資源。 根據實際項目要求，業務所有者可能與系統管理員相同，也可能不相同。

## 以系統管理員和業務所有者身份訪問雲管理器 {#access-sysadmin-bo}

在您分配給 **業務所有者** 角色可以訪問雲管理器並開始建立雲資源，必須為系統管理員分配 **業務所有者** 角色並登錄到雲管理器，就像您在登機過程中執行的上一步操作一樣。

1. 確保作為系統管理員，您 **業務所有者** 已分配角色。

   * 回到前一步， [將團隊成員分配給Cloud Manager產品配置檔案，](assign-profiles-cloud-manager.md) 的子菜單。 **業務所有者** 角色。

1. 登錄Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並顯示正常登錄頁。

通過以系統管理員身份登錄， **業務所有者** 角色，初始化雲管理器，供其他用戶使用 **業務所有者** 角色。 您不會收到此消息或任何消息的確認。 只需登錄即可。

直到您以系統管理員身份登錄到Cloud Manager **業務所有者** 角色，其他用戶 **業務所有者** 角色將無法在雲管理器中建立程式，即使它們被分配了正確的角色。

## 導航到雲管理器 {#navigate-cloud-manager}

具有 **業務所有者** 角色將收到一封歡迎電子郵件，其中包含要開始的連結。 按照以下步驟使用此歡迎電子郵件導航到Cloud Manager。

1. 從歡迎電子郵件中按一下 **開始**，如下圖所示。
   ![電子郵件示例](/help/journey-onboarding/assets/get-started-email.png)

1. 您將導航至Cloud Manager **計畫和產品** 的子菜單。

   >[!TIP]
   >
   >您還可以直接從Cloud Manager的登錄頁導航 `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`。 請將此頁面加入書籤以供將來參考。

1. 您將被定向到Cloud Manager的登錄頁。

或者，您也可以導航至Cloud Manager **計畫和產品** 按照以下步驟從Adobe Experience Cloud首頁頁面

1. 直接導航到 [Adobe Experience Cloud](https://experience.adobe.com) 用你的Adobe ID登錄。

1. 從Adobe Experience Cloud首頁，選擇 **Experience Manager**。

   ![Experience Cloud首頁](/help/journey-onboarding/assets/setup-resources2.png)

1. 這會帶你到主AEM頁。 從此處，按一下 **啟動** 的 **雲管理器** 平鋪。

   ![AEM首頁](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登錄後，您將被定向到Cloud Manager的登錄頁。 請參閱 [查看雲管理器的程式](#viewing-programs) 的子菜單。

您如何通過雲管理器訪問您的程式和產品取決於您自己，對您如何使用雲管理器或如何管理程式沒有影響。

>[!NOTE]
>
>根據在雲管理器中分配的角色和應用程式的狀態，在使用雲管理器UI時，您將看到不同的螢幕。

## 查看程式 {#viewing-programs}

成功訪問雲管理器後，您所看到的內容將取決於您程式的狀態，如以下各節中所詳述。

### 當不存在程式時 {#no-programs}

如果組織中不存在程式，則登錄頁會指導您建立第一個程式。

![無程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### 當程式已存在時 {#programs-exist}

如果您的組織中已存在程式，則登錄頁將顯示您的現有程式，並提供一個按鈕以添加其他程式。

![程式存在](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### 當程式存在且您是系統管理員時 {#programs-exist-sysadmin}

如果您的組織中已存在程式，並且您是系統管理員，則將顯示登錄頁 **管理訪問** 按鈕 **添加程式** 的雙曲餘切值。

![系統管理員視圖](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## 驗證用戶角色 {#verify-user-roles}

成功登錄雲管理器後，您可以驗證是否已為您分配了 **業務所有者** 產品配置檔案。

1. 從窗口的右上角選擇您的配置檔案。

   ![使用者設定檔](/help/journey-onboarding/assets/setup-resources5.png)

1. 選擇 **用戶角色** 顯示分配給用戶的角色。

   ![用戶角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 該對話框應確認您的用戶 **業務所有者** 角色。

   ![用戶角色清單](/help/journey-onboarding/assets/setup-resources7.png)

您已以業務所有者身份成功登錄到雲管理器！ 如果未分配 **業務所有者** 角色，請與系統管理員聯繫。

## 下一步是什麼 {#whats-next}

現在，您可以以系統管理員身份訪問雲管理器，您已準備好建立第一個程式。

您應通過下次查看文檔來繼續登機旅程 [建立程式](create-program.md) 你將在哪裡學習如何做。

## 其他資源 {#additional-resources}

按照其他資源瞭解：

* [雲管理器簡介](/help/onboarding/cloud-manager-introduction.md)  — 瞭解Cloud Manager、Cloud Manager程式和環境。
