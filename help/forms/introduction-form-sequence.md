---
title: 如何建立多步驟表單順序？
description: 替換為 [!DNL Experience Manager Forms]，您可以定義一系列表單面板，讓使用者導覽及填寫最適化表單。 以使用案例法為例，深入瞭解如何建立多步驟表單序列。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 2%

---

# 多步驟表單序列簡介 {#introduction-to-multi-step-form-sequence}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/introduction-form-sequence.html) |
| AEM as a Cloud Service  | 本文 |

最適化Forms可讓表單作者輕鬆建立多步驟資料擷取體驗。 隨附內建支援，可建立多個面板，以及將每個面板與不同導覽模式建立關聯。 表單作者可將邏輯區段中的表單欄位分組，並將群組表示為面板。 面板之間的整體導覽會使用面板配置來控制。 作者可以選擇以不同的版面配置來排列面板，例如，使用「精靈」版面配置按順序放置，或使用「索引標籤」版面配置以臨機操作方式放置。 如需面板配置的相關資訊，請參閱 [Adaptive Forms的版面配置功能](layout-capabilities-adaptive-forms.md).

在典型的表單填寫體驗中，除了擷取資料以外，還有更多步驟需要處理。 完整的表單提交可包括其他步驟，例如以數位方式簽署表單、驗證表單中填寫的資訊、處理付款等。 每個案例都不同。

如果您的使用案例需要一組資料擷取步驟，或有一些法規需要遵循某些步驟， [!DNL Experience Manager Forms] 提供一種在表單間實施該通用結構的方法。 表單結構的預先實施會定義表單的步驟順序。 ![多步驟表單序列的範例](assets/formpipeline.png)

多步驟表單序列的範例

請讓我們舉一個使用案例，您必須在表單中建立填寫、驗證、簽署和確認步驟的順序。 建立此類序列的步驟如下：

1. 定義表單範本並在其中新增必要面板。 序列中的每個步驟都應該有一個面板。 不過，您可以在面板中包含子面板。

   在此範例中，我們可以新增下列面板：

   * **[!UICONTROL 填滿]**：其中包含用於擷取資料的表單欄位。 在這裡，您可以包含巢狀子面板，以針對不同型別的資訊（例如個人、家庭、財務等）建立區段。

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL 電子簽章]**：此變數包含 **[!UICONTROL 簽署]** 可以在XFA型最適化表單中使用的元件。 它提供下列簽署服務：

      * Adobe Document Cloud eSign服務
      * 草寫簽名

   * **[!UICONTROL 確認]**：此變數包含 **[!UICONTROL 摘要]** 在使用者簽署表單並到達序列中的確認（摘要）步驟後，顯示確認表單提交的訊息的元件。 作者可以設定 [!UICONTROL 摘要] 元件、顯示感謝訊息、顯示產生PDF的連結等。

1. 選取根面板的版面配置為 **[!UICONTROL 精靈]**.
1. 完成其餘步驟以建立表單範本。 <!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

在表單範本中定義表單順序後，您可以使用它來建立具有定義為現有順序的基本結構的表單，不過您可以隨時自訂表單以符合您的需求。
