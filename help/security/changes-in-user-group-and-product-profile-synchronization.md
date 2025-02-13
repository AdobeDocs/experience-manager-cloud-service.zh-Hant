---
title: 使用者群組和產品設定檔同步的變更
description: 了解 AEM as a Cloud Service 使用者群組和產品設定檔同步的變更
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: 5c103fcce1ae47bc89f4f572d89967c62c1f7603
workflow-type: ht
source-wordcount: '385'
ht-degree: 100%

---

# 使用者群組和產品設定檔同步的變更 {#changes-in-user-group-and-product-profile-synchronization}

每當使用者登入 AEM as a Cloud Service 或有人使用存取權杖時，Adobe Admin Console 使用者群組、產品設定檔和產品設定檔服務都會以群組的形式同步到 AEM 存放庫。

從 AEM 維護版本 19149 開始，群組同步行為有所變更，以減少使用者介面混亂並將效能最佳化。具體來說，以下兩類 AEM 群組的使用者群組成員資格將不再同步：

1. 字尾是 `GROUP_NAME_SUFFIX` 的 AEM 群組。這些群組並未顯示在 Adobe Developer Console，但是顯示在 AEM 群組管理畫面，如下所示。萬一您的 AEM 應用程式參考這些群組，請務必參考未使用該字尾的 Adobe Admin Console 使用者群組。

   ![已移除的群組 1](/help/security/assets/removed-groups-1.png)

1. 與 Adobe Admin Console 產品設定檔相關的 AEM 群組與特定環境無關。可能包括以下產品設定檔：

   * 與其他 Adobe 產品相關
   * 與其他 AEM 計畫相關
   * 與同一 AEM 計畫中的其他 AEM 環境相關
   * 與 Cloud Manager 相關 (例如 `Business Owner - Cloud Service`)

   例如，在下圖中，有許多列採用 `AEM Administrators-<suffix>` 或 `AEM Users-<suffix>` 的樣式，其字尾與目前環境無關。

   ![已移除的群組 2](/help/security/assets/removed-groups-2.png)

您可以在 Cloud Manager 環境的動作選單中選取「管理&#x200B;**存取 - 作者設定檔**」(或「**發佈設定檔**」)，檢查哪個字尾與目前環境相關。

![檢查字尾](/help/security/assets/suffix-check.png)

這將導覽至 Adobe Admin Console，如以下螢幕擷圖所示。請注意，`<suffix>` 可能是隨機字元集或層、程式和環境 ID (例如 `author - Program 12345 - Environment 45678`)。

![ Admin Console 中的字尾](/help/security/assets/admin-console-profile-suffixes.png)

萬一您的 AEM 應用程式參考的群組在 AEM 中不會再顯示，請務必改用 i) 來自正確的 AEM 執行個體的產品設定檔，或 ii) Adobe Admin Console 使用者群組。

當使用者登入環境時，其群組成員資格會進行同步，而且會把使用者移出與目前環境無關的群組。這些群組本身仍然存在，且包括自該功能啟用後尚未登入的使用者。
