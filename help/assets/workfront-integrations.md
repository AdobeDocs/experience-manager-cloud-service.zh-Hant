---
title: "[!DNL Experience Manager Assets] 整合 [!DNL Adobe Workfront]"
description: 介紹在 [!DNL Assets] 和 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 5bcc2e420c1683509e29eba41f5b1847cf2cfa72
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] [!DNL Assets] 整合 [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] 是工作管理應用程式，協助您在一個地方管理整個工作生命週期。整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 使公司能夠通過將工作與數字資產管理內在地聯繫起來，提高內容的速度和上市時間。 在管理Workfront工作的範圍內，用戶可以訪問所需的檔案和影像。

Adobe [整合 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 本機(支援Assets Essentials和資產as a Cloud Service)或使用WorkfrontExperience Manager增強連接器](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html)。 在本機整合的情況下，您不需要連接器來整合兩個解決方案。

>[!NOTE]
>
>Adobe不支援使用Workfront並行Experience Manager增強連接器和Experience Manager整合。

通過本機Experience Manager整合和 [!DNL Workfront for Experience Manager enhanced connector]，您可以：

| 本機 [!DNL Adobe Experience Manager Assets] 特徵 | [!DNL Workfront for Experience Manager enhanced connector] 特徵 |
|---|---|
| <ul><li>快速建立Workfront內部的整合。</li><li>自動建立連結在Workfront和Experience Manager之間的資料夾。</li><li>輕鬆同步現有連結資產的元資料。</li><li>在Workfront更改項目元資料時自動更新。</li><li>跨組織ID將多個Experience Manager Assets儲存庫平穩地連接到一個Workfront環境，或將多個Workfront環境連接到一個Experience Manager Assets儲存庫。</li> | <ul><li>在Workfront自動建立連結的Experience Manager資料夾，並根據WorkfrontPortfolio、程式和項目組織資料夾。</li><li>將Workfront項目元資料與連結的Experience Manager資料夾同步。</li><li>Experience Manager元資料更新為新版本。</li><li>使用Workfront工作流根據可配置條件設定Experience Manager對象狀態。</li><li>將資產發佈到Experience Manager或發佈到Brand Portal。</li> |

查看 [以下支援的功能用於比較](#feature-parity-matrix) 或使用兩個解決方案之間的連接器進行整合。



查看平台支援和 [增強連接器的先決條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)。

>[!IMPORTANT]
>
>* Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅通過認證合作夥伴或 [!DNL Adobe Professional Services]。 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services]，它不受Adobe支援。
>
>* Adobe可以發佈更新 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使這個連接器冗餘；如果發生這種情況，可能需要客戶從使用此連接器進行過渡。
>
>* Adobe支援增強的連接器1.7.4版和更高版本。 不支援以前的預發行版和自定義版本。 要檢查增強的連接器版本，請參見第5(a)步 [增強的連接器安裝說明](workfront-connector-install.md)。
>
>* 請參閱 [Workfront的Experience Manager Assets增強型連接器合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 有關考試的資訊，請參見 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。


## 比較不同的整合 [!DNL Assets] 和 [!DNL Workfront] {#feature-parity-matrix}

以下是通過不同類型的整合提供的功能的詳細資訊 [!DNL Assets] 和 [!DNL Workfront]。

| 功能 | 說明 | [!DNL Workfront] 和 [!DNL Assets Essentials] *無連接器(OOTB)* | [!DNL Workfront for Experience Manager enhanced connector] *需要連接器* | Workfront [!DNL Experience Manager as a Cloud Service] *無連接器(OOTB)* |
|----|----|----|-----|-----|
| 部署方法 | 適合 [!DNL Assets] 提供。 | Assets Essentials | Adobe托管服務，內部部署 | 雲端服務 |
| **一般** |
| 從 [!DNL Workfront] 至 [!DNL Assets] | WF文檔的最新版本可以上載到AEM Assets，該文檔將作為文檔的新版本連結。 | ✓ | ✓ | ✓ |
| 手動將文AEM件夾連結到Workfront對象 | 現有AEM資料夾可以作為Workfront資料夾連結，其子資產則作為新Workfront文檔連結。 | ✓ | ✓ | ✓ |
| 連結 [!DNL Assets] 到Workfront物體 | 中的現AEM有資產可以連結到新的Workfront文檔或作為現有文檔的新版本。 | ✓ | ✓ | ✓ |
| 添加到連結資料夾的資產將自動發送AEM到 | 如果文檔添加到連結的資料夾，則關聯的資產將自動作為新資產上載到AEM Assets。 | ✓ | ✓ | ✓ |
| 從Workfront內下載連結的AEM Assets | 在Workfront連結資產時，用戶可以下載資產的位元組。 | ✓ | ✓ | ✓ |
| 在Workfront內搜尋AEM Assets | Workfront的AEM Assets選擇器允許對資產進行全文搜索。 | ✓ | ✓ | ✓ |
| 從WorkfrontAEM內搜索資料夾 | Workfront的AEM Assets選擇器允許對資料夾進行全文搜索。 | ✓ | ✓ | ✓ |
| 從Workfront內查AEM看和導航資料夾層次結構 | Workfront的AEM Assets選擇器允許瀏覽受用戶在中設定的關聯訪問控制和權限限制的AEM Assets層次結構AEM。 | ✓ | ✓ | ✓ |
| 按時間表跟蹤資AEM產版本 | 維護Workfront和之間的文檔版本歷AEM史。 | ✓ | ✓ | ✓ |
| 取消與AEM Assets在Workfront的資產連結 | 可以從關聯的AEMWorkfront文檔中取消連結現有連結資產。 這不會刪除的原始資AEM產。 | ✓ | ✓ | ✓ |
| 將新版本化資產從Workfront添加到AEM Assets | 在Workfront的文檔上添加新添加的版本時，用戶可以將新版本發送AEM到以替換現有版本。 | ✓ | ✓ | ✓ |
| 按一下直接用戶到時在Workfront連結的資AEM產 | 用戶將從AEMWorkfront內預覽連結的資產。 | ✓ | ✓ | 即將 |
| 在Workfront自AEM動建立連結資料夾 | 使用項目狀AEM態在Workfront自動建立連結資料夾。 根據WorkfrontAEMPortfolio、程式和項目自動配置資料夾。 | 否 | ✓ | 否 |
| 從Workfront直AEM接導航到儲存庫 | 允許用戶導航到Workfront內AEM配置的可用儲存庫。 | ✓ | 否 | ✓ |
| 在WorkfrontAEM建立連結資料夾 | 使用「文檔」(Documents)選AEM項卡中的選項在Workfront手動建立連結資料夾。 | ✓ | 否 | ✓ |
| 注釋同步 | 自動同步資產注釋 [!DNL Workfront] 至 [!DNL Assets] | 否 | ✓ | 否 |
| 支援連接到單個環境的多個WorkfrontAEM環境 | 來自多個Workfront環境的用戶可以連接到AEM單個環境。 | ✓ | 否 | ✓ |
| 支援連AEM接到單個Workfront環境的多個環境 | 單個Workfront環境中的用戶可以在多個環境之間發送或AEM連結資產。 | ✓ | ✓ | ✓ |
| **中繼資料** |
| 將Workfront資產元資料映射到AEM Assets | Workfront對象和自定義表單屬性可映射到AEM資產元資料屬性。 初始上載/連結時將推送值。 | ✓ | ✓ | ✓ |
| 在Workfront自動建立文檔自定義Forms | 使用工作流將自定義表單附加到Workfront文檔、任務AEM和問題。 | 否 | ✓ | 否 |
| AEM Assets與Workfront元資料雙向自動更新 | 自動更新AEM Assets和Workfront之間的元資料。 資產最初必須從Workfront推送到AEMWorkfront，而資產元資料必須映射到資AEM產，以便雙向元資料更新能夠正常工作。 | 否 | ✓ | 否 |
| 在Workfront將元資料映射到 | 在「Workfront文檔詳細資訊」和「AEM文檔摘要」面板中查看已更新的映射元資料。 | ✓ | 否 | ✓ |
| 將更新的Workfront元資料即時推送到 | 自動將映射的Workfront元數AEM據更新為，而不重新推送資產或資產的新版本。 | ✓ | 否 | ✓ |
| 將Workfront元資料映射到AEM Assets資料夾 | 將Workfront項目元資料與連結的文AEM件夾同步。 | 否 | ✓ | ✓ |
| 元AEM資料更新與新版本 | 可以進行AEM中的配置，以確定Workfront新版本化的資產是否也會推送對其元資料所做的任何更改。 | 否 | ✓ | 否 |
| 自動更新AEMWorkfront自定義Forms的元資料 | 允AEM許您訂閱Workfront文檔表單的更新。 因此，對Workfront文檔自定義表單元資料的任何更新都會修改映射元資料欄位AEM的值。 | 否 | ✓ | 否 |
| **工作流（現成）** |
| 在連結資產上建立新證明版本 | 在將Workfront的資產連結時，可自動生成證明。 | 否 | 自訂 | 否 |
| 設定Workfront對象的狀態 | 使用工作流設定基於Workfront對象狀態的可配AEM置條件 | 否 | ✓ | 即將 |
| 將資產發佈到AEM發佈環境或Brand Portal | 為Workfront用戶提供自動將連結資產發佈到AEM發佈環境或Brand Portal的選項。 | 否 | ✓ | 即將 |
