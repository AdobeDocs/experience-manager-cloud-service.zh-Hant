---
title: 使用者對應工具概覽
description: 使用者對應工具概覽
source-git-commit: 60e67e92f4f1ecaaf12c58f16f4324868d223934
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---


# 使用者對應工具概覽 {#overview-user-mapping-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="使用者對應工具"
>abstract="「內容轉移工具」可協助您將使用者和群組從您現有的AEM系統移至AEMas a Cloud Service。 現有的使用者和群組必須對應至其IMS ID，以避免Cloud Service製作例項上出現重複的使用者和群組。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="使用使用者對應工具的重要考量"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="使用使用者對應工具"

## 簡介 {#introduction}

在轉換至Adobe Experience Manager(AEM)的as a Cloud Service過程中，您必須將使用者和群組從您現有的AEM系統移至AEMas a Cloud Service。 這是由「內容轉移工具」完成。

AEMas a Cloud Service的重大變更，是完整整合使用AdobeID來存取作者階層。  這需要使用[Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)來管理使用者和使用者群組。 AdobeIdentity Management系統(IMS)會集中提供使用者設定檔資訊，以針對所有Adobe雲端應用程式提供單一登入。 如需詳細資訊，請參閱[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management)。 因為此變更，現有的使用者和群組必須對應至其IMS ID，以避免Cloud Service製作例項上出現重複的使用者和群組。

## 使用者對應工具 {#mapping-tool}

「內容轉移工具」（不含「使用者對應」）將移轉與要移轉之內容相關聯的任何使用者和群組。 「使用者對應工具」是「內容轉移工具」的一部分，其唯一用途是修改使用者和群組，讓IMS(AEMas a Cloud Service使用的單一登入功能)可正確辨識這些使用者和群組。 完成這些修改後，「內容轉移工具」會照常移轉指定內容的使用者和群組。

### 下一步 {#whats-next}

一旦您了解了用戶映射工具是什麼，您現在就可以在使用用戶映射工具之前查看重要注意事項和特殊案例。 如需詳細資訊，請參閱[使用者對應工具的重要考量事項](/help/move-to-cloud-service/content-transfer-tool/user-mapping-tool/considerations-user-mapping-tool.md) 。