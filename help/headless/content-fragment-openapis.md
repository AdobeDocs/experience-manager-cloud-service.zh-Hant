---
title: 內容片段和內容片段模型的 OpenAPI
description: 了解內容片段和內容片段模型的 OpenAPI。
exl-id: 077eed73-a066-4273-b2f5-da4bf5cd900c
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: d683051387af5c0de45917a50003c2194d887bc4
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 47%

---

# 內容片段和內容片段模型管理OpenAPI {#content-fragments-and-content-fragment-models-management-openapis}

內容片段管理 API 的現代化 OpenAPI 實作可讓開發人員以程式設計方式在 AEM Author 上執行建立、讀取、更新和刪除作業，以管理儲存在 AEM 中的內容片段模型和內容片段。這些 API 支援多種使用案例。

內容片段[資產 HTTP API](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets) 的現有用法應遷移到新的內容片段管理 OpenAPI。如需完整文件，請參閱「[內容片段管理 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)」。

>[!NOTE]
>
>若您未登入AEM，則需取得授權才能存取OpenAPI；例如，將OpenAPI用於其他產品作為整合的一部分時。
>
>如需授權您存取OpenAPI的詳細資訊，請參閱[OpenAPI型API](/help/implementing/developing/open-api-based-apis.md)。

>[!CAUTION]
>
>依預設，發佈時會停用內容片段管理OpenAPI。 針對傳遞導向的使用案例，建議您使用[內容片段傳遞OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md)，不要採用此做法。

>[!NOTE]
>
>請參閱[結構化內容傳遞與管理的AEM API](/help/headless/apis-headless-and-content-fragments.md)，以取得各種可用API的概觀，以及所涉及概念的比較。