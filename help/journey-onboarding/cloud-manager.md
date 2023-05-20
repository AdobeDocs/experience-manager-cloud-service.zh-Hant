---
title: 存取 Cloud Manager
description: 了解如何存取 Cloud Manager，以便您可以設定專案資源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 5c9dbaa25f0142afdae8b09dc18d1e1aaaf4c1fb
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 52%

---

# 存取 Cloud Manager {#cloud-resources}

在 [登機之旅，](overview.md) 您將學習如何訪問雲管理器，以便設定項目資源。

## 目標 {#objective}

在這次上線之旅的上一篇文章中，[將團隊成員指派給 Cloud Manager 產品設定檔，](assign-profiles-cloud-manager.md)您授予您的 AEMaaCS 團隊適當的角色。現在，瞭解如何訪問雲管理器，以便您可以設定團隊使用的項目資源。

由於您完成了此歷程的上一步，您的團隊可以存取 Cloud Manager。Cloud Manager 用於建立和管理您的專案資源，例如程序和環境。

閱讀此文檔後，您應瞭解以下內容：

* 系統管理員分配給 **業務所有者** 角色必須是組織中第一個登錄並訪問雲管理器的角色。
* 如何登入 Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要元件，可作為您團隊的單一入口點。透過其專門建構的 CI/CD 管道支援具有企業開發設定的客戶，這些管道可確保進行徹底的測試和最高的程式碼品質，以提供卓越的體驗。Cloud Manager 提供以自助方式開始所需的一切，包括建立雲端資源和環境的能力。

通常是指派給&#x200B;**業主**&#x200B;產品設定檔負責新增您的雲端資源，例如程序和環境。此人了解業務需求以及完成初始 Cloud Manager 設定的人員。

在登機旅程中，作為系統管理員，您已將自己分配給 **業務所有者** 產品配置檔案，並可設定雲資源。 根據實際項目要求，業務所有者可能與系統管理員相同，也可能不相同。

## Access Cloud Manager 可作為系統管理員和業主 {#access-sysadmin-bo}

在您分配給 **業務所有者** 角色可以訪問雲管理器並開始建立雲資源，必須為系統管理員分配 **業務所有者** 角色。 他們還必須像您在登機過程中的上一步驟一樣登錄雲管理器。

1. 確保您作為系統管理員擁有&#x200B;**業主**&#x200B;指派的角色。

   * 回到前一步， [將團隊成員分配給Cloud Manager產品配置檔案，](assign-profiles-cloud-manager.md) 的子菜單。 **業務所有者** 角色。

1. 登入 Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)並顯示正常的登陸頁面。

透過以系統管理員身份成功登入&#x200B;**業主**&#x200B;角色，您初始化 Cloud Manager 以供其他使用者使用&#x200B;**業主**&#x200B;角色。您沒有收到確認或任何消息。 僅僅登錄就足夠了。

直到您以系統管理員身份登錄到Cloud Manager **業務所有者** 角色，其他用戶 **業務所有者** 角色無法在雲管理器中建立程式。 即使為這些規則分配了正確的角色，該規則也是正確的。

## 瀏覽至 Cloud Manager {#navigate-cloud-manager}

具有 **業務所有者** 角色接收一封歡迎電子郵件，其中包含要開始的連結。 按照以下步驟使用此歡迎電子郵件瀏覽到 Cloud Manager。

1. 在歡迎電子郵件中，按一下 **開始**，如下圖所示。
   ![電子郵件範例](/help/journey-onboarding/assets/get-started-email.png)

1. 導航至Cloud Manager **計畫和產品** 的子菜單。

   >[!TIP]
   >
   >您也可以從以下位置直接瀏覽到 Cloud Manager 的登入頁面`[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`。將此頁面加書籤以供將來參考。

1. 您將被定向到Cloud Manager的登錄頁。

您還可以按照以下步驟從 Adobe Experience Cloud 主頁瀏覽到 Cloud Manager 的&#x200B;**程序和產品**&#x200B;頁面。

1. 直接瀏覽至的 [Adobe Experience Cloud](https://experience.adobe.com) 並使用您的 Adobe ID 憑證登入。

1. 在Adobe Experience Cloud首頁中，選擇 **Experience Manager** 開啟主AEM頁。

   ![Experience Cloud 首頁](/help/journey-onboarding/assets/setup-resources2.png)

1. 在 **雲管理器** 拼貼，選擇 **啟動**。

   ![AEM 首頁](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登錄後，您將被定向到Cloud Manager登錄頁。 請參閱 [查看雲管理器的程式](#viewing-programs) 的子菜單。

您如何透過 Cloud Manager 存取您的程序和產品取決於您，並且不會影響您如何使用 Cloud Manager 或您如何管理您的程序。

>[!NOTE]
>
>根據在Cloud Manager中分配的角色和應用程式的狀態，在使用Cloud Manager用戶介面時，您會看到不同的螢幕。

## 檢視程序 {#viewing-programs}

成功訪問雲管理器後，您所看到的內容取決於您程式的狀態，如以下各節中所詳述。

### 不存在程序時 {#no-programs}

如果您的組織中不存在任何程序，那麼您的登入頁面會指導您建立您的第一個程序。

![無程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### 已存在程序時 {#programs-exist}

如果您的組織中存在程式，則登錄頁將顯示您的現有程式，並提供一個按鈕以添加其他程式。

![存在程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### 當程序存在並且您是系統管理員時 {#programs-exist-sysadmin}

如果您的組織中存在程式並且您是系統管理員，則將顯示登錄頁 **管理訪問** 按鈕 **添加程式** 的雙曲餘切值。

![系統管理員檢視](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## 使用者驗證您的使用者角色 {#verify-user-roles}

成功登入 Cloud Manager 後，您可以驗證您是否已被指派&#x200B;**業主**&#x200B;產品簡介。

1. 從窗口的右上角選擇您的個人資料。

   ![使用者設定檔](/help/journey-onboarding/assets/setup-resources5.png)

1. 要顯示分配給用戶的角色，請選擇 **用戶角色**。

   ![使用者角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 該對話框應確認您的使用者擁有&#x200B;**業主**&#x200B;角色。

   ![使用者角色清單](/help/journey-onboarding/assets/setup-resources7.png)

您已成功以業主身份登入 Cloud Manager！如果您未指派&#x200B;**業主**&#x200B;角色，請聯絡您的系統管理員。

## 下一步 {#whats-next}

現在您可以作為系統管理員存取 Cloud Manager，您可以建立您的第一個程序了。

繼續登機旅程，繼續查看文檔 [建立程式](create-program.md) 你在那裡學會如何做。

## 其他資源 {#additional-resources}

如果您想超越登機旅程的內容，請選擇以下附加資源。

* [Cloud Manager 簡介](/help/onboarding/cloud-manager-introduction.md) - 了解 Cloud Manager、Cloud Manager 程序和環境。
* [AEM as a Cloud Service 團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md) - 了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授與和限制您的授權 Adobe 解決方案的存取權。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
