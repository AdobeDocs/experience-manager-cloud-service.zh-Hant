---
title: 使用者對應工具概觀（舊版）
description: 使用者對應工具概觀（舊版）
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 10%

---

# 使用者對應工具概觀（舊版） {#overview-user-mapping-tool}

>[!INFO]
>
>本檔案旨在說明該工具的已棄用版本。 如需最新版本的詳細資訊，請參閱 [使用者對應和主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

<!-- Alexandru: drafting this for now

NOTE: "LEGACY" for user mapping includes everything before (i.e. not including) 2.0.16 of CTT.

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## 簡介 {#introduction}

在轉變到Adobe Experience Manager (AEM) as a Cloud Service的歷程中，您必須將使用者和群組從您現有的AEM系統移動到AEMas a Cloud Service。 此移轉作業會由「內容轉移工具」完成。

AEM as a Cloud Service 最重大的變更是完全整合使用 Adobe ID 以存取作者層。此整合需要使用 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 用於管理使用者和使用者群組。 使用者設定檔資訊集中在AdobeIdentity Management系統(IMS)中，可在所有Adobe雲端應用程式中提供單一登入。 如需詳細資訊，請參閱 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=en#identity-management). 由於此變更，現有使用者和群組必須對應至其IMS ID，以避免Cloud Service作者執行個體上重複的使用者和群組。

## 使用者對應工具 {#mapping-tool}

內容轉移工具（沒有使用者對應）會移轉與正在移轉的內容相關聯的任何使用者和群組。 「使用者對應工具」是「內容轉移工具」的一部分。 其唯一用途是編輯使用者，以便讓IMS (AEMas a Cloud Service使用的單一登入功能)正確辨識使用者。 完成這些修改後，內容轉移工具會照常移轉指定內容的使用者和群組。

### 下一步 {#whats-next}

瞭解了什麼是使用者對應工具後，您現在就可以開始在使用使用者對應工具之前，檢視重要的考量和特殊案例。 另請參閱 [使用者對應工具的重要考量](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) 以取得更多詳細資料。
