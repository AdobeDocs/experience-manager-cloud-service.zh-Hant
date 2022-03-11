---
title: 以多種語言建立和管理數字資產
description: 瞭解如何自動化將資產（包括二進位檔案、元資料和標籤）轉換為多種語言的工作流。
contentOwner: AG
feature: Asset Management,Translation
role: Admin,User
exl-id: 98df1412-a957-48a3-81c2-7dfe1d5e6d31
source-git-commit: cf3273af030a8352044dcf4f88539121249b73e7
workflow-type: tm+mt
source-wordcount: '2584'
ht-degree: 21%

---

# 多語言資產 {#multilingual-assets}

多語言資產是指使用多種語言的二進位檔案、元資料和標籤的資產。 通常，資產的二進位檔案、元資料和標籤以一種語言存在，然後翻譯成其他語言以用於多語言項目。 Adobe Experience Manager資產使您能夠自動執行資產（包括二進位檔案、元資料和標籤）的翻譯工作流，以生成其他語言的資產，以用於多語言項目。

要自動化翻譯工作流，您需要將翻譯服務提供商與Experience Manager整合，並建立項目以將資產翻譯成多種語言。 Experience Manager支援人和機器翻譯工作流。

人文翻譯：已換算資產會退回並導入Experience Manager。 當翻譯提供商與Experience Manager整合時，資產將自動在Experience Manager和翻譯提供商之間發送。

機器翻譯：機器翻譯服務立即翻譯資產的元資料和標籤。

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only ONE UBER article.

https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/translation-projects.html
https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/tc-prep.html

-->

<!-- 
Translating assets includes the following:

1. [Connecting Experience Manager with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with Experience Manager, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## 準備資產以進行翻譯 {#prepare-assets-for-translation}

多語言資產是指使用多種語言的二進位檔案、元資料和標籤的資產。 通常，資產的二進位檔案、元資料和標籤以一種語言存在，然後翻譯成其他語言以用於多語言項目。

在Adobe Experience Manager資產中，多語言資產包含在資料夾中，其中每個資料夾都包含不同語言的資產。

每個語言資料夾都稱為語言副本。 語言副本的根資料夾（稱為語言根）標識語言副本中內容的語言。 比如說， `/content/dam/it` 是義大利語副本的義大利語根。 語言副本必須使用 [正確配置的語言根](#create-a-language-root) 這樣，在執行源資產的翻譯時，就能找到正確的語言。

您最初為其添加資產的語言副本是語言主要。 主要語言是翻譯成其他語言的源。 一個示例資料夾層次結構包括多個語言根：

```shell
/content
    /- dam
        |- en
        |- fr
        |- de
        |- es
        |- it
        |- ja
        |- zh
```

執行以下步驟以準備資產以進行翻譯：

1. 建立語言主語的語言根。 例如，示例資料夾層次結構中英文副本的語言根為 `/content/dam/en`。 確保根據中的資訊正確配置語言根 [建立語言根](#create-a-language-root)。

1. 將資源添加到您的語言主語。
1. 建立需要語言副本的每個目標語言的語言根。

### 建立語言根 {#create-a-language-root}

要建立語言根，請建立一個資料夾，並使用ISO語言代碼作為「名稱」屬性的值。 在建立語言根目錄後，可以在語言根目錄的任何級別建立語言副本。

例如，示例層次結構的義大利語語言副本的根頁具有 `it` 名稱屬性。 「名稱」屬性用作儲存庫中資產節點的名稱，因此確定資產的路徑。 (*&lt;server>:&lt;port>/assets.html/content/dam/it////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////*)

1. 在「資產」主控台中，按一下/點選「 **[!UICONTROL 建立]** 」，然後從 **[!UICONTROL 選單選擇「資料夾]** 」。
1. 在「名稱」欄位中，鍵入國家/地區代碼，格式為 `<language-code>`。
1. 按一下或點擊 **[!UICONTROL 建立]**。 語言根在Assets控制台中建立。

### 查看語言根 {#view-language-roots}

觸控優化的UI提供了「參考」面板，其中顯示了在中建立的語言根清單 [!DNL Assets]。

1. 在「資產」控制台中，選擇要為其建立語言副本的語言主要版本。
1. 按一下或點擊GlobalNav表徵圖，然後選擇 **[!UICONTROL 引用]** 開啟「引用」窗格。
1. 在「引用」(References)窗格中，按一下或點擊 **[!UICONTROL 語言副本]**。 「語言副本」面板顯示資產的語言副本。

### 建立新的翻譯專案 {#create-a-new-translation-project}

如果使用此選項，則要翻譯的資產將被複製到要翻譯的語言的語言的語言根中。 根據您選擇的選項，將在「項目」控制台中為資產建立翻譯項目。 根據設定，可以手動啟動翻譯項目，或在建立翻譯項目後立即自動運行翻譯項目。

1. 在資產UI中，選擇要為其建立語言副本的源資料夾。
1. 開啟「參 **[!UICONTROL 考」窗格]** ，然後按一下「復本」下的「語言復本 **[!UICONTROL 」(Language Copies]****[!UICONTROL )]**。
1. 按一下/點擊 **[!UICONTROL 建立和翻譯]** 在底部。
1. 從「目 **[!UICONTROL 標語言]** 」清單中，選取您要建立檔案夾結構的語言。
1. 從 **[!UICONTROL 項目]** 清單，選擇 **[!UICONTROL 新建翻譯項目]**。
1. 在「專 **[!UICONTROL 案標題]** 」欄位中，輸入專案標題。
1. 按一下/點擊 **[!UICONTROL 建立]**。 源資料夾中的資產將複製到步驟4中所選區域設定的目標資料夾。
1. 要導航到資料夾，請選擇語言副本，然後按一下 **[!UICONTROL 在資產中顯示]**。
1. 導航到「項目」控制台。 翻譯資料夾會複製到「項目」控制台。
1. 開啟資料夾以查看翻譯項目。
1. 按一下/點擊項目以開啟詳細資訊頁面。
1. 要查看翻譯作業的狀態，請按一下 **[!UICONTROL 翻譯作業]** 平鋪。 <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. 在「資產」用戶介面中，開啟每個已轉換資產的「屬性」頁以查看已轉換的元資料。

>[!NOTE]
>
>此功能可用於資產和資料夾。 當選擇資產而不是資料夾時，將複製直至語言根目錄的整個資料夾層次結構，以便為資產建立語言副本。

### 添加到現有翻譯項目 {#add-to-existing-translation-project}

如果使用此選項，則在運行上一個翻譯工作流後，將為添加到源資料夾的資產運行翻譯工作流。 只有新添加的資產才會複製到包含以前轉換的資產的目標資料夾中。 在這種情況下，未建立新的翻譯項目。

1. 在資產UI中，導航到包含未轉換資產的源資料夾。
1. 選取您要轉換的資產，並開啟「參考」 **[!UICONTROL 窗格]**。「語 **[!UICONTROL 言副本]** 」部分顯示當前可用的翻譯副本數。
1. 按一下/點選「 **[!UICONTROL 復本」下的]** 「語言 **[!UICONTROL 復本」]**。將顯示可用翻譯副本的清單。
1. 按一下/點擊 **[!UICONTROL 建立和翻譯]** 在底部。
1. 從「目 **[!UICONTROL 標語言]** 」清單中，選取您要建立檔案夾結構的語言。
1. 從「項 **[!UICONTROL 目]** 」清單中，選擇「 **[!UICONTROL 添加到現有翻譯項目」]** ，以在資料夾中運行翻譯工作流。
   >[!NOTE]
   >
   >如果選擇 **[!UICONTROL 添加到現有翻譯項目]** 選項，只有在項目設定與預先存在的項目的設定完全匹配時，翻譯項目才會添加到預先存在的項目中。 否則，將建立新項目。
1. 從 **[!UICONTROL 現有翻譯項目]** 清單中，選擇要添加資產以進行轉換的項目。
1. 按一下/點選「 **[!UICONTROL 建立]**」。要翻譯的資產會新增至目標資料夾。更新的資料夾會列在「語言復 **[!UICONTROL 本」區段下]** 。
1. 導航到「項目」控制台，然後開啟您添加到的現有翻譯項目。
1. 按一下/點擊翻譯項目查看項目詳細資訊頁面。
1. 按一下/點擊位於 **翻譯作業** 平鋪以在翻譯工作流中查看資產。 翻譯作業清單還顯示資產元資料和標籤的條目。 這些條目表示還翻譯了資產的元資料和標籤。

   >[!NOTE]
   >
   >* 如果刪除標籤或元資料的條目，則不會為任何資產轉換標籤或元資料。
   >* 如果使用「機器翻譯」，則資產二進位檔案不會被翻譯。
   >* 如果添加到翻譯作業的資產包括子組，請選擇子組並刪除它們，以便翻譯繼續，不出現任何故障。


1. 要開始資產的轉換，請按一下/點擊 **[!UICONTROL 翻譯作業]** 平鋪和選擇 **[!UICONTROL 開始]** 清單中。 消息將通知翻譯作業的開始。
1. 要查看翻譯作業的狀態，請按一下/點擊 **[!UICONTROL 翻譯作業]** 平鋪。 <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. 翻譯完成後，狀態將更改為「準備審閱」。 導航到「資產」UI，並開啟每個已轉換資產的「屬性」頁以查看已轉換的元資料。

### 更新語言副本 {#update-language-copies}

運行此工作流以翻譯任何附加的資產集，並將其包含在特定區域設定的語言副本中。 在這種情況下，已轉換的資產將添加到已包含先前轉換的資產的目標資料夾中。 根據選項的選擇，建立翻譯項目或更新新資產的現有翻譯項目。 「更新語言副本」工作流包括以下選項：

* 建立新的翻譯專案
* 新增至現有翻譯專案

### 新增至現有翻譯專案 {#add-to-existing-translation-project-1}

如果使用此選項，則資產集將添加到現有翻譯項目中，以更新所選區域設定的語言副本。

1. 從資產UI中，選擇添加資產資料夾的源資料夾。
1. 開啟「參 **[!UICONTROL 考」窗格]**，然後按一下/點選「復本」下的「語言復本 ******** 」，以顯示語言復本清單。
1. 在「語言副本」之前選 **[!UICONTROL 取核取方塊]**，以選取所有語言副本。取消選擇與要翻譯的語言環境相對應的語言副本 (副本) 以外的其他副本。
1. 按一下/點擊 **[!UICONTROL 更新語言副本]** 在底部。
1. 從 **[!UICONTROL 項目]** 清單 **[!UICONTROL 添加到現有翻譯項目]**。
1. 從 **[!UICONTROL 現有翻譯項目]** 清單中，選擇要添加資產以進行轉換的項目。
1. 按一下/點選「 **[!UICONTROL 開始]**」。
1. 請參閱第9-14步 [添加到現有翻譯項目](#add-to-existing-translation-project) 完成其餘的程式。

### 建立臨時語言副本 {#creating-temporary-language-copies}

運行翻譯工作流以使用已編輯的原始資產版本更新語言副本時，現有語言副本將保留，直到您批准已翻譯的資產。 [!DNL Assets] 將新翻譯的資產儲存在臨時位置，並在明確批准資產後更新現有語言副本。 如果拒絕資產，則語言副本將保持不變。

1. 按一下/點擊下的源根資料夾 **[!UICONTROL 語言副本]** 已建立語言副本，然後按一下/點擊 **[!UICONTROL 在資產中顯示]** 開啟資料夾 [!DNL Assets]。
1. 從「資產」UI中，選擇已翻譯的資產，然後按一下/點擊 **[!UICONTROL 編輯]** 的子菜單。
1. 編輯資產，然後保存更改。
1. 執行第2-14步 [添加到現有翻譯項目](#add-to-existing-translation-project) 更新語言副本的過程。
1. 按一下/點擊位於 **[!UICONTROL 翻譯作業]** 平鋪。 從 **[!UICONTROL 翻譯作業]** 頁面中，您可以清楚地查看儲存已轉換的資產版本的臨時位置。
1. 選中旁邊的複選框 **[!UICONTROL 標題]**。
1. 在工具列中，按一下/點選「 **[!UICONTROL Accept Translation]** 」 (接受翻譯)，然後在對話方塊中按一下/點選「 **[!UICONTROL Accept]** 」 (接受)，以使用已編輯資產的翻譯版本覆寫目標資料夾中的翻譯資產。

   >[!NOTE]
   >
   >要啟用翻譯工作流來更新目標資產，請同時接受資產和元資料。

   按一下/點擊 **[!UICONTROL 拒絕翻譯]** 以在目標區域設定根目錄中保留資產的最初翻譯版本並拒絕編輯的版本。

1. 導航到Assets控制台，並開啟每個已轉換資產的「屬性」頁以查看已轉換的元資料。

<!-- TBD: Possibly this blog wasn't migrated. Still try to find from the author. Old one is archived at https://web.archive.org/web/20180423042713/https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/

For tips on translating metadata for assets efficiently, see [5 Steps to efficiently translate metadata](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/). 
-->

## 建立翻譯項目 {#creating-translation-projects}

要建立語言副本，請觸發「資產」UI中「參考」欄下可用的以下語言副本工作流之一：

**建立和翻譯**

在此工作流中，要翻譯的資產將複製到要翻譯的語言的語言的語言根中。 此外，根據您選擇的選項，將在「項目」控制台中為資產建立一個翻譯項目。 根據設定，可以手動啟動翻譯項目，或允許在建立翻譯項目後立即自動運行。

**更新語言副本**

您可以運行此工作流，以翻譯其他資產組，並將其包含在特定區域設定的語言副本中。 在這種情況下，已轉換的資產將添加到已包含先前轉換的資產的目標資料夾中。

>[!NOTE]
>
>資產二進位檔案僅在翻譯服務提供商支援二進位檔案的翻譯時才進行翻譯。

>[!NOTE]
>
>如果為複雜資產(如PDF檔案和Adobe InDesign檔案)啟動翻譯工作流，則不會提交其子元件或格式副本（如果有）以供翻譯。

### 建立和轉換工作流 {#create-and-translate-workflow}

首次使用建立和翻譯工作流為特定語言生成語言副本。 工作流提供以下選項：

* 僅建立結構
* 建立新的翻譯專案
* 新增至現有翻譯專案

### 僅建立結構 {#create-structure-only}

使用「 **僅建立結構** 」選項，在目標語言根目錄中建立目標資料夾層次結構，以匹配源語言根目錄中源資料夾的層次結構。在這種情況下，來源資產會複製到目標資料夾。但是，不會生成任何翻譯項目。

1. 在資產UI中，選擇要在目標語言根目錄中建立結構的源資料夾。
1. 開啟「參 **[!UICONTROL 考」窗格]** ，然後按一下「復本」下的「語言復本 **[!UICONTROL 」(Language Copies]****[!UICONTROL )]**。
1. 按一下/點擊 **[!UICONTROL 建立和翻譯]** 在底部。
1. 從 **[!UICONTROL 目標語言]** 清單中，選擇要為其建立資料夾結構的語言。
1. 從「專 **[!UICONTROL 案]** 」清單中，選 **[!UICONTROL 擇「僅建立結構」]**。
1. 按一下/點選「 **[!UICONTROL 建立]**」。目標語言的新結構列於 **[!UICONTROL 語言副本]**。
1. 按一下/點擊清單中的結構，然後按一下/點擊 **[!UICONTROL 在資產中顯示]** 導航到目標語言中的資料夾結構。

## 將翻譯雲服務應用於資料夾 {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager允許您使用您選擇的翻譯提供商提供的基於雲的翻譯服務，以確保根據您的要求翻譯您的資產。

您可以將翻譯雲服務直接應用到您的資產資料夾，以便在翻譯工作流期間利用這些服務。

### 應用翻譯服務 {#applying-the-translation-services}

將翻譯雲服務直接應用到您的資產資料夾，無需在建立或更新翻譯工作流時配置翻譯服務。

1. 從「資產」用戶介面中，選擇要應用翻譯服務的資料夾。
1. 在工具列中，按一下/點選「屬 **[!UICONTROL 性」圖示]** ，以顯示「資 **** 料夾屬性」頁面。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 導覽至「 **[!UICONTROL 雲端服務]** 」標籤。
1. 從「Cloud Service配置」清單中，選擇所需的翻譯提供程式。 例如，如果您想從Microsoft獲得翻譯服務，請選擇 **[!UICONTROL Microsoft翻譯]**。

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 選擇翻譯提供程式的連接器。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 在工具列中，按一下/點選「 **[!UICONTROL 儲存]**」，然後按一下「確定 **** 」以關閉對話方塊。轉譯服務會套用至資料夾。

### 應用自定義翻譯連接器 {#applying-custom-translation-connector}

如果要為要用於翻譯工作流的翻譯服務應用自定義連接器。要應用自定義連接器，請首先從 [包管理器。](/help/implementing/developing/tools/package-manager.md)然後，從雲端服務主控台設定連接器。在您設定連接器後，「套用轉譯服務」中所述的「雲端服務」標籤中的連接器清 [單中會顯示此連接器](#applying-the-translation-services)。在您應用自定義連接器並運行翻譯工作流後，翻譯項目的「 **[!UICONTROL Translation Summary]** 」 (翻譯摘要) 表徵圖會在heads **[!UICONTROL Provider]** and **[!UICONTROL Method下顯示連接器詳細資訊]**。

1. 從安裝連接器 [包管理器。](/help/implementing/developing/tools/package-manager.md)
1. 按一下/點擊Experience Manager徽標，然後導航至 **[!UICONTROL 工具>部署>Cloud Services]**。
1. 在「雲端服務」頁面的「 **[!UICONTROL 協力廠商服務]** 」下，找 **[!UICONTROL 出您安裝的連接器]** 。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 按一下/點擊 **[!UICONTROL 立即配置]** 連結以開啟 **[!UICONTROL 建立配置]** 對話框。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 指定連接器的標題和名稱，然後按一下/點選「建 **[!UICONTROL 立」]**。自訂連接器位於「套用轉譯服務」步驟5中所述「 **[!UICONTROL 雲端服務]** 」標籤的連 [接器清單中](#applying-the-translation-services)。
1. 在套用自訂連接器後，執行建立翻譯專案中說明的任何翻譯工作流程。驗證「項目」控制台中翻譯項 **[!UICONTROL 目的「翻譯摘要]** 」表徵圖中連接器的詳 **[!UICONTROL 細資訊]** 。

   ![chlimage_1-220](assets/chlimage_1-220.png)
