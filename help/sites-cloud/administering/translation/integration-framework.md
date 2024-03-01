---
title: 設定翻譯整合框架
description: 瞭解如何設定翻譯整合框架以與協力廠商翻譯服務整合。
feature: Language Copy
role: Admin
exl-id: 6e74cdee-7965-4087-a733-e9d81c4aa7c2
source-git-commit: 05e4adb0d7ada0f7cea98858229484bf8cca0d16
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 10%

---

# 設定翻譯整合框架 {#configuring-the-translation-integration-framework}

翻譯整合框架會與協力廠商翻譯服務整合，以協調AEM內容的翻譯。 它涉及三個基本步驟。

1. [連接到您的翻譯服務提供者。](#connecting-to-a-translation-service-provider)
1. [建立翻譯整合框架設定。](#creating-a-translation-integration-configuration)
1. [將雲端設定與您的頁面建立關聯。](#configuring-pages-for-translation)

如需AEM內容翻譯功能的總覽，請參閱 [翻譯多語言網站的內容](overview.md).

>[!TIP]
>
>如果您不熟悉翻譯內容，請參閱 [網站翻譯歷程，](/help/journey-sites/translation/overview.md) 將引導您使用AEM強大的翻譯工具來翻譯AEM Sites內容，非常適合沒有AEM或翻譯經驗的人士。

## 連接到翻譯服務提供者 {#connecting-to-a-translation-service-provider}

建立雲端設定，將AEM連線至您的翻譯服務提供者。 AEM具備以下功能： [連線至Microsoft® Translator](connect-ms-translator.md) 依預設。

以下翻譯供應商提供翻譯專案的AEM API 實施。

* [微軟](connect-ms-translator.md)
* [](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) Translations.com（Adobe Systems交易所優秀合作夥伴）
* [Clay平板電腦技術](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM Cloud](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
<!-- THIS URL IS 404 * [RWS](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108277.html) -->
* [斯馬特林](https://www.smartling.com/software/integrations/adobe-experience-manager/)
* [西斯特蘭](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)

安裝聯結器套件後，您可以為聯結器建立雲端設定。 通常，您必須提供認證來向翻譯服務進行驗證。 有關為 Microsoft Translator 連接器添加雲端配置的資訊，請參閱 [與 Microsoft®® Translator](connect-ms-translator.md) 集成。

如有必要，您可以為同一連接器創建多個雲端配置。 例如，為您在同一供應商處擁有的每個帳戶或專案創建一個配置。

配置連接后，您可以建立使用該連接的翻譯集成框架配置。

## 建立翻譯整合設定 {#creating-a-translation-integration-configuration}

建立翻譯整合框架設定，讓您可以指定如何翻譯您的內容。 設定包括以下資訊：

* 要使用哪個翻譯服務提供者
* 是否進行人工翻譯或機器翻譯
* 是否要翻譯與頁面或資產相關聯的其他內容，例如標籤

建立框架設定後，請將雲端設定與您要根據該設定翻譯的頁面建立關聯。 開始翻譯流程時，翻譯工作流程會根據關聯的框架設定進行。

若您網站的不同區段有不同的翻譯需求，請據以建立多個框架設定。 例如，多語言網站可能包含英文、西班牙文和日文版本。 網站擁有者使用兩家不同的翻譯服務提供者提供西班牙文和日文翻譯。 因此，已設定框架的兩個設定。 每個設定使用不同的翻譯服務提供者。

設定翻譯整合框架後，您可以 [將其與頁面建立關聯](preparation.md) 使用它的使用者。

>[!TIP]
>
>如需AEM內容翻譯功能的總覽，請參閱 [翻譯多語言網站的內容](overview.md).

框架的單個配置控制頁面 內容和資產的轉換方式。 若要建立翻譯設定：

1. 在 [全域導覽功能表中，](/help/sites-cloud/authoring/basic-handling.md#global-navigation) 選取「 **工具 > Cloud Services與翻譯Cloud Services**」。
1. 導覽至您要在內容結構中建立設定的位置。這通常基於特定網站，也可以是全球性的。
1. 在欄位中提供以下資訊，然後選擇建立&#x200B;****。
   1. 在下拉清單中選擇 **配置類型** 。
   1. 輸入設定的&#x200B;**標題**。**標題**&#x200B;會識別&#x200B;**雲端服務**&#x200B;主控台和頁面屬性下拉清單中的設定。
   1. 或者，輸入&#x200B;**名稱**&#x200B;以用於儲存設定的存放庫節點。
1. 在 **編輯設定** 視窗中，設定以下專案的屬性： **網站** 和 **資產** 索引標籤，然後選取 **儲存並關閉**.

### 網站組態屬性 {#sites-configuration-properties}

此 **網站** tab控制如何執行頁面內容的翻譯。

![網站的翻譯設定](../assets/translation-configuration.png)

| 屬性 | 說明 |
|---|---|
| 翻譯方法 | 此屬性會定義框架為網站內容執行的翻譯方法：<br> — 機器翻譯：翻譯提供者會使用機器翻譯即時執行翻譯。<br> — 人工翻譯：內容會傳送給翻譯提供者，以供譯者翻譯。<br>- 不翻譯：不發送內容進行翻譯。 這是為了跳過某些內容分支，這些分支不會被翻譯，但可以使用最新的內容進行更新。 |
| 翻譯提供程式 | 此屬性定義執行翻譯的翻譯提供程序。 安裝相應的連接器時，提供程序將顯示在清單中。 |
| 內容類別 | （僅限機器翻譯）此屬性是描述您正在翻譯內容的類別。 翻譯內容時，類別可能會影響術語和措辭的選擇。 |
| 翻譯標記 | 此選項可讓您轉譯與頁面相關聯的標籤。 |
| 翻譯頁面資產 | 此屬性會定義如何翻譯從檔案系統新增至元件或從資產參照的資產：<br> — 不翻譯：不翻譯頁面資產。<br> — 使用網站翻譯工作流程：根據上的設定屬性處理資產 **網站** 標籤。<br> — 使用資產翻譯工作流程：根據上設定的屬性處理資產 **資產** 標籤。 |
| 自動執行翻譯 | 啟用此屬性可在建立翻譯專案後自動執行翻譯工作。 選擇此選項時，您沒有機會檢閱翻譯工作並設定其範圍。 |
| 停用僅更新翻譯 | 核取此選項時，更新翻譯專案會提交所有可翻譯的欄位以供翻譯，而不只是自上次翻譯以來變更的欄位。 |

### 資產設定屬性 {#assets-configuration-properties}

Assets属性控制如何配置資產。 有關翻譯資產的詳細信息，請参閱 [為Assets創建語言](/help/assets/translate-assets.md)副本。

![Sites翻譯設定](../assets/translation-configuration-assets.png)

| 屬性 | 說明 |
|---|---|
| 翻譯方法 | 此屬性選擇框架為資產執行的翻譯類型：<br>- 機器翻譯：翻譯提供程序使用機器翻譯立即執行翻譯。<br>- 人工翻譯：內容自動發送到翻譯供應商進行手動翻譯。<br>-請勿翻譯：Assets不送交翻譯。 |
| 翻譯提供程式 | 此屬性定義執行翻譯的翻譯提供程序。 安裝相應的連接器時，提供程序將顯示在清單中。 |
| 內容類別 | （僅限機器翻譯）此屬性說明您要翻譯的內容。 類別會影響翻譯內容時術語和措辭的選擇。 |
| 翻譯資產 | 啟用此屬性，即可將資產納入翻譯專案。 |
| 翻譯中繼資料 | 啟用此屬性以便翻譯資產 中繼資料。 |
| 翻譯標記 | 激活此屬性，以便翻譯與資產關聯的標記。 |
| 自動執行翻譯 | 選取此屬性可讓您在建立翻譯專案後自動執行翻譯工作。 選擇此選項時，您沒有機會檢閱翻譯工作或劃定其範圍。 |
| 停用僅更新翻譯 | 選中此選項后，更新翻譯專案將提交所有可翻譯欄位進行翻譯，而不僅僅是自上次翻譯以來更改的欄位。 |
| 啟用內容模型欄位以進行翻譯 | 啟用此選項將使用&#x200B;**內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties)上的[「可**&#x200B;翻譯」欄位來確定該欄位是否已翻譯，並相應地自動創建[翻譯規則](rules.md)。此選項將取代您可能已建立的任何翻譯規則。 |

## 設定要翻譯的頁面 {#configuring-pages-for-translation}

要設定將源頁面翻譯成其他語言，請將頁面與以下雲端配置相關聯：

* 用於將AEM連線到您的翻譯提供商的雲端設定。
* 設定翻譯細節的翻譯整合框架。

翻譯集成框架雲端配置標識用于連接到服務提供者的雲端配置。 將源頁面與框架雲端配置關聯時，頁面必須與框架雲端配置使用的服務提供者 雲端配置相關聯。

將頁面與雲端配置關聯時，頁面的後代將繼承該關聯。 例如，如果將頁面與翻譯集成框架相關聯 `/content/wknd/language-masters/en/magazine` ， `magazine` 則頁面和其下方的子頁面將根據該框架進行翻譯。

必要時，您可以覆寫子代頁面上的關聯。 例如，網站的內容主要是關於旅行和生活方式， 不過，其中一個頁面分支會說明公司。 在這種情況下，網站的根頁面可能會與指定使用「生活方式」類別進行機器翻譯的翻譯整合架構相關聯。 說明公司將使用「一般」類別執行機器翻譯之架構的分支。

### 將頁面與翻譯提供者建立關聯 {#associating-a-page-with-a-translation-provider}

將頁面與您用來翻譯頁面和後代頁面的翻譯提供者建立關聯。

1. 在網站主控台中，選取要設定的頁面，然後選取 **檢視屬性**.
1. 選取「**雲端服務**」標籤。
1. 在 **新增設定** 從下拉式清單中選取組態。
1. 選取「**儲存並關閉**」。

### 將頁面與翻譯整合框架建立關聯 {#associating-pages-with-a-translation-integration-framework}

將頁面與定義您要如何執行頁面和後代頁面翻譯的翻譯整合框架建立關聯。

1. 在網站控制台中，選擇要配置的頁面，然後選擇檢視 屬性&#x200B;****。
1. 選取「**雲端服務**」標籤。
1. 在“添加配置&#x200B;**”**&#x200B;下拉列表中清單，選擇配置。
1. 選取「**儲存並關閉**」。
