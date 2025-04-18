---
title: 具有 OpenAPI 功能的 Dynamic Media 常見問題
description: 具有 OpenAPI 功能的 Dynamic Media 常見問題
role: User
exl-id: 3450e050-4b0b-4184-8e71-5e667d9ca721
source-git-commit: c36938e80d0b159c5f89d450aaa228c37c4f5276
workflow-type: ht
source-wordcount: '1600'
ht-degree: 100%

---

# 具有 OpenAPI 功能的 Dynamic Media 常見問題 {#new-dynaminc-media-apis-frequently-asked-questions}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 與 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 與 Edge Delivery Services 整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>使用者介面可擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用 Dynamic Media Prime 與 Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>具有 OpenAPI 功能的 Dynamic Media 指南現已提供 PDF 格式。下載完整指南，並使用 Adobe Acrobat AI 助理來回答您的查詢問題。
>
>[!BADGE 具有 OpenAPI 功能的 Dynamic Media 指南 PDF]{type=Informative url="https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

+++**Experience Manager Assets as a Cloud Service 存放庫中的所有資產是否都能使用具有 OpenAPI 功能的 Dynamic Media 進行搜尋和傳遞？**

否，只有[已核准的最新版本資產](/help/assets/approve-assets.md)才可使用具有 OpenAPI 功能的 Dynamic Media 進行搜尋和傳遞，以確保所有管道和應用程式的品牌一致性。

+++

+++**管理員如何將新增至資料夾的新資產和現有資產標記為已核准？**

Experience Manager Assets 中資產的狀態由 `jcr:content/metadata/dam:status` 屬性進行控管。此屬性的值可以是：

* 已核准

* 已拒絕

* 已要求變更

Experience Manager Assets 可使用資產卡片上提供的已核准圖示來辨別已核准狀態，如下圖的管理員視圖和資產視圖中所示：

**管理員視圖**

![管理員視圖中的已核准資產](/help/assets/assets/approved-assets-thumbs-up.png)

**資產視圖**

![資產視圖中的已核准資產](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


若要核准資料夾中的所有資產，請參閱[如何大量核准資料夾中的資產](/help/assets/approve-assets.md#bulk-approve-assets)相關指示。還有一段影片說明整個過程。

設定用於大量核准的資料夾後，所有新增至該資料夾的新資產都會自動獲得核准。所有現有資產都會在重新處理資產後獲得核准。請參閱[重新處理數位資產](/help/assets/reprocessing.md)以了解有關如何重新處理資產的指示。如果您從任何其他資料夾複製或移動未經核准的資產，就需要[重新處理資產](/help/assets/reprocessing.md)。

如果管理員指定 `Rejected``Rejected` 或 `Changes requested` 值，該資產會標記為 。Experience Manager Assets 可透過管理視圖中資產卡片上提供的![拒絕資產](/help/assets/assets/do-not-localize/reject-assets.svg)來辨別已拒絕狀態。

同樣地，Experience Manager Assets 可使用資產卡片上的下列已拒絕狀態，來辨別資產視圖中的已拒絕狀態：

![資產視圖中的已拒絕資產](/help/assets/assets/rejected-assets-admin-view.png)


+++

+++**如何取得 Adobe IMS (Adobe Identity Management Services) 使用者或群組 ID，藉此在 Experience Manager 管理員視圖中設定資產角色，以確保傳遞和搜尋體驗？**

在 Adobe 的 Admin Console 中，系統會將需要存取 Experience Manager 製作環境的使用者視為 Adobe IMS 使用者來管理。如需有關何謂 Adobe IMS 使用者，以及如何在 Admin Console 中加以存取和管理的資訊，請參閱 [Adobe IMS 使用者](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=zh-hant)。

+++

+++**可以在一個資料夾內同時核准多項資產嗎？**

可以，您可以在一個資料夾內同時核准多項資產。

執行以下步驟即可在 [!DNL Experience Manager Assets Admin view] 中同時核准多項資產：

1. 選取資產，然後按一下「**[!UICONTROL 屬性]**」。
1. 在「**[!UICONTROL 基本]**」索引標籤中，向下捲動至「**[!UICONTROL 審查狀態]**」。
1. 將審查狀態變更為「**[!UICONTROL 已核准]**」。
1. 按一下「**[!UICONTROL 儲存並關閉]**」。

同樣地，若要在資產視圖中的資料夾內同時核准多項資產：

1. 選取資產，然後按一下「**[!UICONTROL 大量中繼資料編輯]**」。

1. 在右側面板「[!UICONTROL 屬性]」區段內提供的「**[!UICONTROL 狀態]**」欄位中，選取「**[!UICONTROL 已核准]**」。

1. 按一下「**[!UICONTROL 儲存]**」。


+++

+++**如何確保資產傳遞和 Dynamic Media OpenAPI 的搜尋？**

Experience Manager 的中央資產控管可讓 DAM 管理員或品牌經理管理對資產的存取權。他們可以透過設定角色，或在製作端 (特別是 AEM as a Cloud Service 作者執行個體上) 設定已核准資產的啟用和停用時間，藉此限制存取權。

搜尋或使用傳遞 URL 的一般使用者，在成功通過授權流程後即可取得對限制資產的存取權。

如需更多資訊，請參閱[限制存取 Experience Manager 中的資產](restrict-assets-delivery.md#authoring)。

+++

+++**如何取得編輯資產核准狀態的權限？**

身為 DAM 使用者，您可能沒有[核准資產](approve-assets.md#approve-assets)的權限。若要取得編輯資產核准狀態的權限，管理員可以編輯套用至資產資料夾的預設或任何其他中繼資料結構，藉此提供對「**[!UICONTROL 核准狀態]**」欄位的編輯權限。如需更多資訊，請參閱[如何停用「核准狀態」欄位的編輯](approve-assets.md#configuration)。

+++

+++**支援的影片檔案大小為何？**

具有 OpenAPI 功能的 Dynamic Media 支援長格式影片。影片可支援高達 50 GB 和 2 小時。

+++

+++**具有 OpenAPI 功能的 Dynamic Media 與 Dynamic Media 解決方案有何不同？**

具有 OpenAPI 功能的 Dynamic Media 和 Dynamic Media 代表不同的解決方案，每個解決方案都提供其專門的傳遞功能。必須徹底檢閱您的特定要求，才能確定最適合您需求的解決方案。

Adobe 的一般指引是將具有 OpenAPI 堆疊的 Dynamic Media 用於執行任何整合使用案例 (第一方或第三方應用程式)。如果已經有與 Dynamic Media 堆疊的整合，建議不要變更它，因為 OpenAPI 堆疊 URL 的結構不同。請僅針對全新的整合使用案例來運用 OpenAPI 堆疊。如果您的使用案例需要的是 OpenAPI 堆疊無法提供的進階修飾元，則在 Adobe 消弭此差距之前，請避免使用 OpenAPI 堆疊。即使是 AEM Assets Cloud Services 的基礎原生傳遞，只要您的使用案例涵蓋 OpenAPI 堆疊提供的修飾元，就可以評估 OpenAPI 堆疊。總之，視您使用案例的性質而定，Dynamic Media 和具有 OpenAPI 堆疊的 Dynamic Media 可以共存。

以下是具有 OpenAPI 功能的 Dynamic Media 與 Dynamic Media 之間的一些主要差異：

| 具有 OpenAPI 功能的 Dynamic Media | Dynamic Media |
|---|---|
| [僅適用於 Assets as a Cloud Service](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | 也可以搭配內部部署或 Adobe Managed Services 使用，但需要額外的設定和佈建步驟。 |
| [有限的影像修飾元支援，例如寬度、高度、旋轉、翻轉、品質和格式](/help/assets/deliver-assets-apis.md) | 豐富的可用影像修飾元 |
| [根據使用者、角色、日期和時間來限制資產傳遞](/help/assets/restrict-assets-delivery.md) | 所有使用者都可以存取發佈到 Dynamic Media 的資產 |
| 大多數的開發人員都熟悉 OpenAPI 規格。透過使用[微前端資產選擇器](/help/assets/overview-asset-selector.md)，AEM Assets 的可擴充性就變得相當簡單。 | SOAP 型的 API 會成為開發整合自訂時的阻礙。 |
| 對 DAM 中已核准資產所做的任何變更 (包括版本更新和中繼資料修改)，都會自動反映在傳遞 URL 中。透過內容傳遞網路為具有 OpenAPI 功能的 Dynamic Media 設定 10 分鐘的短存留時間 (TTL) 值，更新就會在 10 分鐘內顯示於所有製作中和已發佈的介面中。 | 建議的內容傳遞網路 TTL 為 10 小時。您可以使用快取失效動作來覆寫 TTL 值。 |
| 只有已核准的資產才能傳遞到下游應用程式，進而在數位體驗中啟用品牌核准的資產。 | 對於 Dynamic Media 已發佈資產的任何更新都會自動發佈，無需任何核准工作流程，因此無法確保數位體驗中的品牌核准資產。 |
| 以傳遞資產數量為依據的使用情況報告。此功能即將推出。 | 使用情況報告尚無法使用。此功能即將推出。 |
| Assets as a Cloud Service 存放庫中標記為過期的資產，無法再提供下游應用程式使用。 | 沒有固有的資產到期時間。資產從 AEM as a Cloud Service 存放庫中刪除之前，會一直保持公開狀態。 |
| 不支援影像預設集和影片智慧裁切功能。 | 支援影像預設集和影片智慧裁切功能。 |
| Dynamic Video 編碼，可確保根據輸入的影片提供最佳編碼。原生影片傳遞不需要任何設定。 | 標準 3 編碼與輸入影片無關 (可能會影響影片傳遞效能)。您需要針對不同的影片位元率來手動設定不同的編碼。 |
| 很難猜測資產 UID 型的 URL (啟用 URL 混淆)，但已將 SEO 最佳化。 | URL 模糊化僅適用於 URL 查詢參數。URL 中的資產 ID (資產名稱) 是可識別的。 |

+++

+++**具有 OpenAPI 功能的 Dynamic Media 如何解決已連線資產功能的限制？**

下列表格概述了兩種解決方案之間的主要區別：

| 具有 OpenAPI 功能的 Dynamic Media | 已連線資產 |
|---|---|
| 遠端 DAM 部署上的資產可在 AEM as a Cloud Service 上使用。 | 遠端 DAM 部署上的資產可在 AEM as a Cloud Service 或 Adobe Managed Services 上使用。 |
| 遠端 DAM 部署上的資產可用於 AEM Sites 執行個體時，不會複製資產二進位檔案。 | 遠端 DAM 部署上的資產可用於 AEM Sites 執行個體時，會複製資產二進位檔案。 |
| 支援 AEM Assets 所支援的所有資產格式類型。 | 不支援影片。 |
| 您可以在本機 Sites 部署上使用 Dynamic Media，同時從遠端 DAM 部署擷取資產。 | 本機 Sites 部署上的 Dynamic Media 是唯讀的。 |
| 連線到遠端 DAM 部署的 AEM Sites 執行個體數量沒有限制。您可以透過為遠端 DAM 上已核准的資產設定角色，以[限制對 Sites 執行個體上資產的存取權](/help/assets/restrict-assets-delivery.md)。 | 限制連線到遠端 DAM 部署的 AEM Sites 執行個體不得超過 4 個。增加數量需要執行額外測試。 |
| 資產選擇器和具有 OpenAPI 功能的 Dynamic Media 均可擴展以允許自訂整合。 | 已連線資產 API 無法進行擴展，因此無法允許自訂整合。 |
| 對於遠端 DAM 部署上可用之已核准資產所做的任何變更 (包含版本更新和中繼資料修改)，都會在 10 分鐘的短存留時間 (TTL) 值內自動反映在 Sites 執行個體上。 | 遠端 DAM 部署上的資產更新是透過生命週期事件自動處理，但與具有 OpenAPI 功能的 Dynamic Media 相比之下，會需要更多時間。 |
| 遠端 DAM 上的資產中繼資料也可以在 AEM Sites 執行個體上使用。 | 遠端 DAM 上的資產中繼資料在 AEM Sites 執行個體上無法使用。 |

+++
