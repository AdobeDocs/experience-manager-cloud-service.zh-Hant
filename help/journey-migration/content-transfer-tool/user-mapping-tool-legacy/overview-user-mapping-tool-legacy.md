---
title: 用戶映射工具概述（舊版）
description: 用戶映射工具概述（舊版）
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: 8a258c2c929f9af84a1cde99072291a3e7f6cfc3
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 10%

---

# 用戶映射工具概述（舊版） {#overview-user-mapping-tool}

>[!INFO]
>
>本文檔指的是已過時的工具版本。 有關最新版本的詳細資訊，請參見 [用戶映射和主遷移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md)。

<!-- Alexandru: drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## 簡介 {#introduction}

在向Adobe Experience Manager(AEM)as a Cloud Service過渡的過程中，您需要將用戶和組從現有系統移AEM動到AEMas a Cloud Service。 這由內容傳輸工具完成。

AEM as a Cloud Service 最重大的變更是完全整合使用 Adobe ID 以存取作者層。這需要使用 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 用於管理用戶和組。 用戶配置檔案資訊集中在AdobeIdentity Management系統(IMS)中，該系統在所有Adobe雲應用程式中提供單點登錄。 有關詳細資訊，請參閱 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management)。 由於這一變化，現有用戶和組需要映射到其IMS ID以避免在Cloud Service作者實例上出現重複的用戶和組。

## 使用者對應工具 {#mapping-tool}

內容傳輸工具（沒有用戶映射）將遷移與要遷移的內容相關聯的所有用戶和組。 用戶映射工具是內容傳輸工具的一部分，其唯一目的是修改用戶，使其能夠被IMS正確識別，IMS是as a Cloud Service使用的單點登錄功AEM能。 完成這些修改後，內容傳輸工具將像往常一樣遷移指定內容的用戶和組。

### 下一步 {#whats-next}

一旦您瞭解了用戶映射工具是什麼，您現在就可以在使用用戶映射工具之前查看重要注意事項和例外情況。 請參閱 [用戶映射工具的重要注意事項](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) 的子菜單。
