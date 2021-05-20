---
title: 建立內容片段模型無頭快速入門手冊
description: 使用「內容片段模型」，定義您要使用AEM無頭功能建立和提供的內容結構。
exl-id: 8e3e4d00-34d3-4d4f-bc3a-43b8a322b986
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 建立內容片段模型無頭快速入門手冊{#creating-content-fragment-models}

使用「內容片段模型」，定義您要使用AEM無頭功能建立和提供的內容結構。

## 什麼是內容片段模型？{#what-are-content-fragment-models}

[現在您已建立設定，](create-configuration.md) 可以使用它來建立內容片段模型。

內容片段模型會定義您要在AEM中建立和管理的資料和內容的結構。 它們可以充當內容的支架。 選擇建立內容時，作者將從您定義的內容片段模型中選取，以引導他們建立內容。

## 如何建立內容片段模型{#how-to-create-a-content-fragment-model}

資訊架構師只會偶爾執行這些工作，因為需要新模型。 在本快速入門手冊中，我們只需建立一個模型。

1. 以Cloud Service身分登入AEM，然後在主功能表中選取&#x200B;**工具 — >資產 — >內容片段模型**。
1. 點選或按一下建立設定所建立的資料夾。

   ![模型資料夾](../assets/models-folder.png)
1. 點選或按一下&#x200B;**建立**。
1. 提供&#x200B;**模型標題**、**標籤**&#x200B;和&#x200B;**說明**。 您也可以選擇/取消選擇&#x200B;**啟用模型**&#x200B;以控制建立時是否立即啟用模型。

   ![建立模型](../assets/models-create.png)
1. 在確認視窗中，點選或按一下&#x200B;**開啟**&#x200B;以設定您的模型。

   ![確認窗口](../assets/models-confirmation.png)
1. 使用&#x200B;**內容片段模型編輯器**，從&#x200B;**資料類型**&#x200B;欄拖放欄位，以建立內容片段模型。

   ![拖放欄位](../assets/models-drag-and-drop.png)

1. 放置欄位後，必須配置其屬性。 編輯器會自動切換至新增欄位的&#x200B;**屬性**&#x200B;標籤，您可在此提供必填欄位。

   ![設定屬性](../assets/models-configure-properties.png)
1. 完成模型建置後，點選或按一下「**儲存**」。 新建立的模型保存在&#x200B;**草稿**&#x200B;模式中。

   ![拔模模式下的模型](../assets/models-draft.png)
1. 必須啟用模型才能使用它（如果尚未啟用）。 選取您剛建立的模型，然後點選或按一下「**啟用**」。

   ![啟用模型](../assets/models-enable.png)
1. 點選或按一下確認對話方塊中的&#x200B;**啟用**&#x200B;以確認已啟用模型。

   ![啟用確認對話方塊](../assets/models-enabling.png)
1. 模型現已啟用並可供使用。

   ![已啟用模型](../assets/models-enabled.png)

**內容片段模型編輯器**&#x200B;支援許多不同的資料類型，例如簡單文字欄位、資產參考、其他模型的參考，以及JSON資料。

您可以建立多個模型。 模型可參考其他內容片段。 使用[configurations](create-configuration.md)組織模型。

## 後續步驟{#next-steps}

現在您已透過建立模型來定義內容片段的結構，您可以繼續前往快速入門手冊的第三部分，以及[建立資料夾，以便儲存片段本身。](create-assets-folder.md)

>[!TIP]
>
>如需內容片段模型的完整詳細資訊，請參閱[內容片段模型檔案](/help/assets/content-fragments/content-fragments-models.md)
