---
title: '[!DNL Experience Manager Assets] 整合 [!DNL Adobe Workfront]'
description: 介紹 [!DNL Assets] 和 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: c029fb1ded4d3e1b9a2cdfadd82b2508b18bd980
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 整合 [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] 是工作管理應用程式，協助您在一個地方管理整個工作生命週期。整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 讓組織通過內在連接工作和數字資產管理來提高內容速度和上市時間。 在Workfront中管理其工作的內容中，使用者可存取所需的檔案和影像。

Adobe選件至 [整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 原生(支援Assets Essentials和as a Cloud Service資產)、使用Workfront for AEM連接器，或使用Workfront for Experience Manager增強型連接器](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html). 若是原生整合，您不需要連接器來整合這兩個解決方案。

>[!NOTE]
>
>Adobe不支援使用Workfront for AEM連接器或Workfront來同時Experience Manager增強連接器和Experience Manager整合。

與原生Experience Manager整合，以及 [!DNL Workfront for Experience Manager enhanced connector]，您可以：

| 原生 [!DNL Adobe Experience Manager Assets] 功能 | [!DNL Workfront for Experience Manager enhanced connector] 功能 |
|---|---|
| <ul><li>快速設定Workfront內的整合。</li><li>自動建立在Workfront和Experience Manager之間連結的資料夾。</li><li>輕鬆同步現有連結資產的中繼資料。</li><li>在Workfront中變更專案中繼資料時，自動更新該中繼資料。</li><li>跨組織ID將數個Experience Manager Assets存放庫順暢地連結至一個Workfront環境，或將數個Workfront環境順暢地連結至一個Experience Manager Assets存放庫。</li> | <ul><li>在Workfront中自動建立連結的Experience Manager資料夾，並根據WorkfrontPortfolio、方案和專案組織資料夾。</li><li>將Workfront專案中繼資料與連結的Experience Manager資料夾同步。</li><li>Experience Manager中繼資料會以新版本更新。</li><li>使用Workfront工作流程，根據可設定條件設定Experience Manager物件狀態。</li><li>將資產發佈至Experience Manager發佈環境或Brand Portal。</li> |

請參閱 [以下支援的比較功能](#feature-parity-matrix) 在原生整合或使用兩個解決方案之間連接器的整合之間。



請參閱平台支援和 [enhanced connector的必要條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe需要部署，並配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services],Adobe不支援。
>
>* Adobe可發行 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此連接器冗餘；如果發生此情況，客戶可能需要從使用此連接器進行轉變。
>
>* Adobe支援增強的連接器1.7.4版及更新版本。 不支援舊版和自訂版本。 要檢查增強的連接器版本，請參閱 [增強型連接器安裝指示](workfront-connector-install.md).
>
>* 請參閱 [Workfront for Experience Manager Assets enhanced connector的合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有關考試的資訊，請參見 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## 比較不同的整合 [!DNL Assets] 和 [!DNL Workfront] {#feature-parity-matrix}

以下是可透過以下各種整合功能的詳細資訊： [!DNL Assets] 和 [!DNL Workfront].

| 功能 | 說明 | [!DNL Workfront] 和 [!DNL Assets Essentials] *無連接器(OOTB)* | [!DNL Workfront] for [!DNL AEM] 連接器 *需要連接器* | [!DNL Workfront for Experience Manager enhanced connector] *需要連接器* | Workfront和 [!DNL Experience Manager as a Cloud Service] *無連接器(OOTB)* |
|----|----|----|------|-----|-----|
| 部署方法 | 適合 [!DNL Assets] 提供。 | Assets Essentials | Cloud Service, Adobe Managed Services，內部部署 | Cloud Service, Adobe Managed Services，內部部署 | 雲端服務 |
| **一般** |
| 從 [!DNL Workfront] to [!DNL Assets] | WF文檔的最新版本可以上載到AEM Assets，該文檔將作為新版本連結。 | ✓ | ✓ | ✓ | ✓ |
| 手動將AEM資料夾連結至Workfront物件 | 現有的AEM資料夾可以連結為Workfront資料夾，其子資產可以連結為新的Workfront檔案。 | ✓ | ✓ | ✓ | ✓ |
| 連結 [!DNL Assets] 至Workfront物件 | AEM中的現有資產可以連結至新Workfront檔案，或連結為現有檔案的新版本。 | ✓ | ✓ | ✓ | ✓ |
| 新增至連結資料夾的資產會自動傳送至AEM | 如果將檔案新增至連結的資料夾，則相關聯的資產會自動上傳至AEM Assets做為新資產。 | ✓ | ✓ | ✓ | ✓ |
| 從Workfront下載連結的AEM Assets | 在Workfront中連結資產時，使用者可以下載資產的位元組。 | ✓ | ✓ | ✓ | ✓ |
| 從Workfront中搜尋AEM Assets | Workfront中的AEM Assets選取器允許資產的全文搜尋。 | ✓ | ✓ | ✓ | ✓ |
| 從Workfront中搜尋AEM資料夾 | Workfront中的AEM Assets選取器可進行資料夾的全文搜尋。 | ✓ | 否 | ✓ | ✓ |
| 從Workfront檢視並導覽AEM資料夾階層 | Workfront中的AEM Assets選取器可瀏覽受使用者在AEM中設定之相關存取控制和權限所限制的AEM Assets階層。 | ✓ | ✓ | ✓ | ✓ |
| 在AEM時間軸中追蹤資產版本 | 維護Workfront和AEM之間的檔案版本記錄。 | ✓ | ✓ | ✓ | ✓ |
| 取消連結Workfront中的AEM Assets資產 | 可從相關聯的Workfront檔案中取消連結來自AEM的現有連結資產。 這不會刪除AEM內的原始資產。 | ✓ | ✓ | ✓ | ✓ |
| 從Workfront將新版本控制資產新增至AEM Assets | 在Workfront的檔案上新增新增的版本時，使用者可將新版本傳送至AEM，以取代現有版本。 | ✓ | ✓ | ✓ | ✓ |
| 按一下「將使用者導向AEM」時在Workfront中連結的資產 | 系統會將使用者導向至AEM，從Workfront內預覽連結的資產。 | ✓ | ✓ | ✓ | 即將推出 |
| 在Workfront中自動建立連結的AEM資料夾 | 使用專案狀態在Workfront中自動建立連結的AEM資料夾。 根據WorkfrontPortfolio、方案和專案自動設定AEM資料夾。 | 否 | 否 | ✓ | 否 |
| 從Workfront直接導覽至AEM存放庫 | 允許使用者導覽至在Workfront中設定的可用AEM存放庫。 | ✓ | 否 | 否 | ✓ |
| 在Workfront中建立連結的AEM資料夾 | 使用「檔案」標籤中的選項，在Workfront中手動建立連結的AEM資料夾。 | ✓ | 否 | 否 | ✓ |
| 注釋同步 | 自動同步資產的註解 [!DNL Workfront] to [!DNL Assets] | 否 | ✓ | ✓ | 否 |
| 支援連線至單一AEM環境的多個Workfront環境 | 來自多個Workfront環境的使用者可以連線至單一AEM環境。 | ✓ | 否 | 否 | ✓ |
| 支援連線至單一Workfront環境的多個AEM環境 | 單一Workfront環境中的使用者可以在多個AEM環境之間傳送或連結資產。 | ✓ | ✓ | ✓ | ✓ |
| **中繼資料** |
| 將Workfront資產中繼資料對應至AEM Assets | Workfront物件和自訂表單屬性可對應至AEM資產中繼資料屬性。 值會在初始上傳/連結時推送。 | ✓ | ✓ | ✓ | ✓ |
| 在Workfront中自動建立檔案自訂Forms | 使用AEM工作流程將自訂表單附加至Workfront檔案、工作和問題。 | 否 | 手動新增自訂表單，然後自動同步即可運作 | ✓ | 否 |
| AEM Assets與Workfront元資料雙向自動更新 | 自動更新AEM Assets和Workfront之間的中繼資料。 資產最初必須從Workfront推送至AEM，且Workfront資產中繼資料必須對應至AEM資產，才能進行雙向中繼資料更新，以正常運作。 | 否 | ✓ | ✓ | 否 |
| Workfront中將中繼資料對應至AEM的即時檢視 | 在「Workfront檔案詳細資訊」和「檔案摘要」面板中檢視更新的AEM對應中繼資料。 | ✓ | 否 | 否 | ✓ |
| 將更新的Workfront中繼資料即時推送至AEM | 自動將對應的Workfront中繼資料更新至AEM，而不需重新推送資產或新版本的資產。 | ✓ | 否 | 否 | ✓ |
| 將Workfront中繼資料對應至AEM Assets資料夾 | 將Workfront專案中繼資料與連結的AEM資料夾同步。 | 否 | 否 | ✓ | ✓ |
| AEM中繼資料更新為新版本 | 可進行AEM中的設定，以判斷Workfront中新版本的資產是否也會隨對其中繼資料所做的任何變更推送。 | 否 | 否 | ✓ | 否 |
| 變更Workfront中的自訂Forms時自動更新AEM中繼資料 | AEM可讓您訂閱Workfront中檔案表單的更新。 因此，對Workfront檔案自訂表單中繼資料的任何更新都會修改對應AEM中繼資料欄位的值。 | 否 | ✓ | ✓ | 否 |
| **工作流程（現成可用）** |
| 在連結的資產上建立新校樣版本 | 在Workfront中連結資產時，會自動產生校樣。 | 否 | ✓ | 自訂 | 否 |
| 在Workfront物件上設定狀態 | 使用AEM工作流程，根據可設定條件設定Workfront物件狀態 | 否 | 否 | ✓ | 即將推出 |
| 將資產發佈至AEM發佈環境或Brand Portal | 為Workfront使用者提供自動將連結資產發佈至AEM發佈環境或Brand Portal的選項。 | 否 | 否 | ✓ | 即將推出 |
