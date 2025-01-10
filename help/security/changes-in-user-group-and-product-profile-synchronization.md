---
title: 同步處理使用者群組和產品設定檔的變更
description: 瞭解AEM as a Cloud Service即將推出的使用者群組和產品設定檔同步作業中的變更
feature: Security
role: Admin
hide: true
hidefromtoc: true
source-git-commit: 32ce30ce136a714e277e00197d38ea380c777377
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# 同步處理使用者群組和產品設定檔的變更 {#changes-in-user-group-and-product-profile-synchronization}

每當使用者登入AEM as a Cloud Service或使用存取權杖時，Adobe Admin Console使用者群組、產品設定檔和產品設定檔服務都會以群組的形式同步至AEM存放庫。

在1月28日，為了降低UI雜湊並最佳化效能，同步行為將會有一些變更，導致在AEM中出現的群組減少。 將移除兩種AEM群組：

1. 尾碼為`GROUP_NAME_SUFFIX`的AEM群組。 這些群組未出現在Adobe Developer Console中，但出現在「AEM群組管理」畫面中，如下所示。 若您的AEM應用程式參考這些群組（可能性很低），請務必參考不含該尾碼的Adobe Admin Console使用者群組。

   ![已移除群組1](/help/security/assets/removed-groups-1.png)

1. 與特定環境無關的Adobe Admin Console產品設定檔相關聯的AEM群組。 這可能包括下列產品設定檔：

   * 與其他Adobe產品相關
   * 和其他AEM程式相關
   * 和同一AEM計畫中的其他AEM環境相關
   * 與Cloud Manager相關（例如，`Business Owner - Cloud Service`）

   例如，在下圖中，有許多列具有模式`AEM Administrators-<suffix>`或`AEM Users-<suffix>`，其尾碼與目前環境無關。

   ![已移除群組2](/help/security/assets/removed-groups-2.png)

您可以在Cloud Manager中環境的動作選單中選取管理&#x200B;**存取 — 作者設定檔** (或&#x200B;**Publish設定檔**)，以檢查哪個尾碼與目前環境相關。

![檢查尾碼](/help/security/assets/suffix-check.png)

這將導覽至Adobe Admin Console，如下方熒幕擷圖所示。 請注意，`<suffix>`可能是隨機字元集或層級，以及程式和環境ID （例如`author - Program 12345 - Environment 45678`）。

Admin Console](/help/security/assets/admin-console-profile-suffixes.png)中的![尾碼

在罕見的情況下，您的AEM應用程式會參照將不再出現在AEM中的群組，請務必改用i)來自正確AEM例項的產品設定檔或ii) Adobe Admin Console使用者群組。
