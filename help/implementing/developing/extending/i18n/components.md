---
title: 國際化元件
description: 將您的元件和對話方塊國際化，以便以不同的語言呈現它們的UI字串
topic-tags: components
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 0276b310-b9a9-44b6-b295-06c51ef17208
source-git-commit: 401685af02c720994d72cd95d36f0cfcdf15d198
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# 國際化元件{#internationalizing-components}

將您的元件和對話方塊國際化，以便以不同的語言呈現它們的UI字串。 專為國際化設計的元件可讓UI字串外部化、翻譯，然後匯入存放庫。 在執行階段，使用者的語言偏好設定或頁面地區設定會決定UI中要顯示的語言。

![i18n-components-1.png](/help/implementing/developing/extending/assets/i18n-comp1.png)

使用以下程式將您的元件國際化，並提供不同語言的UI：

1. [使用將字串國際化的程式碼實作您的元件。](/help/implementing/developing/extending/i18n/dev.md)您的程式碼會識別要翻譯的字串，並選取要在執行階段顯示的語言。
1. [建立字典](/help/implementing/developing/extending/i18n/translator.md#creating-a-dictionary)。
1. [匯出](/help/implementing/developing/extending/i18n/translator.md#exporting-a-dictionary)字典為XLIFF格式，翻譯字串，然後將XLIFF檔案匯回AEM。
1. 將字典合併至應用程式的發行管理程式中。

>[!NOTE]
>
>這裡所說明的國際化元件方法，是用來轉譯靜態字串。 當元件字串預期會變更時，您應使用傳統的翻譯工作流程。 例如，當作者可以在元件的「編輯」對話方塊中使用屬性來編輯UI字串時，您不應使用語言字典來將字串國際化。

## 語言字典 {#language-dictionaries}

AEM國際化架構使用存放庫中的字典，以其他語言儲存英文字串及其翻譯。 架構使用英文作為預設語言。 字串的識別方式為英文版。 國際化架構通常使用英數ID作為UI字串。 使用英文版的字串做為ID有許多優點：

* 程式碼易於閱讀。
* 預設語言一律可用。

[翻譯工具](/help/implementing/developing/extending/i18n/translator.md)可讓您從一個中央位置管理所有字典。

![i18n-components-2](/help/implementing/developing/extending/assets/i18n-comp2.png)

必須透過AEM as a Cloud Service中的[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)，從Git變更翻譯。

### 在系統字典中覆蓋字串 {#overlaying-strings-in-system-dictionaries}

如果您的元件使用AEM系統字典中包含的字串，請複製您自己的字典中的字串。 所有元件都將使用字典中的字串。

請注意，當字串在位於`/apps`節點下方的字典中重複時，您無法預測要使用哪個翻譯。
