---
title: 在Dynamic Media中啟用快速連結保護
description: 了解如何在Dynamic Media中啟用直接連結保護。
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 3%

---

# 在Dynamic Media中啟用快速連結保護 {#activating-hotlink-protection-in-dynamic-media}

熱連結是指第三方網站使用HTML代碼來顯示您網站的影像時。 每次請求圖片時，他們都會使用您的頻寬，因為訪客的瀏覽器會直接從您的伺服器存取圖片。 快速連結 *保護* 是防止其他網站直接連結至您網頁上的圖片、CSS或JavaScript的方法。 這種防護有助於減少您Dynamic Media帳戶下不必要的頻寬使用。

[Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=Experience+Manager#home) 可在CDN層級設定反向連結篩選器。 這麼做可確保Dynamic Media內容只會提供給您所允許網域之網站清單上的網站。

>[!NOTE]
>
>若要使用此功能，您必須使用隨Adobe Experience Manager Dynamic Media提供的現成可用CDN。 此功能不支援任何其他自訂CDN。 若要啟用熱連結保護，管理員必須建立支援票證，以要求對您的Dynamic Media帳戶進行配置變更。 激活熱鏈路保護無需額外費用。
