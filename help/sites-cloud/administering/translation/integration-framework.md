---
title: 設定翻譯整合框架
description: 瞭解如何設定翻譯整合架構，以與協力廠商翻譯服務整合。
feature: Language Copy
role: Admin
exl-id: 6e74cdee-7965-4087-a733-e9d81c4aa7c2
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 8%

---

# 設定翻譯整合框架 {#configuring-the-translation-integration-framework}

翻譯整合框架會與協力廠商翻譯服務整合，以協調AEM內容的翻譯。 它涉及三個基本步驟。

1. [連接到您的翻譯服務提供者。](#connecting-to-a-translation-service-provider)
1. [建立翻譯整合框架設定。](#creating-a-translation-integration-configuration)
1. [將雲端設定與您的頁面建立關聯。](#configuring-pages-for-translation)

如需AEM內容翻譯功能的概觀，請參閱 [翻譯多語言網站的內容](overview.md).

>[!TIP]
>
>如果您不熟悉翻譯內容，請參閱 [網站翻譯歷程，](/help/journey-sites/translation/overview.md) 將引導您使用AEM強大的翻譯工具來翻譯AEM Sites內容，非常適合沒有AEM或翻譯經驗的人士。

## 連接到翻譯服務提供者 {#connecting-to-a-translation-service-provider}

建立雲端設定，將AEM連線至您的翻譯服務提供者。 AEM具備以下功能： [連線至Microsoft Translator](connect-ms-translator.md) 依預設。

下列翻譯廠商會為翻譯專案提供AEM API的實作。

* [Microsoft Translator](connect-ms-translator.md)
* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (AdobeExchange主要合作夥伴)
* [Clay平板電腦技術](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM Cloud](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [RWS](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108277.html)
* [Smartling](https://www.smartling.com/software/integrations/adobe-experience-manager/)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)

安裝聯結器套件後，您可以為聯結器建立雲端設定。 通常，您需要提供認證以向翻譯服務進行驗證。 如需有關為Microsoft Translator聯結器新增雲端設定的資訊，請參閱 [與Microsoft Translator整合](connect-ms-translator.md).

您可以視需要為相同的聯結器建立多個雲端設定。 例如，為您與相同廠商的每個帳戶或專案建立一個設定。

設定連線後，您可以建立使用它的翻譯整合框架設定。

## 建立翻譯整合設定 {#creating-a-translation-integration-configuration}

建立翻譯整合框架設定，以指定如何翻譯您的內容。 設定包括以下資訊：

* 要使用哪個翻譯服務提供者
* 是否進行人工翻譯或機器翻譯
* 是否要翻譯與頁面或資產相關聯的其他內容，例如標籤

建立框架設定後，您會根據設定將雲端設定與您要翻譯的頁面建立關聯。 開始翻譯流程時，翻譯工作流程會根據關聯的框架設定繼續進行。

若您網站的不同區段有不同的翻譯需求，請據以建立多個框架設定。 例如，多語言網站可能包含英文、西班牙文和日文版本。 網站擁有者使用兩個不同的翻譯服務提供者進行西班牙文和日文翻譯。 因此，已設定框架的兩個設定。 每個設定使用不同的翻譯服務提供者。

設定翻譯整合框架後，您可以 [將其與頁面建立關聯](preparation.md) 使用它的使用者。

>[!TIP]
>
>如需AEM內容翻譯功能的概觀，請參閱 [翻譯多語言網站的內容](overview.md).

架構的單一設定可控制頁面內容和資產的翻譯方式。 若要建立新的翻譯設定：

1. 在 [全域導覽功能表、](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) 按一下或點選 **工具 — >Cloud Services->翻譯Cloud Services**.
1. 在內容結構中導覽到想要建立設定的位置。這通常是根據特定網站或是全域。
1. 在欄位中提供下列資訊，然後按一下或點選 **建立**.：
   1. 在下拉選單中選取&#x200B;**設定類型**。
   1. 輸入設定的&#x200B;**標題**。此 **標題** 會識別 **Cloud Services** 控制檯和in page property下拉式清單。
   1. 或者，輸入&#x200B;**名稱**&#x200B;以用於儲存設定的存放庫節點。
1. 在 **編輯設定** 視窗中，設定屬性 **網站** 和 **資產** 標籤，然後按一下或點選 **儲存並關閉**.

### 網站組態屬性 {#sites-configuration-properties}

此 **網站** tab控制如何執行頁面內容的翻譯。

![網站的翻譯設定](../assets/translation-configuration.png)

| 屬性 | 說明 |
|---|---|
| 翻譯方法 | 此屬性會定義框架為網站內容執行的翻譯方法：<br> — 機器翻譯：翻譯提供者會使用機器翻譯即時執行翻譯。<br> — 人工翻譯：內容會傳送給翻譯提供者，以供譯者翻譯。<br> — 不翻譯：不傳送內容以供翻譯。 這是為了略過某些不會翻譯但可以使用最新內容更新的內容分支。 |
| 翻譯提供者 | 此屬性會定義執行翻譯的翻譯提供者。 安裝提供者的對應聯結器後，提供者會出現在清單中。 |
| 內容類別 | （僅限機器翻譯）此屬性是說明您要翻譯之內容的類別。 翻譯內容時，類別可能會影響術語和措辭的選擇。 |
| 翻譯標記 | 此選項可讓您轉譯與頁面相關聯的標籤。 |
| 翻譯頁面資產 | 此屬性會定義如何翻譯從檔案系統新增至元件或從資產參照的資產：<br> — 不翻譯：不翻譯頁面資產。<br> — 使用網站翻譯工作流程：根據上的設定屬性處理資產 **網站** 標籤。<br> — 使用資產翻譯工作流程：根據上設定的屬性處理資產 **資產** 標籤。 |
| 自動執行翻譯 | 啟用此屬性可在建立翻譯專案後自動執行翻譯工作。 選取此選項時，您無法檢閱翻譯工作並設定其範圍。 |
| 停用僅更新翻譯 | 核取此選項後，更新翻譯專案將會提交所有可翻譯欄位以供翻譯，而不只是自上次翻譯以來變更的欄位。 |

### 資產設定屬性 {#assets-configuration-properties}

資產屬性可控制如何設定資產。 如需翻譯資產的詳細資訊，請參閱 [建立資產的語言副本](/help/assets/translate-assets.md).

![網站的翻譯設定](../assets/translation-configuration-assets.png)

| 屬性 | 說明 |
|---|---|
| 翻譯方法 | 此屬性會選取框架為資產執行的翻譯型別：<br> — 機器翻譯：翻譯提供者會使用機器翻譯立即執行翻譯。<br> — 人工翻譯：內容會自動傳送給翻譯提供者，以供手動翻譯。<br> — 不翻譯：不傳送資產以供翻譯。 |
| 翻譯提供者 | 此屬性會定義執行翻譯的翻譯提供者。 安裝提供者的對應聯結器後，提供者會出現在清單中。 |
| 內容類別 | （僅限機器翻譯）此屬性說明您要翻譯的內容。 翻譯內容時，類別可能會影響術語和措辭的選擇。 |
| 翻譯資產 | 啟動此屬性以在翻譯專案中包含資產。 |
| 翻譯中繼資料 | 啟動此屬性以翻譯資產中繼資料。 |
| 翻譯標記 | 啟動此屬性以翻譯與資產關聯的標籤。 |
| 自動執行翻譯 | 選取此屬性可在建立翻譯專案後自動執行翻譯工作。 選取此選項時，您無法檢閱翻譯工作或設定其範圍。 |
| 停用僅更新翻譯 | 核取此選項後，更新翻譯專案將會提交所有可翻譯欄位以供翻譯，而不只是自上次翻譯以來變更的欄位。 |
| 啟用內容模型欄位以進行翻譯 | 啟用此選項將使用 **可翻譯** 欄位於 [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties) 以判斷欄位是否已轉譯並自動建立 [翻譯規則](rules.md) 因此， 此選項會取代您可能已建立的任何翻譯規則。 |

## 設定頁面以進行翻譯 {#configuring-pages-for-translation}

若要設定將來源頁面翻譯成其他語言的功能，請將這些頁面與下列雲端設定建立關聯：

* 連線AEM至您的翻譯提供者的雲端設定。
* 可設定翻譯詳細資訊的翻譯整合架構。

請注意，翻譯整合框架雲端設定會識別用於連線至服務提供商的雲端設定。 將來源頁面與框架雲端設定建立關聯時，該頁面必須與框架雲端設定使用的服務提供者雲端設定建立關聯。

將頁面與雲端設定建立關聯時，該頁面的子系會繼承該關聯。 例如，如果您將 `/content/wknd/language-masters/en/magazine` 頁面具備翻譯整合架構， `magazine` 頁面及其下方的子頁面會根據框架進行翻譯。

必要時，您可以覆寫下階頁面上的關聯。 例如，網站的內容主要是關於旅行和生活方式。 不過，有一個頁面分支會說明公司。 在這種情況下，網站的根頁面可能會與指定使用「生活方式」類別進行機器翻譯的「翻譯整合架構」相關聯，而說明公司情況的分支將使用按「一般」類別執行機器翻譯的架構。

### 將頁面與翻譯提供者建立關聯 {#associating-a-page-with-a-translation-provider}

將頁面與您用來翻譯頁面和後代頁面的翻譯提供者建立關聯。

1. 在網站主控台中，選取要設定的頁面，然後按一下或點選 **檢視屬性**.
1. 按一下或點選 **Cloud Services** 標籤。
1. 在 **新增設定** 在下拉式清單中選取設定。
1. 按一下或點選 **儲存並關閉**.

### 將頁面與翻譯整合框架建立關聯 {#associating-pages-with-a-translation-integration-framework}

將頁面與定義您要如何執行頁面和後代頁面翻譯的翻譯整合架構建立關聯。

1. 在網站主控台中，選取要設定的頁面，然後按一下或點選 **檢視屬性**.
1. 按一下或點選 **Cloud Services** 標籤。
1. 在 **新增設定** 在下拉式清單中選取設定。
1. 按一下或點選 **儲存並關閉**.
