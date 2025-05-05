---
title: 在 Dynamic Media 中啟動直接連結保護
description: 瞭解如何在Dynamic Media中啟用直接連結保護。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---

# 在 Dynamic Media 中啟動直接連結保護 {#activating-hotlink-protection-in-dynamic-media}

熱連結是指第三方網站使用HTML程式碼顯示您網站中的影像時。 每次要求圖片時，他們都會使用您的頻寬，因為訪客的瀏覽器會直接從您的伺服器存取圖片。 直接連結&#x200B;*保護*&#x200B;是防止其他網站直接連結至您網頁上的圖片、CSS或JavaScript的方法。 這種遮蔽有助於減少動態媒體帳戶下不必要的頻寬使用量。

[Adobe客戶支援](https://experienceleague.adobe.com/zh-hant?support-solution=Experience+Manager#home)可以在CDN層級設定反向連結篩選器。 這麼做可確保只將Dynamic Media內容提供給網域允許網站清單上的網站。

>[!NOTE]
>
>此功能需要您使用Adobe Experience Manager Dynamic Media隨附的現成可用CDN。 此功能不支援任何其他自訂CDN。 若要啟用快速連結保護，管理員必須建立支援票證以請求對您的Dynamic Media帳戶進行設定變更。 啟用熱連結保護不需要額外付費。
