---
title: 移轉關閉的使用者群組
description: 瞭解將內容移轉至Adobe Experience Manager as a Cloud Service後啟用封閉使用者群組所需的特殊考量事項。
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
source-git-commit: 29ffb48d23b4a2fe4973b005c98c5720b4196367
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 10%

---

# 移轉關閉的使用者群組 {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="封閉使用者群組移轉"
>abstract="封閉使用者群組 (CUG) 的移轉目前需要執行一些檢查和步驟，以便在移轉後正常運作。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=zh-Hant" text="AEM 中的封閉使用者群組"

目前，封閉使用者群組(CUG)需要一些額外的步驟，才能在移轉的目標環境中正常運作。 本檔案將說明相關情境，以及要求他們以預期方式保護節點所需的步驟。

## 群組移轉

如果主體（包括群組）透過該內容的ACL與移轉的內容相關聯，則會自動納入到Adobe Experience Manager as a Cloud Service的移轉中，如果在該內容的CUG原則中參考主體（包括群組）。

## 移轉中的封閉式使用者群組

驗證群組及其成員是否存在，應在上線前完成。 透過「內嵌工作」檢視下載的「主體報表」可用來檢視相關群組是否包含，或因不在ACL或CUG原則中而不包含。

接下來，必須觸發程式，且必須設定屬性以啟用CUG。 為此，請重新發佈與CUG原則相關的所有頁面。 這樣會校準Publish執行個體以追蹤原則。

這樣會啟用「發佈」上的CUG原則，而且只有屬於與原則相關群組成員的已驗證使用者才能存取內容。

## 摘要

總而言之，以下是移轉後啟用CUG的步驟：

1. 請確定CUG原則中使用的每個群組，在移轉後都存在於發佈上。
   - 如果移轉內容的CUG原則或該內容的ACL中包含群組，則群組可能存在。
   - 如果沒有，請使用套件將其安裝在目的地執行個體上（或在那裡手動建立），並啟動它及其成員。 然後確認它存在於Publish上。
1. 重新發佈與CUG原則相關聯的所有頁面，例如先編輯頁面，以確保發佈該頁面。 請務必將其全部重新發佈。
   - 重新發佈所有頁面後，請確認每個受CUG保護頁面的功能。
