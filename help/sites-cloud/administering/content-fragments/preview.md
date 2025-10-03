---
title: 預覽內容片段
description: 瞭解如何透過一系列方法預覽您的內容片段。
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
source-git-commit: 3781b494394405f69892686790c17ffa9c69f28b
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---

# 預覽內容片段 {#previewing-content-fragments}

內容片段可用於Headless傳送和頁面製作。 由於片段僅是內容，不含格式，因此對其進行審查可能更具挑戰性。 因此，我們提供多種方法，可在各種情況下預覽您的片段。

有數種方法可用於內容片段，從主控台片段主控台和編輯器可存取。 本節中說明的主控台和編輯器是針對Headless內容傳送而開發（雖然它們可用於所有情境）。

您可以預覽您的片段：

* 使用[預覽URL模式](#preview-url-pattern)

* 透過發佈至[預覽執行個體](#preview-instance)並從中取消發佈

<!--
* with a HTML template, using **[Preview]()** from the Content Fragments console
-->

當然，您也可以在[內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md)中檢視您的片段。

>[!IMPORTANT]
>
>可以從兩個主控台存取內容片段： **內容片段**&#x200B;和&#x200B;**Assets**。
>
>編寫內容片段時也有兩個編輯器；雖然基本功能相同，但有一些差異。 兩個編輯器都可從兩個主控台存取。
>
>本節處理&#x200B;**內容片段**&#x200B;主控台和&#x200B;*新*&#x200B;內容片段編輯器。 這些是針對Headless內容傳送開發的（儘管可用於所有情境）
>
>如需進一步詳細資訊，請參閱：
>
>* 使用&#x200B;**Assets**&#x200B;主控台進行[管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)
>* 使用&#x200B;[*原始*&#x200B;內容片段編輯器](/help/assets/content-fragments/content-fragments-variations.md)，
>* 使用[內容片段進行頁面編寫](/help/sites-cloud/authoring/fragments/content-fragments.md)。

## 預覽 URL 模式 {#preview-url-pattern}

內容片段編輯器為作者提供在外部前端應用程式中預覽其編輯的選項。

若要使用此功能，您首先需要：

* 與您的IT團隊合作，設定外部前端應用程式，該應用程式會透過使用其JSON輸出來呈現內容片段。

* 設定外部前端應用程式時，**預設預覽URL模式**&#x200B;必須定義為適當內容片段模式[的](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#model-properties)屬性。

預覽URL應遵循此模式：

    `https://<preview_url>?param=${expression}`

可用的運算式包括：

* `${contentFragment.path}`
* `${contentFragment.model.path}`
* `${contentFragment.model.name}`
* `${contentFragment.variation}`
* `${contentFragment.id}`

定義URL後，編輯器頂端工具列中的&#x200B;**[預覽](/help/sites-cloud/administering/content-fragments/authoring.md#preview-content-fragment)**&#x200B;按鈕會變成使用中狀態。 您可以選取此按鈕來啟動外部應用程式（在單獨的索引標籤中）以呈現內容片段。

## 預覽例項 {#preview-instance}

您可以&#x200B;**發佈**&#x200B;和&#x200B;**取消發佈**，將您的片段發佈到您的&#x200B;**[預覽服務](/help/headless/deployment/architecture.md)** （以及您的發佈執行個體）。

您可以從編輯器或控制檯發佈您的片段。

請參閱：

* [發佈並預覽片段](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment)以取得完整詳細資訊。

* [正在取消發佈片段](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment)，以取得完整詳細資訊。

<!--
## Preview based on a HTML Template {#preview-based-on-a-html-template}

The Content Fragment console provides a **Preview** option for every fragment.

The icon can be selected to open a dialog that represents the fragment based on a HTML template. You can use the default template, or develop and load your own.
-->
