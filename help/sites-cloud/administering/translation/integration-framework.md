---
title: 配置翻譯整合框架
description: 瞭解如何配置翻譯整合框架以與第三方翻譯服務整合。
feature: 語言副本
role: 管理員
translation-type: tm+mt
source-git-commit: 69c865dbc87ca021443e53b61440faca8fa3c4d4
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 1%

---


# 配置翻譯整合框架{#configuring-the-translation-integration-framework}

翻譯整合框架與第三方翻譯服務整合，以協調內容AEM翻譯。 它包括三個基本步驟。

1. [連接到您的翻譯服務提供商。](#connecting-to-a-translation-service-provider)
1. [建立翻譯整合框架配置。](#creating-a-translation-integration-configuration)
1. [將雲端組態與您的頁面建立關聯。](#configuring-pages-for-translation)

有關中的內容翻譯功能的概AEM述，請參閱[多語言站點的翻譯內容](overview.md)。

## 連接到翻譯服務提供商{#connecting-to-a-translation-service-provider}

建立連接到翻譯服務提AEM供商的雲配置。 包AEM括[預設連接到Microsoft Translator](connect-ms-translator.md)的功能。

以下翻譯供應商為翻譯項目提供AEM了API的實施。

* [Microsoft Translator](connect-ms-translator.md)
* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (AdobeExchange Premier合作夥伴)
* [Clay Tablet Technologies](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [雲字](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [CrossLang NV](https://exchange.adobe.com/experiencecloud.details.90049.crosslang-xtm-for-adobe-experience-manager.html)
* [林戈特克](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [Smartling](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)

在安裝連接器套件後，您可以為連接器建立雲端組態。 通常，您需要提供認證，以便向翻譯服務進行驗證。 有關為Microsoft Translator連接器添加雲配置的資訊，請參閱[與Microsoft Translator整合](connect-ms-translator.md)。

如有需要，您可以為同一個連接器建立多個雲端組態。 例如，為您與相同供應商擁有的每個帳戶或專案建立一個組態。

在配置連接後，可以建立使用該連接的翻譯整合框架配置。

## 建立翻譯整合配置{#creating-a-translation-integration-configuration}

建立翻譯整合架構設定，以指定如何翻譯您的內容。 配置包括以下資訊：

* 哪個翻譯服務提供商要使用
* 無論要執行人文還是機器翻譯
* 是否翻譯與頁面或資產相關聯的其他內容，例如標籤

建立架構設定後，您會將雲端設定與您要根據設定轉譯的頁面建立關聯。 當翻譯過程啟動時，翻譯工作流會根據相關框架配置進行。

當您網站的不同區域有不同的翻譯需求時，請依此建立多個架構設定。 例如，多語言網站可能包含英文、西班牙文和日文版。 網站擁有者使用兩種不同的翻譯服務供應商進行西班牙文和日文翻譯。 因此，配置了框架的兩種配置。 每個配置使用不同的翻譯服務提供方。

配置翻譯整合框架後，可以[將其與使用該框架的頁面](preparation.md)關聯。

>[!TIP]
>
>有關中的內容翻譯功能的概AEM述，請參閱[多語言站點的翻譯內容](overview.md)。

架構的單一設定可控制如何翻譯頁面內容和資產。

![翻譯配置](../assets/translation-configuration.png)

要建立新的翻譯配置，請：

1. 在[全域導覽功能表中，](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)按一下或點選&#x200B;**工具->Cloud Services-&amp;翻譯Cloud Services**。
1. 導覽至您要在內容結構中建立設定的位置。 這通常是以特定網站為基礎，或可以是全域網站。
1. 在欄位中提供下列資訊，然後按一下或點選&#x200B;**Create**:
   1. 在下拉式清單中選擇&#x200B;**配置類型**。
   1. 為配置輸入&#x200B;**Title**。 **Title**&#x200B;在&#x200B;**Cloud Services**&#x200B;控制台以及頁面屬性下拉式清單中識別設定。
   1. 或者，鍵入&#x200B;**Name**&#x200B;以用於儲存配置的儲存庫節點。
1. 在&#x200B;**編輯配置**&#x200B;窗口中，在&#x200B;**站點**&#x200B;和&#x200B;**資產**&#x200B;頁籤上配置屬性，然後按一下或點選&#x200B;**保存並關閉**。

### 站點配置屬性{#sites-configuration-properties}

**Sites**&#x200B;標籤控制頁面內容的翻譯方式。

| 屬性 | 說明 |
|---|---|
| 轉換工作流程 | 此屬性定義框架對站點內容執行的轉換方法：<br>-機器轉換：翻譯提供者使用機器翻譯即時執行翻譯。<br>-人文翻譯：內容將發送到翻譯提供者，翻譯者將翻譯。<br>-不翻譯：內容不會傳送以進行翻譯。這是為了略過某些無法翻譯但可更新為最新內容的內容分支。 |
| 翻譯提供者 | 此屬性定義要執行翻譯的翻譯提供器。 當安裝了相應的連接器時，提供器將出現在清單中。 |
| 內容類別 | （僅限機器翻譯）此屬性是描述要翻譯的內容的類別。 在翻譯內容時，類別可能會影響術語和措辭的選擇。 |
| 翻譯標記 | 此選項可啟用與頁面關聯的轉換標籤。 |
| 翻譯頁面資產 | 此屬性定義如何轉換從檔案系統添加到元件或從資產引用的資產：<br>-不要轉換：頁面資產不會轉譯。<br>-使用網站翻譯工作流程：資產會根據網站標籤上的設定屬性 **** 處理。<br>-使用資產轉換工作流程：資產會根據「資產」標籤上設定的屬性 **** 處理。 |
| 自動執行翻譯 | 啟用此屬性可在建立翻譯項目後自動執行翻譯作業。 選擇此選項時，您沒有機會複查和調整翻譯作業的範圍。 |

### 資產配置屬性{#assets-configuration-properties}

資產屬性可控制如何設定資產。 有關轉譯資產的詳細資訊，請參閱[為資產建立語言副本](/help/assets/translate-assets.md)。

| 屬性 | 說明 |
|---|---|
| 轉換工作流程 | 此屬性選擇框架為資產執行的翻譯類型：<br>-機器翻譯：翻譯提供者使用機器翻譯立即執行翻譯。<br>-人文翻譯：內容會自動傳送給翻譯提供者，以手動翻譯。<br>-不翻譯：資產不會傳送以進行翻譯。 |
| 翻譯提供者 | 此屬性定義要執行翻譯的翻譯提供器。 當安裝了相應的連接器時，提供器將出現在清單中。 |
| 內容類別 | （僅限機器翻譯）此屬性描述要翻譯的內容。 在翻譯內容時，類別可能會影響術語和措辭的選擇。 |
| 翻譯資產 | 啟用此屬性，將資產包含在翻譯專案中。 |
| 翻譯中繼資料 | 啟用此屬性以翻譯資產中繼資料。 |
| 翻譯標記 | 啟用此屬性可轉換與資產相關聯的標籤。 |
| 自動執行翻譯 | 選擇此屬性可在建立翻譯項目後自動執行翻譯作業。 選擇此選項時，您沒有機會複查或調整翻譯作業的範圍。 |

## 配置翻譯頁面{#configuring-pages-for-translation}

若要設定將來源頁面翻譯成其他語言，請將頁面與下列雲端設定建立關聯：

* 連接到翻譯提供AEM商的雲配置。
* 配置翻譯詳細資訊的翻譯整合框架。

請注意，翻譯整合架構雲端組態可識別用於連線至服務提供者的雲端組態。 將源頁面與Framework雲端配置關聯時，該頁面必須與Framework雲端配置使用的服務提供商雲端配置關聯。

將頁面與雲端設定關聯時，頁面的子系會繼承關聯。 例如，如果將`/content/wknd/language-masters/en/magazine`頁與翻譯整合框架關聯，則`magazine`頁及其下面的子頁將根據框架進行翻譯。

如有需要，您可以覆寫子系頁面上的關聯。 例如，網站的內容主要與旅行和生活方式有關。 不過，其中一個頁面分支會說明該公司。 在這種情況下，站點的根頁面可能與翻譯整合框架相關聯，該框架指定使用「生活」類別進行機器翻譯，而描述該公司的分支將使用使用「一般」類別執行機器翻譯的框架。

### 將頁面與翻譯提供者{#associating-a-page-with-a-translation-provider}關聯

將頁面與翻譯提供者建立關聯，您使用該提供者翻譯頁面和後代頁面。

1. 在站點控制台中，選擇要配置的頁面，然後按一下或點選&#x200B;**查看屬性**。
1. 按一下或點選&#x200B;**Cloud Services**&#x200B;頁籤。
1. 在&#x200B;**添加配置**&#x200B;下拉清單中，選擇配置。
1. 按一下或點選&#x200B;**保存並關閉**。

### 將頁面與翻譯整合框架{#associating-pages-with-a-translation-integration-framework}關聯

將頁面與Translation Integration Framework關聯，該框架定義了如何執行頁面和後代頁面的翻譯。

1. 在站點控制台中，選擇要配置的頁面，然後按一下或點選&#x200B;**查看屬性**。
1. 按一下或點選&#x200B;**Cloud Services**&#x200B;頁籤。
1. 在&#x200B;**添加配置**&#x200B;下拉清單中，選擇配置。
1. 按一下或點選&#x200B;**保存並關閉**。
