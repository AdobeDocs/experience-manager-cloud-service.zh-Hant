---
title: '[!DNL Experience Manager Assets] 與整合 [!DNL Adobe Workfront]'
description: 以下專案之間的整合簡介： [!DNL Assets] 和 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 5568be57db4e270fcee22e637fc40f07529e0ecd
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 與整合 [!DNL Adobe Workfront] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service  | 本文 |

[!DNL Adobe Workfront] 是工作管理應用程式，協助您在一個地方管理整個工作生命週期。以下兩者的整合： [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 可讓組織在本質上連線工作和數位資產管理，藉以改善內容速度和上市時間。 在Workfront中管理其工作的情況下，使用者可以存取所需的檔案和影像。

將優惠方案Adobe至 [整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 本機(支援Assets Essentials和Assetsas a Cloud Service)或使用Workfront進行Experience Manager增強型聯結器](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html). 如果是原生整合，您不需要聯結器來整合這兩個解決方案。

>[!NOTE]
>
>Adobe不支援同時使用Workfront進行Experience Manager增強型聯結器和Experience Manager整合。

透過原生Experience Manager整合和 [!DNL Workfront for Experience Manager enhanced connector]，您可以：

| 原生 [!DNL Adobe Experience Manager Assets] 功能 | [!DNL Workfront for Experience Manager enhanced connector] 功能 |
|---|---|
| <ul><li>在Workfront中快速設定整合。</li><li>自動建立在Workfront和Experience Manager之間連結的資料夾。</li><li>輕鬆同步現有連結資產的中繼資料。</li><li>在Workfront中變更專案中繼資料時自動更新。</li><li>將多個Experience Manager Assets存放庫順利連線到一個Workfront環境，或將多個Workfront環境連線到跨組織ID的一個Experience Manager Assets存放庫。</li> | <ul><li>在Workfront中自動建立連結的Experience Manager資料夾，並根據WorkfrontPortfolio、計畫和專案組織資料夾。</li><li>將Workfront專案中繼資料與連結的Experience Manager資料夾同步。</li><li>以新版本Experience Manager中繼資料更新。</li><li>使用Experience Manager工作流程，根據可設定的條件設定Workfront物件狀態。</li><li>將資產發佈到Experience Manager發佈環境或Brand Portal。</li> |

請參閱 [以下支援的功能可供比較](#feature-parity-matrix) 原生整合或兩個解決方案之間使用聯結器的整合之間的關聯。

>[!IMPORTANT]
>
>自2022年6月起，Adobe已發行新的原生整合，用於將Workfront與Adobe Experience Manager Assetsas a Cloud Service連線。 此整合已成為連線這兩個解決方案的必要方法。 日後任何新實施的增強型聯結器（1.9.8及更新版本）都會遭到封鎖，而無法連線Workfront與AEM Assetsas a Cloud Service。 如需如何設定此整合的詳細資訊，請參閱 [設定Experience Manager Assetsas a Cloud Service整合](workfront-connector-configure.md).
>

請參閱平台支援和 [增強型聯結器的先決條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe需要部署和設定 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署與設定沒有認證合作夥伴或 [!DNL Adobe Professional Services]，Adobe不支援。
>
>* Adobe可能會將更新發行至 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 讓此聯結器成為備援；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
>
>* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請參閱的步驟5(a) [增強型聯結器安裝指示](workfront-connector-install.md).
>
>* 另請參閱 [適用於Experience Manager Assets增強型聯結器的Workfront合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 如需有關考試的資訊，請參閱 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## 比較以下專案之間的不同整合： [!DNL Assets] 和 [!DNL Workfront] {#feature-parity-matrix}

以下為透過以下各種整合型別所提供的功能細節： [!DNL Assets] 和 [!DNL Workfront].

| 功能 | 說明 | [!DNL Workfront] 和 [!DNL Assets Essentials] *無聯結器(OOTB)* | [!DNL Workfront for Experience Manager enhanced connector] *需要聯結器* | Workfront和 [!DNL Experience Manager as a Cloud Service] *無聯結器(OOTB)* |
|----|----|----|-----|-----|
| 部署方法 | 適合的 [!DNL Assets] 方案。 | Assets Essentials | Adobe Managed Services，內部部署 | 雲端服務 |
| **一般** |
| 傳送數位檔案來源 [!DNL Workfront] 至 [!DNL Assets] | WF檔案的最新版本可上傳至AEM Assets，並以檔案新版本連結。 | ✓ | ✓ | ✓ |
| 手動將AEM資料夾連結至Workfront物件 | 現有的AEM資料夾可連結為Workfront資料夾，其子資產可連結為新的Workfront檔案。 | ✓ | ✓ | ✓ |
| 連結 [!DNL Assets] Workfront物件 | AEM中的現有資產可以連結到新的Workfront檔案，或作為現有檔案的新版本。 | ✓ | ✓ | ✓ |
| 新增至連結資料夾的資產會自動傳送至AEM | 如果將檔案新增至連結的資料夾，則會自動將關聯的資產作為新資產上傳到AEM Assets。 | ✓ | ✓ | ✓ |
| 從Workfront下載連結的AEM Assets | 在Workfront中連結資產時，使用者可以下載資產的位元組。 | ✓ | ✓ | ✓ |
| 在Workfront中搜尋AEM Assets | Workfront中的AEM Assets選擇器可讓您以全文搜尋資產。 | ✓ | ✓ | ✓ |
| 在Workfront中搜尋AEM資料夾 | Workfront中的AEM Assets選擇器允許對資料夾進行全文搜尋。 | ✓ | ✓ | ✓ |
| 從Workfront檢視和導覽AEM資料夾階層 | Workfront中的AEM Assets選擇器可讓您瀏覽受使用者在AEM中設定的相關存取控制項和許可權限制的AEM Assets階層。 | ✓ | ✓ | ✓ |
| 在AEM時間軸中追蹤資產版本 | 維護Workfront和AEM之間的檔案版本記錄。 | ✓ | ✓ | ✓ |
| 在Workfront中取消資產與AEM Assets的連結 | 從AEM連結的現有資產可以從關聯的Workfront檔案中取消連結。 這不會刪除AEM內的原始資產。 | ✓ | ✓ | ✓ |
| 從Workfront將新版本的資產新增至AEM Assets | 在Workfront的檔案中新增新版本時，使用者可以將新版本傳送至AEM以取代現有版本。 | ✓ | ✓ | ✓ |
| 按一下時在Workfront中連結的資產(直接使用者連結至AEM) | 系統會將使用者導向至AEM，以從Workfront預覽連結的資產。 | ✓ | ✓ | 近期 |
| 在Workfront中自動建立連結的AEM資料夾 | 使用專案狀態在Workfront中自動建立連結的AEM資料夾。 根據WorkfrontPortfolio、計畫和專案自動設定AEM資料夾。 | 否 | ✓ | 否 |
| 從Workfront直接導覽至AEM存放庫 | 允許使用者導覽至Workfront中設定的可用AEM存放庫。 | ✓ | 否 | ✓ |
| 在Workfront中建立連結的AEM資料夾 | 使用「檔案」標籤中的選項，在Workfront中手動建立連結的AEM資料夾。 | ✓ | 否 | ✓ |
| 評論同步 | 從自動同步資產的註解 [!DNL Workfront] 至 [!DNL Assets] | 否 | ✓ | 否 |
| 支援連線至單一AEM環境的多個Workfront環境 | 來自多個Workfront環境的使用者可以連線至單一AEM環境。 | ✓ | 否 | ✓ |
| 支援連線至單一Workfront環境的多個AEM環境 | 單一Workfront環境內的使用者可以在多個AEM環境之間傳送或連結資產。 | ✓ | ✓ | ✓ |
| **中繼資料** |
| 將Workfront資產中繼資料對應至AEM Assets | Workfront物件和自訂表單屬性可能會對應至AEM資產中繼資料屬性。 值會在初始上傳/連結時推送。 | ✓ | ✓ | ✓ |
| 在Workfront中自動建立檔案自訂Forms | 使用AEM工作流程將自訂表單附加至Workfront檔案、任務和問題。 | 否 | ✓ | 否 |
| 在AEM Assets和Workfront之間雙向自動更新中繼資料 | 在AEM Assets和Workfront之間自動更新中繼資料。 資產必須先從Workfront推送至AEM，且Workfront資產中繼資料必須對應至AEM資產，才能正確進行雙向中繼資料更新。 | 否 | ✓ | 否 |
| 在Workfront中即時檢視對應至AEM的中繼資料 | 在「Workfront檔案詳細資訊」和「檔案摘要」面板中，檢視更新後對應至AEM的中繼資料。 | ✓ | 否 | ✓ |
| 將更新的Workfront中繼資料即時推送到AEM | 自動將對應的Workfront中繼資料更新為AEM，無需重新推送資產或資產的新版本。 | ✓ | 否 | ✓ |
| 將Workfront中繼資料對應至AEM Assets資料夾 | 將Workfront專案中繼資料與連結的AEM資料夾同步。 | 否 | ✓ | ✓ |
| 新版本的AEM中繼資料更新 | AEM中的設定可決定Workfront中新版本的資產是否也會推動對其中繼資料所做的任何變更。 | 否 | ✓ | 否 |
| 在Workfront中自訂Forms變更時自動更新AEM中繼資料 | AEM可讓您訂閱Workfront中檔案表單的更新。 因此，Workfront檔案自訂表單中繼資料的任何更新都會修改對應AEM中繼資料欄位的值。 | 否 | ✓ | 否 |
| **工作流程（現成可用）** |
| 在連結的資產上建立新校訂版本 | 在Workfront中連結資產時，會自動產生校訂。 | 否 | 自訂 | 否 |
| 在Workfront物件上設定狀態 | 使用AEM工作流程根據可設定的條件設定Workfront物件狀態 | 否 | ✓ | 近期 |
| 將資產發佈至AEM發佈環境或Brand Portal | 為Workfront使用者提供自動將連結的資產發佈至AEM發佈環境或Brand Portal的選項。 | 否 | ✓ | 近期 |
