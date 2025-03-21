---
title: Content Hub 常見問題 (FAQ)
description: 了解一些 Content Hub 最常見問題 (FAQ) 的答案。
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 97%

---

# Content Hub 常見問題 {#content-hub-frequently-asked-questions}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets與Edge Delivery Services整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用Dynamic Media Prime和Ultimate</b></a>
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

![Content Hub 常見問題](assets/content-hub-faqs.png)

>[!AVAILABILITY]
>
>現已提供 PDF 格式的 Content Hub 指南。下載完整指南，並使用 Adobe Acrobat AI 助理來回答您的查詢問題。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

## 什麼是 Content Hub？ {#what-is-content-hub}

Content Hub 是 Adobe Experience Manager Assets as a Cloud Service 的一項功能。

Content Hub 可讓更廣泛的團隊透過直覺的入口網站，輕鬆發現相關且經核准的資產，並快速根據需求加以調整。此外，Content Hub 提供了一種攝取機制，可讓使用者將資產上傳至 DAM 時，能夠輕鬆地自助進行。這直接滿足了組織對於加快內容建立速度的需求，同時保持品牌一致性，並遵守適當的保護措施。

## 為什麼我無法在 Cloud Manager 程式/環境中啟用 Content Hub？ {#cannot-enable-content-hub}

Content Hub 目前僅適用於含有 Assets 授權 (Assets Cloud Service、Assets Ultimate、Assets Prime) 的 AEM Cloud Manager Production 方案。當您點按並啟用 [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) 時，系統會加以部署，並與該程式中 AEM 的編寫生產環境建立關聯。請參閱[部署 Content Hub](/help/assets/deploy-content-hub.md) 以了解詳細資訊和先決條件。

## 我在生產程式/環境中啟用了 Content Hub，我可以停用它嗎？ {#can-i-disable-content-hub}

在生產程式上啟用 Content Hub 會將其部署為生產基礎結構的一部分。AEM Cloud Manager 不允許移除或停用生產基礎結構，藉此盡量降低人為錯誤對生產使用帶來的風險。

如果您不希望部署完畢後為使用者提供 Content Hub，則請不要在 Admin Console 中將任何使用者指派至 Content Hub 產品設定檔。請參閱[部署 Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) 以了解詳細資訊。

## 如果 Content Hub 僅適用於生產程式/生產製作環境，我該如何評估組織中的 Content Hub？ {#how-can-i-evaluate-content-hub}

Content Hub 是 Adobe 提供和維護的功能，沒有任何需要透過開發/中繼/生產進行典型驗證的自訂程式碼。此外，使用者對該功能的存取權完全由管理員控制，因此您可以對其進行評估，而無需將其向所有使用者開放。

可以在不影響 AEM as a Cloud Service Assets 中管理之使用者/生產內容的情況下評估 Content Hub。評估程序可能如下所示：

* 在生產環境中[啟用 Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) (Cloud Manager 程式)
* 從生產作者[新增 AEM 管理員使用者](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator)至 Content Hub 產品設定檔。
* AEM 管理員[設定 Content Hub](/help/assets/configure-content-hub-ui-options.md)
* AEM 管理員或 AEM 生產作者上的 AEM 使用者會[核准 Content Hub 的多項資產](/help/assets/approve-assets-content-hub.md)；若您不想變更 DAM 中的任何生產內容，就可能需要在 AEM 作者執行個體中建立單獨的評估資料夾，並將 DAM 中的一些資產上傳/標記或複製到其中。
* Admin Console 管理員會將[一些選定的使用者](/help/assets/deploy-content-hub.md#onboard-content-hub-users)新增到 Content Hub 產品設定檔，以便他們開始評估。
* 評估完成後，作者執行個體中的 AEM 使用者可以移除測試資產的核准、為 Content Hub 核准生產資產，然後 Admin Console 管理員可以新增所有需要存取 Content Hub 和已核准內容的使用者。恭喜，您的 Content Hub 現已上線。

在沙箱程式或其編寫生產環境中有一項 Content Hub 的搶先體驗方案。如需更多資訊，請參閱[沙箱程式簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。若要了解有關搶先體驗方案的詳細資訊，請聯絡您的 Adobe 客戶團隊。

Content Hub 目前尚不適用於非生產環境 (中繼和開發)。Assets Ultimate 的中繼/開發環境預計將於 2025 年 3 月推出。

## 為什麼我登入 Content Hub 後看不到任何資產？ {#no-assets-in-content-hub}

在 Assets as a Cloud Service 中標記為已核准的資產會自動出現在 Content Hub 中。如果您登入 Content Hub 後看不到任何資產，請使用 AEM as a Cloud Service 編寫環境核准資產，使其出現在 Content Hub 中。如需更多資訊，請參閱[為 Content Hub 核准資產](/help/assets/approve-assets-content-hub.md)。

## 為什麼我看不到直接使用 Content Hub 上傳或是使用 Content Hub 從 Dropbox 或 OneDrive 帳戶匯入的資產？ {#no-assets-uploaded-from-content-hub}

使用 Content Hub 上傳的資產是否會顯示取決於您是否啟用了「設定」介面上的[自動核准](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub)切換開關：

* 如果啟用&#x200B;**自動核准**&#x200B;切換開關，您使用 Content Hub 上傳的資產則會自動顯示。

* 如果停用&#x200B;**自動核准**&#x200B;切換開關，您使用 Content Hub 上傳的資產就不會自動顯示。這些資產會顯示在您 Assets as a Cloud Service 環境的 `hydrated-assets` 資料夾中。導覽至該資料夾，並將資產狀態[大量編輯](/help/assets/approve-assets-content-hub.md)為 `Approved`，使資產顯示於 Content Hub 中。

## 如何在 AEM as a Cloud Service 環境中快速找到使用 Content Hub 上傳的資產？ {#find-uploaded-assets-on-aem-cloud}

您可透過以下方法，在 AEM as a Cloud Service 環境中快速找到使用 Content Hub 上傳的資產：

1. 導覽至 `hydrated-assets` 資料夾。

1. 按一下「**[!UICONTROL 篩選器]**」，並將「**[!UICONTROL 資產狀態]**」欄位設定為「**[!UICONTROL 無狀態]**」。

1. 使用「**[!UICONTROL 修改日期]**」欄位對資產進行排序。

## 為什麼我不能使用資產卡片上的 Adobe Express 選項來檢視編輯內容，藉此混編資產以建立新的變化版本？ {#edit-using-express-not-available}

若要使用資產卡片上的 Adobe Express 選項來檢視編輯內容，除了 [Content Hub 使用者的權限 (有權將資產混編為新的變化版本)](#onboard-content-hub-users-add-assets) 之外，您還必須擁有 Adobe Express 授權。Adobe Express 必須部署在與 Adobe Experience Manager 部署位置相同之 Adobe Admin Console 的組織中。

## 我可以設定 Content Hub，以便本組織的品牌指導方針在首頁上顯示為連結嗎？ {#content-hub-setup-brand-guidelines}

除了 Content Hub 首頁上標準的「所有資產」、「集合」和「分析」索引標籤之外，您還可以新增自訂連結作為單獨的索引標籤。如需有關如何進行設定的資訊，請參閱[自訂連結](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub)。

## 是否有任何關於將現有的 Brand Portal 客戶遷移到 Content Hub 的計畫？ {#migration-brand-portal}

Adobe 提供從 Brand Portal 到 Content Hub 的遷移支援，您可以透過建立 Adobe 支援服務單來使用該支援。

## 為什麼我在 Content Hub 中看不到「產品設定/設定」選項？ {#ui-configuration-option-missing}

若要存取[「設定」使用者介面](/help/assets/configure-content-hub-ui-options.md)，您必須是 [Content Hub 管理員](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator)。如果您獲指派至 Adobe Admin Console 中生產作者執行個體上的 AEM 管理員產品設定檔，但仍看不到設定選項，請確定 AEM 管理員產品設定檔未被重新命名。如需更多詳細資訊，請參閱 [AEM as a Cloud Service 團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md)。
