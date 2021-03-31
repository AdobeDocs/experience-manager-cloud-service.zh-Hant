---
title: 利用Dynamic MediaClassic對CDN快取進行失效
description: 「瞭解如何使您的CDN（內容傳送網路）快取內容失效，讓您快速更新由Dynamic Media傳送的資產，而不需等待快取過期。」
feature: 資產管理，Dynamic Media經典
topic: 業務從業人員
role: 管理員，業務從業人員
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 14%

---


# 透過Dynamic MediaClassic {#invalidating-your-cdn-cached-content}使CDN快取失效

Dynamic Media資產由CDN（內容傳送網路）快取，以快速傳送。 不過，當您更新資產時，您會希望這些變更立即生效。 停用CDN快取內容可讓您快速更新由Dynamic Media傳送的資產，而不需等待快取過期。

>[!NOTE]
>
>此功能需要您使用隨附於Adobe Experience Manager·Dynamic Media的現成可用CDN。 此功能不支援任何其他自訂CDN。

>[!IMPORTANT]
>
>這些步驟僅適用於AEM6.5、Service Pack 5或更舊版本的Dynamic Media。<!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

另請參見[Dynamic MediaClassic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)中的快取概述。

**若要透過Dynamic MediaClassic使CDN快取失效：**

1. 開啟[Dynamic Media經典案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   您的認證和登入詳細資訊是在布建時由Adobe提供。 如果您沒有此資訊，請聯絡技術支援。

1. 按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。
1. 在「應用程式一般設定」頁面的「伺服器」群組標題下，找到&#x200B;**[!UICONTROL CDN失效範本]**&#x200B;文字方塊。

1. 指定用於使CDN（內容傳送網路）快取失效的範本。

   例如，假設您輸入參照`<ID>`的影像URL（包括影像預設集或修飾元），而不是像下列範例中的特定影像ID:

   `https://server.com/is/image/Company/<ID>?$product$`

   如果範本僅包含`<ID>`，則Dynamic Media會填入`https://<server>/is/image`，其中`<server>`是「一般設定」中定義的發佈伺服器名稱，而&lt;ID>是選取無效的資產。

1. 在頁面的右下角，點選&#x200B;**[!UICONTROL Close]**。
1. 在Dynamic Media經典(Scene7)UI中，選取一或多個資產，然後點選「**[!UICONTROL 檔案>使CDN失效」]**。 您會看到從您建立的範本和所選資產產生的一或多個URL清單。 它使用「應用程式一般設定」下「已發佈伺服器名稱」下所列的伺服器URL。

   例如，在上一步驟中設定「CDN失效範本」時，假設您選取了名為`Backpack_B`的單一影像資產影像。 當您點選「**[!UICONTROL 檔案>廢止CDN]**」時，會在「CDN失效」使用者介面中產生下列產生的URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在「URL」清單方塊中，點選「**[!UICONTROL 繼續]**」以清除每個特定URL的快取。 您可以編輯URL，也可以輸入URL或貼到URL清單方塊中，以新增URL;您不需要事先設定CDN失效範本。

   點選&#x200B;**[!UICONTROL 繼續]**&#x200B;後，會顯示一個指示器，讓您估計清除快取所需的時間。

   如果您選取多個資產，然後點選「**[!UICONTROL 檔案>使CDN]**&#x200B;無效」，則儲存的&#x200B;**[!UICONTROL 範本URL]**&#x200B;會參照每個資產。 因此，您可以定義&#x200B;**[!UICONTROL CDN無效範本]**，以參考網站上參考的每個URL影像預設集，例如產品詳情和搜尋結果。 然後，當您從快取中選取一或影像以進行失效時，URL會自動填入介面。

   >[!NOTE]
   >
   >當您選取資產，然後點選「**[!UICONTROL 檔案>使CDN失效]**」時，Dynamic Media會使用無效的CDN範本，自動建立要從CDN中失效的URL。 如果「 **[!UICONTROL CDN失效範本」文字方塊中沒有任何項目]** ，則會顯示空白的URL清單。CDN的快取並非以資產為基礎；它是以URL為基礎。因此，您必須注意您網站上的完整URL。在您決定這些URL後，可以在步驟的前面將它們新 **[!UICONTROL 增至「使CDN範本無效]** 」文字方塊。然後，您可以選取這些資產，並在單一步驟中使URL無效。
   >
   >另一個選項是將完整的URL新增至&#x200B;**[!UICONTROL 使CDN]**&#x200B;清單無效。 如果您遵循此方法，在前往「**[!UICONTROL 檔案>使CDN]**」選項之前，不必先在Dynamic MediaClassic中選取資產。

