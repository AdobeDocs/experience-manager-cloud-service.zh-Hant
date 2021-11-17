---
title: '[!DNL Experience Manager Assets] integration with [!DNL Adobe Workfront]'
description: 介紹 [!DNL Assets] 和 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
source-git-commit: d75d9ac16f64b6770fcf35d58474c47c52b1585b
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 整合 [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] 是一種工作管理應用程式，可幫助您在一個位置管理工作的整個生命週期。 整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 讓組織通過內在連接工作和數字資產管理來提高內容速度和上市時間。 在Workfront中管理其工作的內容中，使用者可存取所需檔案和影像。

Adobe提供兩種不同的連接器來整合這兩種解決方案。 連接器可讓企業自動化、設定和可擴充的工作流程在 [!DNL Assets] 和 [!DNL Workfront]. 此外， [!DNL Assets Essentials] 可作為新 [!DNL Workfront] 客戶可個別購買。 要了解更多資訊，請參閱 [[!DNL Workfront] and [!DNL Assets Essentials] 整合](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/integration.html).

[!DNL Workfront for Experience Manage enhanced connector] 讓您的組織：

* 輕鬆協作。 創意團隊可以少擔心一件事。 現在，完成工作後，只需按一下按鈕，即可將其傳送至AEM Assets
* 讓資產在每個步驟都更豐富。 在資產生命週期的每個階段收集新資料。 從構思到傳送，您的組織都可擷取關鍵量度，對未來資產開發做出更明智的業務決策。
* 參考現有資產。 在生產環境中輕鬆尋找和重複使用現有資產，並將其新增至新專案作為參考項目。
* 同步所有中繼資料。 盡可能輕鬆新增，以增強您的中繼資料。 透過連接器，Workfront和AEM Assets之間可雙向同步中繼資料
* 運用 [!DNL Experience Manager Assets] 數位管理功能。 直接在您最愛的內部存取您所有的數位資產 [!DNL Creative Cloud] 應用程式。 啟用AI的智慧標籤和裁切、搜尋工具、動態傳遞，透過 [!DNL Dynamic Media]，還有更多。

請參閱平台支援和其他 [enhanced connector的必要條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobe需要部署，並配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services],Adobe不支援。
>
>Adobe可發行 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 這使得該連接器冗餘；如果發生此情況，客戶可能需要從使用此連接器進行轉變。

## 比較不同的整合 [!DNL Assets] 和 [!DNL Workfront] {#feature-parity-matrix}

以下是可透過以下各種整合功能的詳細資訊： [!DNL Assets] 和 [!DNL Workfront].

| 功能 | 說明 | [!DNL Workfront]與[!DNL Assets Essentials] | [!DNL Workfront] for [!DNL Experience Manager] 連接器 | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| 部署方法 | 適合 [!DNL Assets] 提供。 | Assets Essentials | Cloud Service, Adobe Managed Services，內部部署 | Cloud Service, Adobe Managed Services，內部部署 |
| 從 [!DNL Workfront] to [!DNL Assets] | WF文檔的最新版本可以上載到AEM Assets，該文檔將作為新版本連結。 | ✓ | ✓ | ✓ |
| 手動將AEM資料夾連結至Workfront物件 | 現有的AEM資料夾可以連結為Workfront資料夾，其子資產可以連結為新的Workfront檔案。 | ✓ | ✓ | ✓ |
| 連結 [!DNL Assets] 至Workfront物件 | AEM中的現有資產可以連結至新Workfront檔案，或連結為現有檔案的新版本。 | ✓ | ✓ | ✓ |
| 新增至連結資料夾的資產會自動傳送至AEM | 如果將檔案新增至連結的資料夾，則相關聯的資產會自動上傳至AEM Assets做為新資產。 | ✓ | ✓ | ✓ |
| 從Workfront下載連結的AEM Assets | 在Workfront中連結資產時，使用者可以下載資產的位元組。 | ✓ | ✓ | ✓ |
| 從Workfront中搜尋AEM Assets | Workfront中的AEM Assets選取器允許資產的全文搜尋。 | ✓ | ✓ | ✓ |
| 從Workfront檢視並導覽AEM資料夾階層 | Workfront中的AEM Assets選取器可瀏覽受使用者在AEM中設定之相關存取控制和權限所限制的AEM Assets階層。 | ✓ | ✓ | ✓ |
| 取消連結Workfront中的AEM Assets資產 | 可從相關聯的Workfront檔案中取消連結來自AEM的現有連結資產。 這不會刪除AEM內的原始資產。 | ✓ | ✓ | ✓ |
| 從Workfront將新版本控制資產新增至AEM Assets | 在Workfront的檔案上新增新增的版本時，使用者可將新版本傳送至AEM，以取代現有版本。 | ✓ | ✓ | ✓ |
| 按一下「將使用者導向AEM」時在Workfront中連結的資產 | 系統會將使用者導向至AEM，從Workfront內預覽連結的資產。 | ✓ | ✓ | 自訂 |
| 在Workfront中自動建立連結的AEM資料夾 | 使用物件狀態在Workfront中自動建立連結的AEM資料夾。 根據WorkfrontPortfolio、方案和專案自動組織AEM資料夾。 | 否 | 否 | ✓ |
| 注釋同步 | 自動同步資產的註解 [!DNL Workfront] to [!DNL Assets] | 否 | ✓ | ✓ |
| 將Workfront資產中繼資料對應至AEM Assets | Workfront物件和自訂表單屬性可對應至AEM資產中繼資料屬性。 值會在初始上傳/連結時推送。 | ✓ | ✓ | ✓ |
| 在Workfront中自動建立檔案自訂Forms | 使用AEM工作流程將自訂表單附加至Workfront檔案、工作和問題。 | 否 | 手動新增自訂表單，然後自動同步即可運作 | ✓ |
| AEM Assets與Workfront元資料雙向自動更新 | 自動更新AEM Assets和Workfront之間的中繼資料。 | 否 | ✓ | ✓ |
| 將Workfront中繼資料對應至AEM Assets資料夾 | 將Workfront專案中繼資料與連結的AEM資料夾同步。 | 否 | 否 | ✓ |
| AEM中繼資料更新為新版本 | 可進行AEM中的設定，以判斷Workfront中新版本的資產是否也會隨對其中繼資料所做的任何變更推送。 | 否 | 否 | ✓ |
| 變更Workfront中的自訂Forms時自動更新AEM中繼資料 | Workfront的設定方式為將指定的AEM資產中繼資料屬性對應至檔案自訂表單。 最初連結資產或更新資產時，這些中繼資料屬性的值會複製到對應的Workfront檔案自訂表單欄位。 請務必謹慎防止變更從AEM傳回至AEM，如同是源自Workfront的變更。 | 否 | ✓ | ✓ |
| 在連結的資產上建立新校樣版本 | 在Workfront中連結資產時，會自動產生校樣。 | 否 | ✓ | 自訂 |
| 在Workfront物件上設定狀態 | 使用AEM工作流程，根據可設定條件設定Workfront物件狀態 | 否 | 否 | ✓ |
| 將資產發佈至AEM發佈環境或Brand Portal | 為Workfront使用者提供自動將連結資產發佈至AEM發佈環境或Brand Portal的選項。 | 否 | 否 | ✓ |
