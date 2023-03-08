---
title: 使用者對應工具概觀（舊版）
description: 使用者對應工具概觀（舊版）
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: 69dfe7f98628ab67cc3a994c32b1530550ec6a01
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 11%

---

# 使用者對應工具概覽 {#overview-user-mapping-tool}


<!-- Alexandru: drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## 簡介 {#introduction}

在轉換至Adobe Experience Manager(AEM)的as a Cloud Service過程中，您必須將使用者和群組從您現有的AEM系統移至AEMas a Cloud Service。 這是由「內容轉移工具」完成。

AEM as a Cloud Service 最重大的變更是完全整合使用 Adobe ID 以存取製作層。這需要使用 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 用於管理使用者和使用者群組。 AdobeIdentity Management系統(IMS)會集中提供使用者設定檔資訊，以針對所有Adobe雲端應用程式提供單一登入。 如需詳細資訊，請參閱 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). 因為此變更，現有的使用者和群組必須對應至其IMS ID，以避免Cloud Service製作例項上出現重複的使用者和群組。

## 使用者對應工具 {#mapping-tool}

「內容轉移工具」（不含「使用者對應」）將移轉與要移轉之內容相關聯的任何使用者和群組。 「使用者對應工具」是「內容轉移工具」的一部分，其唯一用途是修改使用者，讓IMS(AEMas a Cloud Service使用的單一登入功能)能正確辨識他們。 完成這些修改後，「內容轉移工具」會照常移轉指定內容的使用者和群組。

### 下一步 {#whats-next}

一旦您了解了用戶映射工具是什麼，您現在就可以在使用用戶映射工具之前查看重要注意事項和特殊案例。 請參閱 [使用者對應工具的重要考量](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) 以取得更多詳細資訊。
