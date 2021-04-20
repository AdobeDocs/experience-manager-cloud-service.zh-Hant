---
title: HTTP2 傳送內容常見問答集
description: 瞭解HTTP2內容傳送。
topic: "Administrator,Business Practitioner"
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 3%

---


# HTTP2 傳送內容常見問答集{#http-delivery-of-content-faq}

Adobe很高興宣佈推出HTTP/2內容傳送。 使用HTTP/2時，整體效能會有所提升。

>[!NOTE]
>
>此功能需要您使用隨附於Adobe Experience Manager·Dynamic Media的現成可用CDN。 此功能不支援任何其他自訂CDN。

## 什麼是HTTP/2?{#what-is-http}

HTTP/2改善了瀏覽器和伺服器通訊的方式，讓資訊傳輸更快速，同時降低了所需的處理能力。

以下網站以簡單簡單的方式說明HTTP/2及其優點：

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## 轉換至HTTP/2以進行內容傳送的主要優點為何？{#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

由於效能改進基於各種因素，因此存在很大差異。 例如，您網站的程式碼、您使用Dynamic Media的方式、消費者的裝置、螢幕和位置。

Adobe的自行測試得出如下結果：

* 對於影像，視裝置和瀏覽器而定，回應時間提高了7%至28%。 在iOS裝置上，效能提升最顯著。
* 對於檢視器，載入時間效能提升了15%。

下列展示說明HTTP/1與HTTP/2載入之間的差異：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否符合切換至HTTP/2的資格？{#am-i-eligible-to-switch-over-to-http}

若要使用HTTP/2，您必須符合下列需求：

* 針對您的豐富式媒體要求使用安全的HTTPS。
* 使用Adobe搭售的CDN（內容傳送網路）做為您的Dynamic Media經典授權的一部分。
* 使用專用網域（即`images.company.com`或`mycompany.scene7.com`），而不使用通用Dynamic Media網域（即`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

   若要尋找您的網域，請開啟[Dynamic MediaClassic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。查找標有&#x200B;**「已發佈伺服器名稱」的欄位。**&#x200B;如果您目前使用一般的Dynamic Media網域，則可請求移至您自己的自訂網域，做為轉換的一部分。

## 為我的Dynamic Media帳戶啟用HTTP/2的程式為何？{#what-is-the-process-for-enabling-http-for-my-dm-account}

[使用Admin Console建立支援案](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) 例並要求切換至HTTP/2;它不會自動為您完成。

1. 在您的支援案例中提供下列資訊：

   * 主要聯絡人姓名、電子郵件和電話號碼。
   * 要轉換到HTTP2的所有網域。 即`images.company.com`或`mycompany.scene7.com`。

   若要尋找您的網域，請開啟[Dynamic MediaClassic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。查找標有&#x200B;**[!UICONTROL 「已發佈伺服器名稱」的欄位。]**

   * 確認您對多媒體請求使用安全的HTTPS。
   * 驗證您是否透過Adobe使用CDN，而非直接關係管理。
   * 確認您使用的是專用網域。 即`images.company.com`或`mycompany.scene7.com`，而非一般的Dynamic Media網域，例如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`。

   若要尋找您的網域，請開啟[Dynamic MediaClassic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。查找標有&#x200B;**[!UICONTROL 「已發佈伺服器名稱」的欄位。]**&#x200B;如果您目前使用一般的Dynamic Media網域，則可請求移至您自己的自訂網域，做為轉換的一部分。

   1. 技術支援會根據提交請求的順序，將您新增至HTTP/2客戶候補清單。
   1. 當Adobe準備好處理您的請求時，客戶服務會聯絡您以協調轉換並設定目標日期。
   1. 完成後，您將會收到通知，並可驗證是否成功轉換至HTTP2。



## 我何時可以轉換為HTTP/2?{#when-can-i-expect-to-be-transitioned-over-to-http}

請求的處理順序為技術支援部門接收請求的順序。

>[!NOTE]
>
>因為轉換至HTTP/2需要清除快取，所以前置時間較長。 因此，一次只能處理幾次客戶轉場。

## 改用HTTP/2有哪些風險？{#what-are-the-risks-with-moving-to-http}

轉換至HTTP/2會清除CDN中的快取，因為它需要移至新的CDN設定。

非快取內容會直接點擊Adobe的原始伺服器，直到重新建立快取為止。 由於採取了這項行動，Adobe計劃一次處理幾次客戶轉場。 此方法可確保在從來源提取請求時仍能維持可接受的效能。

## 如何驗證URL或網站是否已使用HTTP/2啟動？{#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

下載擴充功能以搭配您的網頁瀏覽器使用。 對於Firefox和Chrome，有一個名為&#x200B;**[!UICONTROL HTTP/2和SPDY Indicator]**&#x200B;的擴充功能。 瀏覽器僅安全支援HTTP/2，因此必須使用HTTPS呼叫URL以進行驗證。 如果支援HTTP/2，則會以藍色Flash符號的擴充功能來指出，並加上標題&quot;X-Firefox-Spdy&quot;:&quot;h2&quot;。
