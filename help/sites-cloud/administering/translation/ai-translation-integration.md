---
title: 設定AI翻譯整合
description: 瞭解如何使用翻譯雲端服務和翻譯整合架構，將Adobe Experience Manager連線至Azure OpenAI以進行代理式翻譯。
feature: Language Copy
role: Admin
badgeSaas: label="AEM Sites" type="Positive" tooltip="適用於AEM Sites)。"
solution: Experience Manager Sites
source-git-commit: cb7dcc07a5913d6c7e88e0eec03f0003f1e3997a
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# 設定AI翻譯整合 {#ai-translation-integration}

AI翻譯整合可讓您使用&#x200B;**大型語言模型(LLM)**&#x200B;作為您在Adobe Experience Manager中編寫內容的翻譯服務。 您可以將AEM連線至您的LLM提供者（從Microsoft Azure OpenAI開始）、重複使用與其他聯結器相同的[翻譯工作流程](/help/sites-cloud/administering/translation/overview.md)，並選擇性地上傳&#x200B;**翻譯風格指南**，讓AEM可以產生在不同地區設定保持語調、術語和品牌語言一致的規則。

如需翻譯專案、雲端設定和翻譯整合架構的背景，請參閱[翻譯多語言網站的內容](overview.md)和[設定翻譯整合架構](integration-framework.md)。

## AI翻譯如何融入AEM {#how-ai-translation-fits-in-aem}

大型語言模型可以翻譯完整的段落，並注意上下文、語調和成語，而不是文字逐字替換。 當您設定AI翻譯整合時，LLM會像您透過AEM連線的其他提供者一樣，當作&#x200B;**協力廠商翻譯服務**。 您為LLM服務提供您&#x200B;**自己的授權和認證**。

初始支援會將AEM連線至&#x200B;**Azure OpenAI**。 Adobe計畫在較新版本中新增對其他提供者的支援。

您同時在&#x200B;**翻譯雲端服務**&#x200B;中設定LLM連線和選用的樣式指南，以及其他翻譯設定。 您可以針對不同的[雲端設定](/help/sites-cloud/administering/translation/integration-framework.md#creating-a-translation-integration-configuration)使用不同的翻譯服務；例如，一個設定可以使用AI翻譯，而另一個設定則使用傳統的機器翻譯聯結器。

## 設定翻譯雲端服務 {#configure-translation-cloud-services}

在管理其他翻譯雲端設定的相同區域中設定AI翻譯。

1. 在[全域導覽功能表](/help/sites-cloud/authoring/basic-handling.md#global-navigation)中，選取&#x200B;**工具** > **雲端服務** > **翻譯雲端服務**。
1. 開啟或建立您要啟用AI轉譯的設定（如果功能應廣泛套用，則包括`/conf/global`）。

![Translation Cloud Services主控台顯示管理翻譯設定的位置。](assets/ai-translation-integration/aem_ai-translation_translation-cloud-services.png)

## 設定LLM連線 {#configure-the-llm-connection}

**代理翻譯組態**&#x200B;體驗包含您連線提供者的&#x200B;**LLM組態**&#x200B;區段。

1. 開啟翻譯雲端服務專案的AI翻譯設定。
1. 選取&#x200B;**[!UICONTROL LLM設定]**。
1. 選擇您的提供者（例如，**Azure OpenAI**）。
1. 輸入您的訂閱的必要認證和端點詳細資料（**API金鑰**、**API版本**、**基本路徑**、**部署名稱**&#x200B;以及您的提供者所需的任何其他欄位）。
1. 儲存設定。

![具有LLM Config索引標籤和Azure OpenAI欄位的Agentic Translation Configuration畫面。](assets/ai-translation-integration/aem_ai-translation_agentic-translation-llm-config.png)

## 新增翻譯樣式參考線和產生的規則 {#add-translation-style-guides-and-generated-rules}

您可以上傳&#x200B;**翻譯樣式指南**&#x200B;檔案（通常每個目標語言一份）。 AEM會分析每份指南，並產生&#x200B;**翻譯規則**，讓輸出符合您的品牌和語言期望。

1. 在&#x200B;**代理翻譯組態**&#x200B;中，選取&#x200B;**[!UICONTROL LLM Guidelines]**。
1. 選擇地區設定並使用&#x200B;**[!UICONTROL 上傳]**&#x200B;來新增該語言的樣式參考檔案。
1. AEM處理指南時，狀態指標顯示進度（**處理**、**已完成**&#x200B;或&#x200B;**已中止**）。
1. 在編輯器中檢閱或編輯產生的規則（例如，擷取膚色、術語和範例的JSON）。

![LLM Guidelines索引標籤顯示選定語言的地區設定清單和產生的翻譯規則。](assets/ai-translation-integration/aem_ai-translation_agentic-translation-llm-guidelines.png)

## 在框架中設定預設翻譯方法 {#set-the-default-translation-method-in-the-framework}

儲存雲端設定後，當您建立翻譯專案時，請在[翻譯整合架構](integration-framework.md)設定中將&#x200B;**代理翻譯**&#x200B;註冊為預設行為。 您可以視需要變更每個專案的方法。

![顯示包含代理翻譯的翻譯方法選項的[翻譯整合框架網站]索引標籤。](assets/ai-translation-integration/aem_ai-translation_translation-integration-framework-default.png)

## 執行翻譯專案 {#run-translation-projects}

設定AI翻譯並將其與您的頁面關聯後，您就可以像與其他翻譯提供者一樣[建立和執行翻譯專案](managing-projects.md)。 頁面、內容片段和資產中的內容會遵循您的翻譯規則和框架設定。

>[!NOTE]
>
>AI翻譯整合是&#x200B;**無法**&#x200B;從Adobe Experience Manager](/help/implementing/cloud-manager/ai-assistant-in-aem.md)聊天UI中的[AI助理或從Experience Production Agent介面取得。 使用本文所述的翻譯工作流程和控制檯。

