---
title: 用戶映射工具概述
description: 用戶映射工具概述
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# 用戶映射工具概述 {#overview-user-mapping-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="用戶映射工具"
>abstract="內容傳輸工具可幫助您將用戶和組從現有系統移AEM動到AEMas a Cloud Service。 現有用戶和組需要映射到其IMS ID以避免在Cloud Service作者實例上出現重複的用戶和組。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="使用用戶映射工具的重要注意事項"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="使用用戶映射工具"

## 簡介 {#introduction}

在向Adobe Experience Manager(AEM)as a Cloud Service過渡的過程中，您需要將用戶和組從現有系統移AEM動到AEMas a Cloud Service。 這由內容傳輸工具完成。

對as a Cloud Service的一AEM個主要改變是完全整合地使用AdobeID訪問作者層。  這需要使用 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 用於管理用戶和組。 用戶配置檔案資訊集中在AdobeIdentity Management系統(IMS)中，該系統在所有Adobe雲應用程式中提供單點登錄。 有關詳細資訊，請參閱 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management)。 由於這一變化，現有用戶和組需要映射到其IMS ID以避免在Cloud Service作者實例上出現重複的用戶和組。

## 用戶映射工具 {#mapping-tool}

內容傳輸工具（沒有用戶映射）將遷移與要遷移的內容相關聯的所有用戶和組。 用戶映射工具是內容傳輸工具的一部分，其唯一目的是修改用戶和組，以便IMS能夠正確識別它們，IMS是as a Cloud Service使用的單點登錄功能AEM。 完成這些修改後，內容傳輸工具將像往常一樣遷移指定內容的用戶和組。

### 下一步是什麼 {#whats-next}

一旦您瞭解了用戶映射工具是什麼，您現在就可以在使用用戶映射工具之前查看重要注意事項和例外情況。 請參閱 [用戶映射工具的重要注意事項](/help/journey-migration/content-transfer-tool/user-mapping-tool/considerations-user-mapping-tool.md) 的子菜單。
