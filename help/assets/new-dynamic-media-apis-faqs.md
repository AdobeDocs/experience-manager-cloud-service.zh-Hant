---
title: 具有OpenAPI功能的Dynamic Media常見問題
description: 具有OpenAPI功能的Dynamic Media常見問題
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# 具有OpenAPI功能的Dynamic Media常見問題 {#new-dynaminc-media-apis-frequently-asked-questions}

+++**Experience Manager Assetsas a Cloud Service存放庫中的所有資產是否都可供使用Dynamic Media搭配OpenAPI功能進行搜尋和傳送？**

否，只有[已核准和最新版本的資產](/help/assets/approved-assets.md)可供使用Dynamic Media搭配OpenAPI功能進行搜尋和傳送，以確保所有管道和應用程式的品牌一致性。

+++

+++**管理員如何將新增到資料夾的新資產和現有資產標示為已核准？**

Experience Manager Assets中資產的狀態是由`jcr:content/metadata/dam:status`屬性所控管。 此屬性的值可以是：

* 已核准

* 已拒絕

* 已要求變更

Experience Manager Assets會使用資產卡上可用的![核准Assets](assets/thumbs-up-icon.svg)來區分「已核准」狀態，如下圖所示：

已核准資產的![圖示](/help/assets/assets/approved-assets-thumbs-up.png)

若要核准資料夾中的所有資產，請參閱[如何大量核准資料夾](/help/assets/approved-assets.md#bulk-approve-assets)中的資產的指示。 此外還有一段影片說明整個程式。

設定資料夾進行大量核准後，所有新增至資料夾的新資產都會自動核准。 重新處理資產後，會核准所有現有資產。 如需如何重新處理資產的指示，請參閱[重新處理數位資產](/help/assets/reprocessing.md)。 如果您從任何其他資料夾複製或移動未核准的資產，您需要[重新處理資產](/help/assets/reprocessing.md)。

如果管理員指定`Rejected`或`Changes requested`值，資產會標示為`Rejected`。 Experience Manager Assets會使用資產卡上可用的![拒絕Assets](/help/assets/assets/do-not-localize/reject-assets.svg)來區分「已拒絕」狀態。

+++

+++**如何取得Adobe IMS (Adobe Identity Management Services)使用者或群組ID，以便在Experience Manager管理員檢視中設定資產的角色，以保護傳遞和搜尋體驗？**

需要存取Experience Manager作者環境的使用者會在Adobe的Admin Console中管理為Adobe IMS使用者。 如需瞭解什麼是Adobe IMS使用者，以及如何在Admin Console中存取和管理這些使用者，請參閱[Adobe IMS使用者](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en)。

+++

+++**您可以在一個資料夾中同時核准多個資產嗎？**

可以，您可以同時核准資料夾中的多個資產。

執行以下步驟，在[!DNL Experience Manager Assets]中同時核准多個資產：

1. 選取資產並按一下&#x200B;**[!UICONTROL 屬性]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤中，向下捲動至&#x200B;**[!UICONTROL 檢閱狀態]**。
1. 將稽核狀態變更為&#x200B;**[!UICONTROL 已核准]**。
1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

+++

+++**如何保護資產傳遞安全，並搜尋Dynamic Media OpenAPI？**

Experience Manager中的中央資產控管可讓DAM管理員或品牌管理員管理對資產的存取。 他們可以透過在編寫端為已核准的資產設定角色來限制存取權，尤其是在AEM as a Cloud Service編寫執行個體上。

搜尋或運用傳送URL的一般使用者，可在成功通過授權程式後取得受限制資產的存取權。

如需詳細資訊，請參閱[限制存取Experience Manager](restrict-assets-delivery.md#authoring)中的資產。

+++

+++**如何取得編輯資產核准狀態的許可權？**

身為DAM使用者，您可能沒有[核准資產](approved-assets.md#approve-assets)的許可權。 若要取得編輯資產核准狀態的許可權，管理員可以編輯套用至資產資料夾的預設或任何其他中繼資料結構，以提供&#x200B;**[!UICONTROL 檢閱狀態]**&#x200B;欄位的編輯許可權。 如需詳細資訊，請參閱[如何停用稽核狀態](approved-assets.md#configuration)欄位的編輯。

+++

+++**具有OpenAPI功能的Dynamic Media與Dynamic Media解決方案有何不同？**

Dynamic Media搭配OpenAPI功能和Dynamic Media代表獨特的解決方案，每個解決方案都有其專門的傳送功能。 您必須徹底檢閱您的特定需求，以決定最符合您需求的解決方案。

以下是具有OpenAPI功能的Dynamic Media與Dynamic Media之間的一些主要差異：

| 具有OpenAPI功能的Dynamic Media | Dynamic Media |
|---|---|
| [僅適用於Assetsas a Cloud Service](/help/assets/new-dynamic-media-overview.md#prerequisites-new-dynaminc-media-apis) | 內部部署或Adobe Managed Services也提供此功能，包含其他設定和布建步驟。 |
| [受支援的影像修飾元集有限，例如寬度、高度、旋轉、翻轉、品質和格式](/help/assets/deliver-assets-apis.md) | 豐富的可用影像修飾元集 |
| 根據使用者和角色[已限制資產傳遞](/help/assets/restrict-assets-delivery.md) | 發佈至Dynamic Media的Assets可供所有使用者存取 |
| 支援影像智慧型裁切 | 支援影像和視訊智慧型裁切 |
| 棧疊以OpenAPI規格為基礎，大多數開發人員都採用類似規格。 使用[Micro Frontend Asset Selector](/help/assets/asset-selector.md)，AEM Assets的擴充性就會變得非常簡單。 | 以SOAP為基礎的API，在開發整合自訂功能時成為了障礙。 |
| 對DAM中已核准的資產所做的任何變更（包括版本更新和中繼資料修改）都會自動反映在傳送URL中。 透過CDN為Dynamic Media的OpenAPI功能設定了短短的存留時間(TTL)值（10分鐘），不到10分鐘即可顯示所有製作和發佈介面的更新。 | 建議的CDN TTL為10小時。 您可以使用快取失效動作覆寫TTL值。 |
| 只有已核准的資產可用於將資產傳送至下游應用程式，以在數位體驗中啟用品牌核准的資產。 傳遞的資產會遵守AEM as a Cloud Service存放庫製作執行個體上的資產到期狀態。 | Dynamic Media已發佈資產的任何更新都會自動發佈，無需任何核准工作流程，而這無法確保在數位體驗中擁有品牌核准的資產。 沒有固有資產到期日。 資產會維持在公開狀態，直到從AEM as a Cloud Service存放庫中刪除為止。 |
| 使用情況報表以傳送的資產數量為基礎。 | 使用情況報表無法使用。 |

+++

+++**具有OpenAPI功能的Dynamic Media如何解決連線Assets功能的限制？**

下表概述兩種解決方案之間的主要差異：

| 具有OpenAPI功能的Dynamic Media | 連接的資產 |
|---|---|
| 遠端DAM部署上的Assets可在AEM as a Cloud Service上使用。 | 遠端DAM部署上的Assets可在AEM as a Cloud Service或Adobe Managed Services上使用。 |
| 遠端DAM部署中的資產可供AEM Sites執行個體使用時，不會複製資產二進位檔。 | 當遠端DAM部署中的資產可在AEM Sites執行個體上使用時，則會複製資產二進位檔。 |
| 支援AEM Assets支援的所有資產格式型別。 | 不支援視訊。 |
| 支援影像智慧型裁切。 | 支援Dynamic Media影像智慧型裁切和影像預設集。 |
| 您可以從遠端DAM部署擷取資產時，在本機Sites部署上使用Dynamic Media 。 | 本機Sites部署上的Dynamic Media為唯讀。 |
| 連線至遠端DAM部署的AEM Sites執行個體數目沒有限制。 您可以針對遠端DAM上核准的資產設定角色](/help/assets/restrict-assets-delivery.md)，以[限制對Sites執行個體上資產的存取。 | 限制最多可將4個AEM Sites執行個體連線至遠端DAM部署。 數量增加需要額外的測試。 |
| Asset Selector和具有OpenAPI功能的Dynamic Media都可擴充，以允許自訂整合。 | 連線的Assets API無法延伸，因此無法自訂整合。 |
| 對遠端DAM部署中可用的已核准資產所做的任何變更（包括版本更新和中繼資料修改），都會在10分鐘的短存留時間(TTL)值內自動反映在Sites執行個體上。 | 遠端DAM部署的資產更新會透過生命週期事件自動處理，但比具有OpenAPI功能的Dynamic Media需要更多時間。 |
| 遠端DAM的資產中繼資料也可在AEM Sites例項上使用。 | 遠端DAM的資產中繼資料在AEM Sites例項上無法使用。 |

+++



