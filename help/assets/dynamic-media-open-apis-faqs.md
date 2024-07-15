---
title: 具有OpenAPI功能的Dynamic Media常見問題
description: 具有OpenAPI功能的Dynamic Media常見問題
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 0%

---

# 具有OpenAPI功能的Dynamic Media常見問題 {#new-dynaminc-media-apis-frequently-asked-questions}

+++**Experience Manager Assetsas a Cloud Service存放庫中的所有資產是否都可供使用Dynamic Media搭配OpenAPI功能進行搜尋和傳送？**

否，只有[已核准和最新版本的資產](/help/assets/approve-assets.md)可供使用Dynamic Media搭配OpenAPI功能進行搜尋和傳送，以確保所有管道和應用程式的品牌一致性。

+++

+++**管理員如何將新增到資料夾的新資產和現有資產標示為已核准？**

Experience Manager Assets中資產的狀態是由`jcr:content/metadata/dam:status`屬性所控管。 此屬性的值可以是：

* 已核准

* 已拒絕

* 已要求變更

Experience Manager Assets會使用資產卡上可用的已核准圖示來區分已核准狀態，如下列用於「管理員」和「資產」檢視的影像所示：

**管理員檢視**

在管理員檢視中![已核准的資產](/help/assets/assets/approved-assets-thumbs-up.png)

**Assets檢視**

![在Assets檢視中核准的資產](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


若要核准資料夾中的所有資產，請參閱[如何大量核准資料夾](/help/assets/approve-assets.md#bulk-approve-assets)中的資產的指示。 此外還有一段影片說明整個程式。

設定資料夾進行大量核准後，所有新增至資料夾的新資產都會自動核准。 重新處理資產後，會核准所有現有資產。 如需如何重新處理資產的指示，請參閱[重新處理數位資產](/help/assets/reprocessing.md)。 如果您從任何其他資料夾複製或移動未核准的資產，您需要[重新處理資產](/help/assets/reprocessing.md)。

如果管理員指定`Rejected`或`Changes requested`值，資產會標示為`Rejected`。 Experience Manager Assets會使用「管理員」檢視中資產卡上可用的![拒絕Assets](/help/assets/assets/do-not-localize/reject-assets.svg)來區分「已拒絕」狀態。

同樣地，Experience Manager Assets會使用資產卡上的下列已拒絕狀態，在Assets檢視中區分「已拒絕」狀態：

在Assets檢視中![拒絕的資產](/help/assets/assets/rejected-assets-admin-view.png)


+++

+++**如何取得Adobe IMS (Adobe Identity Management Services)使用者或群組ID，以便在Experience Manager管理員檢視中設定資產的角色，以保護傳遞和搜尋體驗？**

需要存取Experience Manager作者環境的使用者會在Adobe的Admin Console中管理為Adobe IMS使用者。 如需瞭解什麼是Adobe IMS使用者，以及如何在Admin Console中存取和管理這些使用者，請參閱[Adobe IMS使用者](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en)。

+++

+++**您可以在一個資料夾中同時核准多個資產嗎？**

可以，您可以同時核准資料夾中的多個資產。

執行以下步驟，在[!DNL Experience Manager Assets Admin view]中同時核准多個資產：

1. 選取資產並按一下&#x200B;**[!UICONTROL 屬性]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤中，向下捲動至&#x200B;**[!UICONTROL 檢閱狀態]**。
1. 將稽核狀態變更為&#x200B;**[!UICONTROL 已核准]**。
1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

同樣地，若要在Assets檢視的資料夾中同時核准多個資產：

1. 選取資產並按一下&#x200B;**[!UICONTROL 大量中繼資料編輯]**。

1. 在右窗格的[!UICONTROL 屬性]區段中可用的&#x200B;**[!UICONTROL 狀態]**&#x200B;欄位中選取&#x200B;**[!UICONTROL 已核准]**。

1. 按一下「**[!UICONTROL 儲存]**」。


+++

+++**如何保護資產傳遞安全，並搜尋Dynamic Media OpenAPI？**

Experience Manager中的中央資產控管可讓DAM管理員或品牌管理員管理對資產的存取。 他們可以藉由設定角色或在編寫端為已核准資產設定啟用和停用時間(尤其是在AEM as a Cloud Service編寫執行個體上)來限制存取。

搜尋或運用傳送URL的一般使用者，可在成功通過授權程式後取得受限制資產的存取權。

如需詳細資訊，請參閱[限制存取Experience Manager](restrict-assets-delivery.md#authoring)中的資產。

+++

+++**如何取得編輯資產核准狀態的許可權？**

身為DAM使用者，您可能沒有[核准資產](approve-assets.md#approve-assets)的許可權。 若要取得編輯資產核准狀態的許可權，管理員可以編輯套用至資產資料夾的預設或任何其他中繼資料結構，以提供&#x200B;**[!UICONTROL 檢閱狀態]**&#x200B;欄位的編輯許可權。 如需詳細資訊，請參閱[如何停用稽核狀態](approve-assets.md#configuration)欄位的編輯。

+++

+++**具有OpenAPI功能的Dynamic Media與Dynamic Media解決方案有何不同？**

Dynamic Media搭配OpenAPI功能和Dynamic Media代表獨特的解決方案，每個解決方案都有其專門的傳送功能。 您必須徹底檢閱您的特定需求，以決定最符合您需求的解決方案。

Adobe的一般指引是將Dynamic Media與OpenAPI棧疊用於任何整合使用案例（第一方或第三方應用程式）。 如果與Dynamic Media棧疊已存在整合，則建議不要變更它，因為OpenAPI棧疊URL的結構不同。 僅適用於任何全新的整合使用案例，請善用OpenAPI棧疊。 如果您的使用案例需要進階修飾元，而OpenAPI棧疊沒有這些修飾元，請避免OpenAPI棧疊，直到Adobe橋接好缺口為止。 即使是來自AEM AssetsCloud Service的基本原生傳送，只要您的使用案例包含OpenAPI棧疊可用的修飾元，就可以評估OpenAPI棧疊。 總之，根據使用案例的性質，Dynamic Media和具有OpenAPI棧疊的Dynamic Media可以共存。

以下是具有OpenAPI功能的Dynamic Media與Dynamic Media之間的一些主要差異：

| 具有OpenAPI功能的Dynamic Media | Dynamic Media |
|---|---|
| [僅適用於Assetsas a Cloud Service](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | 內部部署或Adobe Managed Services也提供此功能，包含其他設定和布建步驟。 |
| [受支援的影像修飾元集有限，例如寬度、高度、旋轉、翻轉、品質和格式](/help/assets/deliver-assets-apis.md) | 豐富的可用影像修飾元集 |
| 根據使用者、角色、日期和時間[限制資產傳遞](/help/assets/restrict-assets-delivery.md) | 發佈至Dynamic Media的Assets可供所有使用者存取 |
| 大部分開發人員都熟悉OpenAPI規格。 使用[Micro Frontend Asset Selector](/help/assets/asset-selector.md)，AEM Assets的擴充性就會變得非常簡單。 | 以SOAP為基礎的API，在開發整合自訂功能時成為了障礙。 |
| 對DAM中已核准的資產所做的任何變更（包括版本更新和中繼資料修改）都會自動反映在傳送URL中。 透過CDN為Dynamic Media的OpenAPI功能設定了短短的存留時間(TTL)值（10分鐘），不到10分鐘即可顯示所有製作和發佈介面的更新。 | 建議的CDN TTL為10小時。 您可以使用快取失效動作覆寫TTL值。 |
| 只有已核准的資產可用於將資產傳送至下游應用程式，以在數位體驗中啟用品牌核准的資產。 | Dynamic Media已發佈資產的任何更新都會自動發佈，無需任何核准工作流程，而這無法確保在數位體驗中擁有品牌核准的資產。 |
| 使用情況報表以傳送的資產數量為基礎。 此功能即將推出。 | 使用情況報表無法使用。 此功能即將推出。 |
| 下游應用程式無法再使用Assetsas a Cloud Service存放庫中標示為過期的Assets。 | 沒有固有資產到期日。 資產會維持在公開狀態，直到從AEM as a Cloud Service存放庫中刪除為止。 |
| 不支援影像預設集和視訊智慧型裁切功能。 | 支援影像預設集和視訊智慧型裁切功能。 |
| 動態視訊編碼，確保根據輸入視訊提供最佳編碼。 原生視訊傳送不需要任何設定。 | 不論輸入視訊為何，標準3都會進行編碼（可能會影響視訊傳送效能）。 您必須手動設定不同視訊位元速率的不同編碼。 |
| 難以猜測資產UID型URL （啟用URL模糊化），但SEO已最佳化。 | URL模糊化僅適用於URL查詢引數。 URL中的Assets ID （資產名稱）是可辨識的。 |

+++

+++**具有OpenAPI功能的Dynamic Media如何解決連線Assets功能的限制？**

下表概述兩種解決方案之間的主要差異：

| 具有OpenAPI功能的Dynamic Media | 連接的資產 |
|---|---|
| 遠端DAM部署上的Assets可在AEM as a Cloud Service上使用。 | 遠端DAM部署上的Assets可在AEM as a Cloud Service或Adobe Managed Services上使用。 |
| 遠端DAM部署中的資產可供AEM Sites執行個體使用時，不會複製資產二進位檔。 | 當遠端DAM部署中的資產可在AEM Sites執行個體上使用時，則會複製資產二進位檔。 |
| 支援AEM Assets支援的所有資產格式型別。 | 不支援視訊。 |
| 您可以從遠端DAM部署擷取資產時，在本機Sites部署上使用Dynamic Media 。 | 本機Sites部署上的Dynamic Media為唯讀。 |
| 連線至遠端DAM部署的AEM Sites執行個體數目沒有限制。 您可以針對遠端DAM上核准的資產設定角色](/help/assets/restrict-assets-delivery.md)，以[限制對Sites執行個體上資產的存取。 | 限制最多可將4個AEM Sites執行個體連線至遠端DAM部署。 數量增加需要額外的測試。 |
| Asset Selector和具有OpenAPI功能的Dynamic Media都可擴充，以允許自訂整合。 | 連線的Assets API無法延伸，因此無法自訂整合。 |
| 對遠端DAM部署中可用的已核准資產所做的任何變更（包括版本更新和中繼資料修改），都會在10分鐘的短存留時間(TTL)值內自動反映在Sites執行個體上。 | 遠端DAM部署的資產更新會透過生命週期事件自動處理，但比具有OpenAPI功能的Dynamic Media需要更多時間。 |
| 遠端DAM的資產中繼資料也可在AEM Sites例項上使用。 | 遠端DAM的資產中繼資料在AEM Sites例項上無法使用。 |

+++



