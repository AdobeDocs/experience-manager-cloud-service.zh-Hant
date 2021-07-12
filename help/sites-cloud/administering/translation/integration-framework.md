---
title: 配置翻譯整合框架
description: 了解如何配置翻譯整合框架以與第三方翻譯服務整合。
feature: 語言副本
role: Admin
exl-id: 6e74cdee-7965-4087-a733-e9d81c4aa7c2
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 1%

---

# 配置翻譯整合框架 {#configuring-the-translation-integration-framework}

翻譯整合框架與第三方翻譯服務整合，以協調AEM內容的翻譯。 它涉及三個基本步驟。

1. [連接到翻譯服務提供商。](#connecting-to-a-translation-service-provider)
1. [建立翻譯整合架構設定。](#creating-a-translation-integration-configuration)
1. [將雲端設定與您的頁面建立關聯。](#configuring-pages-for-translation)

如需AEM中內容翻譯功能的概觀，請參閱[多語言網站的翻譯內容](overview.md)。

## 連接到翻譯服務提供商 {#connecting-to-a-translation-service-provider}

建立將AEM連接至翻譯服務提供者的雲端設定。 AEM預設包含[連接到Microsoft Translator](connect-ms-translator.md)的功能。

下列翻譯廠商提供翻譯專案的AEM API實作。

* [Microsoft Translator](connect-ms-translator.md)
* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (AdobeExchange首要合作夥伴)
* [粘土片技術](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [雲字](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [CrossLang NV](https://exchange.adobe.com/experiencecloud.details.90049.crosslang-xtm-for-adobe-experience-manager.html)
* [林戈泰克](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [智慧](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)

安裝連接器封裝後，您可以為連接器建立雲端設定。 通常，您需要提供認證以驗證翻譯服務。 有關為Microsoft Translator連接器添加雲配置的資訊，請參閱[與Microsoft Translator整合](connect-ms-translator.md)。

您可以視需要為相同連接器建立多個雲端設定。 例如，為您與相同供應商擁有的每個帳戶或項目建立一個配置。

配置連接後，可以建立使用該連接的翻譯整合框架配置。

## 建立翻譯整合設定 {#creating-a-translation-integration-configuration}

建立翻譯整合架構設定，以指定如何翻譯您的內容。 設定包含下列資訊：

* 要使用哪個翻譯服務提供商
* 是要執行人還是機器翻譯
* 是否翻譯與頁面或資產相關聯的其他內容，例如標籤

建立框架配置後，可將雲配置與要根據配置翻譯的頁面相關聯。 當翻譯過程開始時，翻譯工作流程會根據相關的框架配置進行。

當您網站的不同區段有不同的翻譯需求時，請據此建立多個架構設定。 例如，多語言網站可能包含英文、西班牙文和日文復本。 網站擁有者使用兩個不同的翻譯服務提供者提供西班牙文和日文翻譯。 因此，框架的兩個配置已配置。 每個配置使用不同的翻譯服務提供程式。

配置翻譯整合框架後，您可以[將其與使用該框架的頁面](preparation.md)關聯。

>[!TIP]
>
>如需AEM中內容翻譯功能的概觀，請參閱[多語言網站的翻譯內容](overview.md)。

架構的單一設定可控制如何轉譯頁面內容和資產。

![翻譯設定](../assets/translation-configuration.png)

要建立新的翻譯配置：

1. 在[全域導覽功能表中，](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)按一下或點選&#x200B;**工具 — >Cloud Services-&amp;翻譯Cloud Services**。
1. 導覽至您要在內容結構中建立設定的位置。 這通常以特定網站為基礎，或可為全域。
1. 在欄位中提供下列資訊，然後按一下或點選&#x200B;**Create**:
   1. 在下拉式清單中選取&#x200B;**組態類型**。
   1. 輸入配置的&#x200B;**標題**。 **Title**&#x200B;在&#x200B;**Cloud Services**&#x200B;控制台以及頁面屬性下拉式清單中識別配置。
   1. 或者，鍵入&#x200B;**Name**&#x200B;以用於儲存配置的儲存庫節點。
1. 在&#x200B;**編輯配置**&#x200B;窗口中，在&#x200B;**Sites**&#x200B;和&#x200B;**Assets**&#x200B;頁簽上配置屬性，然後按一下或點選&#x200B;**Save &amp; Close**。

### 站點配置屬性 {#sites-configuration-properties}

**Sites**&#x200B;標籤控制頁面內容轉譯的執行方式。

| 屬性 | 說明 |
|---|---|
| 轉換工作流程 | 此屬性定義框架對站點內容執行的翻譯方法：<br> — 機器翻譯：翻譯提供者使用機器翻譯即時執行翻譯。<br> — 人類翻譯：內容被發送到翻譯提供者，由翻譯者翻譯。<br> — 不翻譯：內容不會傳送以供翻譯。這是為了略過某些內容分支，這些分支不會翻譯，但可以以最新內容更新。 |
| 翻譯提供者 | 此屬性定義要執行翻譯的翻譯提供程式。 當安裝了相應的連接器時，提供程式將出現在清單中。 |
| 內容類別 | （僅限機器翻譯）此屬性是描述要翻譯的內容的類別。 翻譯內容時，類別可能會影響術語和措辭的選擇。 |
| 翻譯標記 | 此選項可轉譯與頁面相關聯的標籤。 |
| 翻譯頁面資產 | 此屬性定義如何轉譯從檔案系統新增至元件或從資產參照的資產：<br> — 請勿轉譯：頁面資產不會翻譯。<br> — 使用網站翻譯工作流程：系統會根據Sitestab上的設定屬性處理 **** 資產。<br> — 使用資產翻譯工作流程：系統會根據Assetstab上設定的屬性處理 **** 資產。 |
| 自動執行翻譯 | 啟用此屬性可在建立翻譯專案後自動執行翻譯工作。 選擇此選項時，您沒有機會複查和調整翻譯工作的範圍。 |

### Assets設定屬性 {#assets-configuration-properties}

資產屬性可控制如何設定資產。 如需轉譯資產的詳細資訊，請參閱[建立資產的語言副本](/help/assets/translate-assets.md)。

| 屬性 | 說明 |
|---|---|
| 轉換工作流程 | 此屬性會選取架構對資產執行的翻譯類型：<br> — 機器翻譯：翻譯提供者使用機器翻譯立即執行翻譯。<br> — 人類翻譯：內容會自動傳送至翻譯提供者，以供手動翻譯。<br> — 不翻譯：不會傳送資產以進行翻譯。 |
| 翻譯提供者 | 此屬性定義要執行翻譯的翻譯提供程式。 當安裝了相應的連接器時，提供程式將出現在清單中。 |
| 內容類別 | （僅限機器翻譯）此屬性說明您要翻譯的內容。 翻譯內容時，類別可能會影響術語和措辭的選擇。 |
| 翻譯資產 | 啟用此屬性以將資產納入翻譯專案。 |
| 翻譯中繼資料 | 啟用此屬性以轉譯資產中繼資料。 |
| 翻譯標記 | 啟用此屬性可轉換與資產相關聯的標籤。 |
| 自動執行翻譯 | 選擇此屬性可在建立翻譯項目後自動執行翻譯作業。 選擇此選項時，您沒有機會複查或限定翻譯工作的範圍。 |

## 配置翻譯頁面 {#configuring-pages-for-translation}

若要配置將源頁面翻譯成其他語言，請將這些頁面與以下雲配置關聯：

* 將AEM連接至翻譯提供者的雲端設定。
* 配置翻譯詳細資訊的翻譯整合框架。

請注意，翻譯整合架構雲配置標識了用於連接到服務提供商的雲配置。 將源頁面與框架雲配置關聯時，該頁面必須與框架雲配置所使用的服務提供商雲配置關聯。

將頁面與雲配置關聯時，頁面的子體將繼承關聯。 例如，如果將`/content/wknd/language-masters/en/magazine`頁與翻譯整合框架相關聯，則其下的`magazine`頁和子頁將根據框架進行翻譯。

如有需要，您可以在子代頁面上覆寫關聯。 例如，網站的內容主要與旅行和生活方式有關。 不過，有一個分頁描述了公司。 在這種情況下，網站的根頁面可能與一個「翻譯整合框架」相關聯，該框架使用「生活風格」類別指定機器翻譯，而描述公司的分支將使用一個框架來使用「一般」類別執行機器翻譯。

### 將頁面與翻譯提供者關聯 {#associating-a-page-with-a-translation-provider}

將頁面與翻譯提供者建立關聯，您使用該提供者翻譯頁面和子代頁面。

1. 在網站主控台中，選取要設定的頁面，然後按一下或點選&#x200B;**檢視屬性**。
1. 按一下或點選&#x200B;**Cloud Services**&#x200B;標籤。
1. 在&#x200B;**新增設定**&#x200B;下拉式清單中，選取設定。
1. 按一下或點選&#x200B;**儲存並關閉**。

### 將頁面與翻譯整合框架關聯 {#associating-pages-with-a-translation-integration-framework}

將頁面與定義您要如何執行頁面和子代頁面翻譯的翻譯整合框架相關聯。

1. 在網站主控台中，選取要設定的頁面，然後按一下或點選&#x200B;**檢視屬性**。
1. 按一下或點選&#x200B;**Cloud Services**&#x200B;標籤。
1. 在&#x200B;**新增設定**&#x200B;下拉式清單中，選取設定。
1. 按一下或點選&#x200B;**儲存並關閉**。
