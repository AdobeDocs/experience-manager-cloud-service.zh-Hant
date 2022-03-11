---
title: 如何建立多步表單序列？
description: '與 [!DNL Experience Manager Forms]，您可以為用戶定義一系清單單面板，以導航和填充自適應表單。 以用例方法為例，深入挖掘，建立多步形式序列。 '
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 多步形式序列簡介 {#introduction-to-multi-step-form-sequence}

自適應Forms使表單作者能夠輕鬆地建立多步資料捕獲體驗。 它提供了內置支援，用於建立多個面板並將每個面板與不同的導航模式相關聯。 表單作者可以在邏輯部分中對表單域進行分組，並將組表示為面板。 使用面板佈局控制面板之間的整體導航。 作者可以選擇以不同佈局排列面板，例如，使用「嚮導」佈局按順序放置面板，或使用「頁籤式佈局」以臨時方式放置面板。 有關面板佈局的資訊，請參見 [自適應Forms的佈局功能](layout-capabilities-adaptive-forms.md)。

在典型的表單填充體驗中，涉及的步驟比僅捕獲資料還要多。 完整的表單提交可以包括其他步驟，如數字簽名表單、驗證表單中填充的資訊、處理付款等。 不同的案例。

如果您的使用案例要求執行一組資料捕獲步驟，或者有一些管理法規需要執行某些步驟， [!DNL Experience Manager Forms] 提供了一種方法，可跨表單強制實施該公共結構。 表單結構的預先實現定義了表單的步驟順序。 ![多步表單序列示例](assets/formpipeline.png)

多步表單序列示例

讓我們採用一個必須為表單建立填充、驗證、簽名和確認步驟的序列的使用案例。 建立此序列的步驟如下：

1. 定義表單模板並向其添加所需的面板。 序列中的每個步驟應有一個面板。 但是，可以在面板中包括子面板。

   在本示例中，我們可以添加以下面板：

   * **[!UICONTROL 填充]**:它包含用於捕獲資料的表單域。 在此，您可以包括嵌套的子面板，以為不同類型的資訊建立節，如個人、家庭、財務等。

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL 電子簽名]**:它包含 **[!UICONTROL 簽名]** 可用於基於XFA的自適應表單的元件。 它提供以下簽名服務：

      * Adobe Document Cloud電子簽名服務
      * Scribble簽名
   * **[!UICONTROL 確認]**:它包含 **[!UICONTROL 摘要]** 元件，它顯示一條消息，確認用戶在簽署表單後提交表單，並進入序列中的「確認（摘要）」步驟。 作者可以配置 [!UICONTROL 摘要] 元件、顯示感謝消息、顯示到生成的PDF的連結等。



1. 選擇根面板的佈局作為 **[!UICONTROL 嚮導]**。
1. 完成其餘步驟以建立表單模板。 <!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

在表單模板中定義表單序列後，您可以使用它建立具有將基本結構定義為已就位序列的表單，不過您始終可以自定義表單以滿足您的要求。
