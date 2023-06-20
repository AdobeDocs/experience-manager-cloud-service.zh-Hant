---
title: 使用「連線資產」在 中共用 DAM 資產 [!DNL Sites]
description: 使用遠端可用的資產 [!DNL Adobe Experience Manager Assets] 在另一個網頁上建立您的網頁時部署 [!DNL Adobe Experience Manager Sites] 部署。
contentOwner: AK
mini-toc-levels: 2
feature: Asset Management,Connected Assets,Asset Distribution,User and Groups
role: Admin,User,Architect
exl-id: 2346f72d-a383-4202-849e-c5a91634617a
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '3829'
ht-degree: 16%

---


# 使用「連線資產」在 中共用 DAM 資產 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html) |
| AEM as a Cloud Service  | 本文 |

大型企業中，建立網站所需的基礎架構可能很分散。有時候，建立這些網站的網站建立功能和數位資產可能會存放在不同的部署中。其中一個原因可能是地理上分散的現有部署需要協同工作。 另一個原因可能是收購導致基礎架構迥異，包括不同的 [!DNL Experience Manager] 版本，母公司想要一起使用的版本。

「連線資產」功能可透過整合以下專案支援上述使用案例 [!DNL Experience Manager Sites] 和 [!DNL Experience Manager Assets]. 使用者可以在以下位置建立網頁： [!DNL Sites] 使用來自不同資產的數位資產 [!DNL Assets] 部署。

>[!NOTE]
>
>只有在您需要使用遠端DAM部署上可用的資產（位於單獨的Sites部署上）來製作網頁時，才需設定「連線資產」。

## 連線資產概觀 {#overview-of-connected-assets}

在中編輯頁面時 [!UICONTROL 頁面編輯器] 作為目標目的地，作者可從不同來源順暢地搜尋、瀏覽及內嵌資產 [!DNL Assets] 作為資產來源的部署。 管理員會建立部署的一次性整合 [!DNL Experience Manager] 替換為 [!DNL Sites] 另一個部署的功能 [!DNL Experience Manager] 替換為 [!DNL Assets] 功能。 您也可以透過「連線資產」，在網站的網頁中使用Dynamic Media影像，並使用Dynamic Media功能，例如智慧型裁切和影像預設集。

對於 [!DNL Sites] 作者，遠端資產會以唯讀本機資產形式提供。 此功能可支援順暢搜尋及存取「網站編輯器」上的遠端資產。 若有任何其他使用案例，需要完整的資產語料庫才能在Sites上使用，請考慮大量移轉資產，而非運用連線資產。

### 先決條件和支援的部署 {#prerequisites}

使用或設定此功能之前，請先確定下列事項：

* 使用者是每個部署中適當使用者群組的一部分。
* 對象 [!DNL Adobe Experience Manager] 部署型別，即符合其中一個支援的條件。 [!DNL Experience Manager] as a Cloud Service [!DNL Assets] 搭配使用 [!DNL Experience Manager] 6.5.如需此功能如何運作的詳細資訊，請參閱 [!DNL Experience Manager] 6.5，請參閱 [中的連線資產 [!DNL Experience Manager] 6.5 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html).

  | | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5 [!DNL Sites] 在AMS上 | [!DNL Experience Manager] 6.5 [!DNL Sites] 內部部署 |
  |---|---|---|---|
  | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | 支援 | 支援 | 支援 |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] 在AMS上** | 支援 | 支援 | 支援 |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] 內部部署** | 不支援 | 不支援 | 不支援 |

### 支援的檔案格式 {#mimetypes}

作者在「內容尋找器」中搜尋影像和下列型別的檔案，並在「頁面編輯器」中拖曳搜尋的資產。 檔案將新增至 `Download` 元件和影像移至 `Image` 元件。 作者也可以在任何自訂內容中新增遠端資產 [!DNL Experience Manager] 延伸預設值的元件 `Download` 或 `Image` 元件。 支援的格式包括：

* **影像格式**：此變數的 [影像元件](file-format-support.md#image-formats) 支援。
* **檔案格式**：請參閱 [支援的檔案格式](file-format-support.md#document-formats).

### 相關使用者和群組 {#users-and-groups-involved}

以下說明設定和功能及其對應使用者群組時涉及的各種角色。 本機範圍適用於作者建立網頁的使用案例。 遠端範圍適用於託管所需資產的 DAM 部署。此 [!DNL Sites] 作者會擷取這些遠端資產。

| 角色 | 範圍 | 使用者群組 | 說明 |
|------|--------|-----------|----------|
| [!DNL Sites] 管理員 | 本機 | [!DNL Experience Manager] `administrators` | 設定 [!DNL Experience Manager] 並設定與遠端裝置的整合 [!DNL Assets] 部署。 |
| DAM 使用者 | 本機 | `Authors` | 用於檢視及複製 `/content/DAM/connectedassets/` 中擷取的資產。 |
| [!DNL Sites] 作者 | 本機 | <ul><li>`Authors` （具有遠端DAM上的讀取存取權和本機上的作者存取權） [!DNL Sites]) </li> <li>`dam-users` 在本機 [!DNL Sites]</li></ul> | 一般使用者為 [!DNL Sites] 使用此整合改善內容速度的作者。 作者可以使用在遠端DAM中搜尋和瀏覽資產 [!UICONTROL 內容尋找器] 並在本機網頁中使用所需的影像。 |
| [!DNL Assets] 管理員 | 遠端 | [!DNL Experience Manager] `administrators` | 設定跨原始資源共用 (CORS)。 |
| DAM 使用者 | 遠端 | `Authors` | 作者 遠端角色 [!DNL Experience Manager] 部署。 在「連線資產」中使用搜尋和瀏覽資產 [!UICONTROL 內容尋找器]. |
| DAM 經銷商 (技術使用者) | 遠端 | <ul> <li> [!DNL Sites] `Authors`</li> <li> `connectedassets-assets-techaccts` </li> </ul> | 遠端部署上的這個使用者使用者 [!DNL Experience Manager] 本機伺服器(非 [!DNL Sites] 作者角色)，代表取得遠端資產 [!DNL Sites] 作者。 |
| [!DNL Sites] 技術使用者 | 本機 | `connectedassets-sites-techaccts` | 允許 [!DNL Assets] 部署，以搜尋中資產的參考 [!DNL Sites] 網頁。 |

### 連線資產架構 {#connected-assets-architecture}

Experience Manager可讓您將遠端DAM部署作為來源連線到多個Experience Manager [!DNL Sites] 部署。 不過，您可以連線 [!DNL Sites] 僅使用一個遠端DAM部署的部署。

評估要連線至遠端DAM部署的最佳Sites執行個體數量。 Adobe建議逐步將Sites執行個體連線至部署，並測試遠端DAM的效能不受影響，因為每個已連線的Sites執行個體都會對遠端DAM上的資料流量造成影響。

下列圖表說明支援的情況：

![連線資產架構](assets/connected-assets-architecture.png)

下圖說明一個不支援的情況：

![連線資產架構](assets/connected-assets-architecture-unsupported.png)

## 設定之間的連線 [!DNL Sites] 和 [!DNL Assets] 部署 {#configure-a-connection-between-sites-and-assets-deployments}

一個 [!DNL Experience Manager] 管理員可建立此整合。 建立後，系統會透過使用者群組建立使用所需的許可權。 使用者群組定義於 [!DNL Sites] 部署和DAM部署。

設定連線資產和本機 [!DNL Sites] 連線能力，請遵循下列步驟：

1. 存取現有的 [!DNL Sites] 部署。 此 [!DNL Sites] 部署用於網頁製作，例如 `https://<sites_server_fqdn>:[port]`. 當頁面製作於以下日期進行時： [!DNL Sites] 部署，呼叫 [!DNL Sites] 從頁面編寫的角度來看，部署為本機。

1. 存取現有的 [!DNL Assets] 部署。 此 [!DNL Assets] 部署用於管理數位資產，例如 `https://[assets_servername]:port`.

1. 確定具有適當範圍的使用者和角色存在於 [!DNL Sites] 部署和 [!DNL Assets] 在AMS上部署。 建立技術使用者： [!DNL Assets] 部署和新增至中提到的使用者群組 [相關使用者和群組](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. 存取本機 [!DNL Sites] 部署位置 `https://[sites_servername]:port`. 按一下&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 連線資產設定」]**，並提供下列各值：

   1. A **[!UICONTROL 標題]** 設定的。
   1. **[!UICONTROL 遠端DAM URL]** 為的URL [!DNL Assets] 位置格式 `https://[assets_servername]:[port]`.
   1. DAM 經銷商 (技術使用者) 的認證。
   1. 在 **[!UICONTROL 掛接點]** 欄位，輸入本機 [!DNL Experience Manager] 路徑，其中 [!DNL Experience Manager] 擷取資產。 例如，`connectedassets` 資料夾。從DAM擷取的資產會儲存在上的此資料夾中， [!DNL Sites] 部署。
   1. **[!UICONTROL 本機站台URL]** 是的位置 [!DNL Sites] 部署。 [!DNL Assets] 部署使用此值來維護對此擷取的數位資產的參考 [!DNL Sites] 部署。
   1. 認證： [!DNL Sites] 技術使用者。
   1. 的值 **[!UICONTROL 原始二進位傳輸最佳化臨界值]** 欄位會指定是否同步傳輸原始資產（包括轉譯）。 檔案大小較小的資產可立即擷取，而檔案大小相對較大的資產最好非同步處理。 該值取決於您的網路功能。
   1. 選取 **[!UICONTROL 與連線資產共用的資料存放區]**，如果您使用資料存放區來儲存資產，且資料存放區在兩個部署之間共用。 在此情況下，臨界值限制並不重要，因為資料存放區上有可用的實際資產二進位檔，而且不會轉移。

   ![連線資產功能的典型設定](assets/connected-assets-typical-config.png)

   *圖：連線資產功能的典型設定。*

1. 上的現有數位資產 [!DNL Assets] 已經處理部署並產生轉譯。 這些轉譯會使用此功能來擷取，因此不需要重新產生轉譯。 停用工作流程啟動器，以防止重新產生轉譯。 調整上的啟動器設定([!DNL Sites])部署，以排除 `connectedassets` 資料夾（在此資料夾中擷取資產）。

   1. 開啟 [!DNL Sites] 部署，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 啟動器]**.

   1. 搜尋將 **[!UICONTROL DAM 更新資產]**&#x200B;和 **[!UICONTROL DAM 中繼資料回寫]**&#x200B;設為工作流程的啟動器。

   1. 選取工作流程啟動器，然後按一下動作列上的&#x200B;**[!UICONTROL 「屬性」]**。

   1. 在 [!UICONTROL 屬性] 精靈，變更 **[!UICONTROL 路徑]** 欄位做為下列對應，以更新其規則運算式來排除掛接點 **[!UICONTROL connectedassets]**.

   | 變更前 | 變更後 |
   | ------ | ------------ |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >作者擷取資產時，會擷取遠端 部署上可用的所有轉譯項目。若要針對所擷取的資產建立更多轉譯項目，請略過此設定步驟。此 [!UICONTROL DAM更新資產] 工作流程會觸發，並建立更多轉譯。 這些轉譯僅在本機提供 [!DNL Sites] 部署，而不是在遠端DAM部署上。

1. 新增 [!DNL Sites] 部署為CORS設定中允許的原點 [!DNL Assets] 部署。 如需詳細資訊，請參閱 [瞭解CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. 設定 [相同網站Cookie支援](/help/security/same-site-cookie-support.md).

您可以檢查已設定的 [!DNL Sites] 部署和 [!DNL Assets] 部署。

![已設定連線資產的連線測試 [!DNL Sites]](assets/connected-assets-multiple-config.png)
*圖：已設定連線資產的連線測試 [!DNL Sites].*

<!-- TBD: Check if Launchers are to be disabled on CS instances. Is this option even available to the users on CS? -->

## 使用Dynamic Media資產 {#dynamic-media-assets}


使用「連線資產」，您可以使用由下列專案處理的影像資產： [!DNL Dynamic Media] 從Sites頁面上的遠端DAM部署，並使用Dynamic Media功能，例如智慧型裁切和影像預設集。

使用 [!DNL Dynamic Media] 連線資產：

1. 設定 [!DNL Dynamic Media] 在已啟用同步模式的遠端DAM部署上。
1. 設定 [連線資產](#configure-a-connection-between-sites-and-assets-deployments).
1. 設定 [!DNL Dynamic Media] （在遠端DAM上設定的相同公司名稱的Sites執行個體上）。 Sites部署必須擁有Dynamic Media帳戶的唯讀存取權，才能使用連線的資產。 因此，請務必在Sites例項的Dynamic Media設定中停用同步模式。

>[!CAUTION]
>
>使用連線資產和 [!DNL Dynamic Media] 設定，您無法使用 [!DNL Dynamic Media] 以處理上可用的本機資產 [!DNL Sites] 部署。

## 設定 [!DNL Dynamic Media] {#configure-dynamic-media}

進行設定 [!DNL Dynamic Media] 於 [!DNL Assets] 和 [!DNL Sites] 部署：

1. 如上所述建立「連線資產」設定，除了設定功能時，請選取「 」 **[!UICONTROL 擷取Dynamic Media連線資產的原始轉譯]** 選項。

1. 設定 [!DNL Dynamic Media] 在本機 [!DNL Sites] 和遠端 [!DNL Assets] 部署。 依照指示進行 [設定 [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

   * 在所有設定中使用相同的公司名稱。
   * 在本機 [!DNL Sites]，在 [!UICONTROL Dynamic Media同步模式]，選取 **[!UICONTROL 預設為停用]**. 此 [!DNL Sites] 部署必須擁有對的唯讀存取權 [!DNL Dynamic Media] 帳戶。
   * 在本機 [!DNL Sites]，在 **[!UICONTROL 發佈資產]** 選項，選取 **[!UICONTROL 選擇性發佈]**. 不要選取 **[!UICONTROL 同步所有內容]**.
   * 在遠端 [!DNL Assets] 部署，在 [!UICONTROL Dynamic Media同步模式]，選取 **[!UICONTROL 預設為啟用]**.

1. 啟用 [[!DNL Dynamic Media] 影像核心元件中的支援](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). 此功能會啟用預設值 [影像元件](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html) 以顯示 [!DNL Dynamic Media] 影像： [!DNL Dynamic Media] 作者在本機網頁中使用影像 [!DNL Sites] 部署。

## 使用遠端資產 {#use-remote-assets}

網站作者使用內容尋找器來連線至DAM部署。 作者可以瀏覽、搜尋和拖曳元件中的遠端資產。若要驗證遠端DAM，請備妥管理員提供的認證（如有）。

作者可以在單一網頁中使用本機DAM和遠端DAM部署上可用的資產。 使用「內容尋找器」，以便在搜尋本機 DAM 和搜尋遠端 DAM 之間切換。

系統只會擷取具有完全對應標籤以及相同分類階層（在本機提供）的遠端資產標籤 [!DNL Sites] 部署。 其他所有標籤會一概捨棄。作者可使用遠端上的所有標籤來搜尋遠端資產 [!DNL Experience Manager] 部署，因為它提供全文檢索搜尋。

### 逐步使用說明 {#walk-through-of-usage}

不妨使用上述設定試著編寫體驗，以了解功能的運作方式。在遠端 DAM 部署中使用您所選擇的文件或影像。

1. 導覽至 [!DNL Assets] 存取遠端部署介面 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]** 從 [!DNL Experience Manager] 工作區。 或者，您也可以在瀏覽器中存取 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上傳您選擇的資產。

1. 於 [!DNL Sites] 部署，在右上角的設定檔啟動器中，按一下 **[!UICONTROL 模擬為]**. 指定使用者名稱，選取提供的選項，然後按一下 **[!UICONTROL 確定]**.

1. 開啟 [!DNL Sites] 並編輯頁面。

   按一下頁面左上角的&#x200B;**[!UICONTROL 「切換側面板」]**。

1. 開啟 [!UICONTROL 資產] 索引標籤（遠端內容尋找器）並按一下 **[!UICONTROL 登入「連線資產」]**.

1. 指定要登入「連線資產」的認證。 此使用者對以下兩個專案均具有編寫許可權： [!DNL Experience Manager] 部署。

1. 搜尋您新增至 DAM 的資產。遠端資產會顯示於左側面板。篩選影像或文件，並進一步篩選支援的文件類型。拖曳 `Image` 元件上的影像和 `Download` 元件上的文件。

   擷取的資產在本機上是唯讀的 [!DNL Sites] 部署。 您仍然可以使用您提供的選項 [!DNL Sites] 元件，以編輯所擷取的資產。 由元件進行編輯屬於非破壞性動作。

   ![在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項](assets/filetypes_filter_connected_assets.png)

   *圖：在遠端 DAM 上搜尋資產時，篩選文件類型和影像的選項.*

1. 如果資產的原始檔案是以非同步方式擷取，且擷取任務失敗，網站作者會收到通知。 編寫過程中或甚至在完成編寫之後，作者都可以在以下連結中檢視擷取任務和錯誤的詳細資訊： [非同步作業](/help/operations/asynchronous-jobs.md) 使用者介面。

   ![背景中非同步擷取資產作業的相關通知。](assets/assets_async_transfer_fails.png)

   *圖：背景中非同步擷取資產作業的相關通知。*

1. 發佈頁面時， [!DNL Experience Manager] 顯示頁面上使用之資產的完整清單。 請確認發佈時，系統已成功擷取遠端資產。若要檢查每個已擷取資產的狀態，請參閱 [非同步作業](/help/operations/asynchronous-jobs.md) 使用者介面。

   >[!NOTE]
   >
   >即使有一或多個遠端資產未完全擷取，頁面仍會發佈。 此 [!DNL Experience Manager] 通知區域會顯示通知，指出非同步作業頁面中顯示的錯誤。

>[!CAUTION]
>
>擷取的遠端資產一旦用於網頁中，只要擁有存取本機資料夾的許可權，任何人都可以搜尋和使用。 擷取的資產會儲存在本機資料夾中(`connectedassets` 上述逐步說明)。 這些資產也可供搜尋，並可透過[!UICONTROL 「內容尋找器」]顯示於本機存放庫。

擷取的資產可設為其他任何本機資產以供使用，只是相關聯的中繼資料無法編輯。

### 檢查跨網頁資產的使用情況 {#asset-usage-references}

[!DNL Experience Manager] 可讓DAM使用者檢查資產的所有參考。 它有助於瞭解和管理遠端資產的使用 [!DNL Sites] 和在複合資產中。 上的許多網頁作者 [!DNL Experience Manager Sites] 部署可在不同網頁中使用遠端DAM上的資產。 若要簡化資產管理，避免導致參照損毀，DAM使用者務必要檢查本機及遠端網頁上資產的使用情況。 此 [!UICONTROL 引用] 索引標籤在資產的 [!UICONTROL 屬性] 頁面會列出資產的本機與遠端參考。

若要檢視及管理上的參照 [!DNL Assets] 部署，請遵循下列步驟：

1. 在中選取資產 [!DNL Assets] 主控台並按一下 **[!UICONTROL 屬性]** （從工具列）。
1. 按一下 **[!UICONTROL 引用]** 標籤。 另請參閱 **[!UICONTROL 本機參考]** 以使用上的資產 [!DNL Assets] 部署。 參閱**[!UICONTROL 遠端參考] 用於上的資產 [!DNL Sites] 使用「連線資產」功能擷取資產的部署。

   ![資產「屬性」頁面中的遠端參考](assets/connected-assets-remote-reference.png)

1. 以下專案的參考： [!DNL Sites] 頁面會顯示每個本機的參照總數 [!DNL Sites]. 尋找所有參照並顯示參照總數可能需要一些時間。
1. 參考清單是互動式的，DAM使用者可以按一下參考以開啟參考頁面。 如果由於某種原因無法擷取遠端參照，則會顯示通知，通知使用者失敗。
1. 使用者可以移動或刪除資產。 移動或刪除資產時，所有選定資產/資料夾的參照總數會顯示在警告對話方塊中。 刪除尚未擷取參照的資產時，會顯示警告對話方塊。

   ![強制刪除警告](assets/delete-referenced-asset.png)

### 管理遠端DAM中資產的更新 {#handling-updates-to-remote-assets}

晚於 [設定連線](#configure-a-connection-between-sites-and-assets-deployments) 在遠端DAM和Sites部署之間，遠端DAM上的資產可在Sites部署中使用。 然後，您可以在遠端DAM資產或資料夾上執行更新、刪除、重新命名和移動操作。 這些更新會在Sites部署中自動提供，但會有一些延遲。 此外，如果本機Experience Manager Sites頁面上使用遠端DAM上的資產，則遠端DAM上的資產更新會顯示在Sites頁面上。

將資產從一個位置移動到另一個位置時，請確保 [調整引用](manage-digital-assets.md) 好讓資產顯示在Sites頁面上。 如果您將資產移至無法從本機Sites部署存取的位置，資產就無法顯示在Sites部署上。

您也可以更新遠端DAM上資產的中繼資料屬性，而變更可在本機Sites部署中使用。

Sites作者可以預覽Sites部署上可用的更新，然後重新發佈變更以使其可在AEM發佈執行個體上使用。

Experience Manager顯示 `expired` 遠端Assets內容尋找器中的資產狀態視覺指示器，可阻止網站作者在Sites頁面上使用資產。 如果您使用資產搭配 `expired` 在Sites頁面上的狀態，資產無法顯示在Experience Manager發佈執行個體上。

## 常見問答 {#frequently-asked-questions}

+++**如果您需要使用上可用的資產，您應設定「連線資產」。 [!DNL Sites] 部署？**

在這種情況下，不需要設定「連線資產」。 您可以使用上的可用資產 [!DNL Sites] 部署。

+++

+++**您何時需要設定「連線資產」功能？**

只有在您需要使用上的遠端DAM部署中可用的資產時，才設定「連線資產」功能。 [!DNL Sites] 部署。

+++

+++**您是否可以連線多個 [!DNL Sites] 在設定「連線資產」之後部署到遠端DAM部署？**

是，您可以連線多個 [!DNL Sites] 在設定「連線資產」之後部署到遠端DAM部署。 如需詳細資訊，請參閱 [連線資產架構](#connected-assets-architecture).

+++

+++**您可以連線多少個遠端DAM部署 [!DNL Sites] 在設定「連線資產」之後進行部署？**

您可以將一個遠端DAM部署連線至 [!DNL Sites] 在設定「連線資產」之後進行部署。 如需詳細資訊，請參閱 [連線資產架構](#connected-assets-architecture).

+++

+++**您能否使用來自以下網站的Dynamic Media資產： [!DNL Sites] 在設定「連線資產」之後進行部署？**

設定「連線資產」後， [!DNL Dynamic Media] 資產位於 [!DNL Sites] 以唯讀模式部署。 因此，您無法使用 [!DNL Dynamic Media] 若要處理上的資產，請 [!DNL Sites] 部署。 如需詳細資訊，請參閱 [設定Sites與Dynamic Media部署之間的連線](#dynamic-media-assets).

+++

+++**您能否在上使用遠端DAM部署中的影像和檔案格式型別的資產？ [!DNL Sites] 在設定「連線資產」之後進行部署？**

可以，您可以從遠端DAM部署( )的影像和檔案格式型別資產位於 [!DNL Sites] 在設定「連線資產」之後進行部署。

+++

+++**您能否在上使用遠端DAM部署的內容片段和視訊資產？ [!DNL Sites] 在設定「連線資產」之後進行部署？**

否，您無法使用來自遠端DAM部署的內容片段和視訊資產。 [!DNL Sites] 在設定「連線資產」之後進行部署。

+++

+++**您能否在上使用遠端DAM部署的Dynamic Media資產？ [!DNL Sites] 在設定「連線資產」之後進行部署？**

是，您可以在上從遠端DAM部署設定及使用Dynamic Media影像資產 [!DNL Sites] 在設定「連線資產」之後進行部署。 如需詳細資訊，請參閱 [設定Sites與Dynamic Media部署之間的連線](#dynamic-media-assets).

+++

+++**設定「連線資產」後，您能否對遠端DAM資產或資料夾執行更新、刪除、重新命名和移動操作？**

可以，在設定「連線資產」後，您可以對遠端DAM資產或資料夾執行更新、刪除、重新命名和移動操作。 這些更新會在Sites部署中自動提供，但會有一些延遲。 如需詳細資訊，請參閱 [管理遠端DAM中資產的更新](#handling-updates-to-remote-assets).

+++

+++**設定「連線資產」後，您能否在 [!DNL Sites] 部署，並使其可用於遠端DAM部署？**

您可以將資產新增至 [!DNL Sites] 但是，部署這些資產無法用於遠端DAM部署。

+++


## 限制和最佳實務 {#tip-and-limitations}

* 若要深入瞭解資產使用狀況，請設定 [Assets Insight](/help/assets/assets-insights.md) 上的功能 [!DNL Sites] 執行個體。
* 連線資產不支援在製作元件中使用路徑瀏覽器。

### 許可權與資產管理 {#permissions-and-managing-assets}

* 本機資產為唯讀副本。[!DNL Experience Manager] 元件會對資產執行非破壞性的編輯作業。不允許執行其他編輯作業。
* 本機擷取的資產僅適用於編寫用途。無法套用資產更新工作流程，也無法編輯中繼資料。
* 使用時 [!DNL Dynamic Media] 在 [!DNL Sites] 頁面不會擷取原始資產並儲存在本機部署中。 此 `dam:Asset` 節點、中繼資料和產生的轉譯 [!DNL Assets] 部署全部擷取到 [!DNL Sites] 部署。
* 僅支援影像和列出的文件格式。[!DNL Content Fragments] 和 [!DNL Experience Fragments] 不受支援。
* [!DNL Experience Manager] 不會擷取中繼資料結構。 這表示可能不會顯示所有擷取的中繼資料。 如果結構描述單獨更新於 [!DNL Sites] 部署，則會顯示所有中繼資料屬性。
* 全部 [!DNL Sites] 作者對擷取的副本具有讀取許可權，即使作者無法存取遠端DAM部署。
* 不提供 API 以支援自訂整合。
* 此功能可支援順暢的搜尋作業及使用遠端資產。若要在本機部署中一次提供多個遠端資產，不妨考慮移轉資產。
* 無法使用遠端資產作為上的頁面縮圖 [!UICONTROL 頁面屬性] 使用者介面。 您可以在下列位置設定網頁縮圖： [!UICONTROL 頁面屬性] 來自的使用者介面 [!UICONTROL 縮圖] 按一下 [!UICONTROL 選取影像].

### 設定和授權 {#setup-licensing}

* [!DNL Assets] 部署日期 [!DNL Adobe Managed Services] 支援。
* [!DNL Sites] 可以連線至單一 [!DNL Assets] 一次部署。
* 的授權 [!DNL Assets] 需要作為遠端存放庫使用。
* 的一或多個授權 [!DNL Sites] 需要以本機編寫部署方式工作。

### 使用狀況 {#usage}

* 使用者可在編寫時搜尋遠端資產，並將這些資產拖曳至本機頁面。 不支援其他功能。
* 擷取作業會於 5 秒後逾時。如果有網路或其他方面的問題，作者擷取資產時就可能遇到問題。作者可從以下位置拖曳遠端資產，以重新嘗試： [!UICONTROL 內容尋找器] 至 [!UICONTROL 頁面編輯器].
* 您可以對擷取的資產執行非破壞性的簡單編輯作業，也能執行透過 `Image` 元件支援的編輯工作。資產僅供唯讀。
* 重新擷取資產的唯一方法是將其拖曳至頁面上。 沒有API支援或其他方法可重新擷取資產以進行更新。
* 如果資產從DAM解除委任，這些資產將繼續用於 [!DNL Sites] 頁面。
* 資產的遠端參考專案會以非同步方式擷取。 參考與總計數不是即時的，而且如果 [!DNL Sites] 作者在DAM使用者檢視參考時使用資產。 DAM使用者可以重新整理頁面，並在幾分鐘後重試以取得總計數。

## 疑難排解問題 {#troubleshoot}

若要疑難排解常見錯誤，請遵循下列步驟：

* 如果您無法從搜尋遠端資產， [!UICONTROL 內容尋找器]，然後確定已具備所需的角色和許可權。

* 基於一個或多個原因，從遠端DAM擷取的資產可能不會發佈在網頁上。 遠端伺服器上不存在該檔案，缺乏擷取該檔案的適當許可權，或是網路故障可能是原因。 確保資產沒有從遠端DAM移除。 確保有適當的許可權且符合先決條件。 再次嘗試將資產新增至頁面並重新發佈。 檢查[非同步工作清單](/help/operations/asynchronous-jobs.md)，找出資產擷取作業的錯誤。

* 如果您無法從本機存取遠端DAM部署 [!DNL Sites] 部署，確保允許跨網站Cookie，並且 [相同網站Cookie支援](/help/security/same-site-cookie-support.md) 已設定。 如果跨網站Cookie遭到封鎖，部署 [!DNL Experience Manager] 可能無法驗證。 例如， [!DNL Google Chrome] 在無痕模式下，可能會封鎖第三方Cookie。 允許Cookie於 [!DNL Chrome] 瀏覽器，按一下地址列中的「眼睛」圖示，導覽至 **網站無法運作** > **已封鎖**，選取遠端DAM URL，並允許登入權杖Cookie。 或者，請參閱 [如何啟用第三方Cookie](https://support.google.com/chrome/answer/95647).

  ![無痕模式下的Chrome瀏覽器發生Cookie錯誤](assets/chrome-cookies-incognito-dialog.png)

* 如果未擷取遠端參照並產生錯誤訊息，請檢查 [!DNL Sites] 部署可用，並檢查網路連線問題。 請稍後重試以檢查。 [!DNL Assets] 部署嘗試與建立連線兩次 [!DNL Sites] 部署，然後報告失敗。

  ![無法擷取資產遠端參考](assets/reference-report-failure.png)

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
