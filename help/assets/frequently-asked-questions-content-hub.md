---
title: Content Hub 常見問題 (FAQ)
description: 了解一些 Content Hub 最常見問題 (FAQ) 的答案。
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: ht
source-wordcount: '1669'
ht-degree: 100%

---

# Content Hub 常見問題 {#content-hub-frequently-asked-questions}

![Content Hub 常見問題](assets/content-hub-faqs.png)

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

## 為什麼我在資產卡上沒有看到「使用 Adobe Express 編輯」選項，以便我能夠混編資產以建立新的變化版本？ {#edit-using-express-not-available}

若要在資產卡上檢視「**使用 Adobe Express 編輯**」選項，除了擁有 [Content Hub 使用者的權限 (有權將資產混編為新的變化版本)](#onboard-content-hub-users-add-assets) 之外，使用者還必須擁有 Adobe Express 企業版或團隊版權益 (請參閱[計劃](https://www.adobe.com/tw/express/pricing))。

對於如何將使用者指派至 [!DNL Content Hub] 和 [!DNL Adobe Express]，有以下幾種設定：

1. 組織擁有 [Assets Ultimate](/help/assets/assets-ultimate-overview.md) 或 [Assets Prime](/help/assets/assets-prime.md) 授權，並且在 Admin Console 中將使用者指派至包含 Adobe Express 權益 (協作者或進階使用者) 的其中一個 Experience Manager 設定檔。此整合無需任何額外設定即可運作。

1. [!DNL Adobe Express] 與含有 [!DNL Content Hub] 的 [!DNL Experience Manager Assets] 是部署在同一個 [!DNL Adobe Admin Console] 中。此整合無需任何額外設定即可運作。

1. [!DNL Adobe Express] 與含有 [!DNL Content Hub] 的 [!DNL Experience Manager Assets] 是部署在不同的 [!DNL Adobe Admin Console] 中。在這種情況下，[!DNL Assets] 管理員可以設定整合 (請參閱[說明文件](/help/assets/connect-assets-with-creative-cloud.md)) 以使整合正常運作。

   >[!NOTE]
   >
   >在兩個 Admin Console 中都指派至 Express 和 Assets 產品設定檔的使用者必須具有相同的電子郵件地址，並使用&#x200B;**企業或學校**&#x200B;帳戶，而不是&#x200B;**個人**&#x200B;帳戶。理想的設定是將兩個 Admin Consoles 都設定為 **Federated ID**，並在它們之間建立信任關係，讓使用者擁有順暢的單一登入體驗。有些 Express 計劃 (例如 Express 團隊版) 不支援 Federated ID/單一登入。

除了正確的產品權益外，Content Hub 中的 Adobe Express 整合還會要求被指派的使用者至少對支援 Content Hub 的 Assets 製作環境擁有「[!UICONTROL 可以編輯]」權限，並且至少在 **[#UICONTROL /content/dam/hydrated-assets/]** 資料夾階層中擁有該權限，以便 Content Hub 使用者在其中儲存使用 Express 製作的內容。請參閱「管理員」檢視 (觸控式 UI) 中的[權限管理](/help/security/touch-ui-principal-view.md)或[「資產」檢視中簡化的權限管理](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions)。

## 我可以設定 Content Hub，以便本組織的品牌指導方針在首頁上顯示為連結嗎？ {#content-hub-setup-brand-guidelines}

除了 Content Hub 首頁上標準的「所有資產」、「集合」和「分析」索引標籤之外，您還可以新增自訂連結作為單獨的索引標籤。如需有關如何進行設定的資訊，請參閱[自訂連結](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub)。

## 是否有任何關於將現有的 Brand Portal 客戶遷移到 Content Hub 的計畫？ {#migration-brand-portal}

Adobe 提供從 Brand Portal 到 Content Hub 的遷移支援，您可以透過建立 Adobe 支援服務單來使用該支援。

## 為什麼我在 Content Hub 中看不到「產品設定/設定」選項？ {#ui-configuration-option-missing}

若要存取[「設定」使用者介面](/help/assets/configure-content-hub-ui-options.md)，您必須是 [Content Hub 管理員](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator)。如果您獲指派至 Adobe Admin Console 中生產作者執行個體上的 AEM 管理員產品設定檔，但仍看不到設定選項，請確定 AEM 管理員產品設定檔未被重新命名。如需更多詳細資訊，請參閱 [AEM as a Cloud Service 團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md)。

## Content Hub 如何解決 Brand Portal 的限制？ {#content-hub-brand-portal-comparison}


下列表格概述兩種解決方案之間的主要差異：

| 區域 | 功能 | Content Hub | Brand Portal |
|---|---|----|----|
| 設定發佈體驗 | 設定篩選器、資產詳細資訊憶及新增資產頁面的後設資料 | ✓ | − |
|  | 從入口網站設定外部連結 | ✓ | − |
|  | 設定橫幅傳送訊息 | ✓ | ✓ |
|  | 設定品牌化的橫幅影像 | ✓ | ✓ |
|  | 按品牌化要求設定使用者介面的主要和次要顏色 | ✓ | − |
| 共用 DAM 中的資產 | 共用 DAM 原始核准的資產 | ✓ | ✓ |
|  | 核准的資產變更會自動同步 | ✓ | − |
| 搜尋和篩選 | 動態篩選器 (根據顯示的資產動態顯示選項) | ✓ | − |
|  | 搜尋歷史記錄 | ✓ | − |
| 資產上傳 | 本機磁碟 | ✓ | ✓ |
|  | 上傳資產時新增可設定的後設資料 | ✓ | − |
| 下載和轉譯 | 下載原始資產 | ✓ | ✓ |
|  | 從 DAM 共用和下載靜態轉譯 | ✓ | ✓ |
|  | 下載動態轉譯 (預設和智慧裁切) | ✓ | ✓ |
|  | 限制檢視和下載過期資產的功能 | ✓ | − |
| 連結共用和集合 | 已登入使用者的連結共用 | ✓ | ✓ |
|  | 公用集合 | ✓ | ✓ |
|  | 在集合內搜尋 | ✓ | − |
|  | 匿名連結共用 | ✓ | ✓ |
|  | 私有集合 | ✓ | ✓ |
| 權限 | ACL 型權限 | − | ✓ |
|  | 屬性型存取控制 | ✓ | − |
| Express 整合 | 在 Adobe Express 中編輯 Content Hub Assets 並儲存至 DAM | ✓ | − |
| 儀表板和報告 | 深入分析儀表板 | ✓ | − |
| 使用者介面擴展性 | 在資產詳細資訊頁面自訂擴展點 | 限量開放使用 | − |
| 即將推出的創新 | 使用者最愛的集合 | ✓ | − |
|  | 管理員釘選的集合 | ✓ | − |
|  | 語意搜尋 | ✓ | − |
|  | 本地化搜尋和後設資料顯示 | ✓ | − |

## 如何選取一個存放庫來檢視僅限所選取環境的資產？ {#select-repository-multiple-environments}

當您設定 Content Hub 供生產環境使用及設定其他較低階環境供相同方案使用時，可以選取存放庫並顯示所選取環境的資產。執行以下步驟：

1. 按一下右側窗格中的使用者圖示。

1. 在「**[!UICONTROL 產品設定]**」區段，選取「**[!UICONTROL 選取存放庫]**」。

1. 從「**[!UICONTROL 存放庫]**」下拉式選單中選取存放庫並按一下「**[!UICONTROL 確定]**」確認。

   Content Hub 現在顯示所選取環境的資產。

## Content Hub 如何顯示 .ZIP 檔案類型的縮圖預覽？ {#thumbnail-preview-zip-file}

若要在 Content Hub 中為 .ZIP 等檔案類型提供縮圖預覽，您可以新增名為 `cq5dam.preview.jpg` 或者 `cq5dam.preview.png` 的轉譯到路徑的根目錄，在那裡的 AEM as a Cloud Service 製作環境中可用 .ZIP。

您新增的作為轉譯的影像：

* 可以是 JPG、JPEG 或 PNG 格式。

* 必須小於 50MB

可用時，Content Hub 上 .ZIP 檔案的預覽縮圖便會顯示該影像。


