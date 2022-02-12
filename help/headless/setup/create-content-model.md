---
title: 建立內容片段模型 — 無頭設定
description: 通過使用內容片段模型，定義將建立和使用無AEM頭功能提供服務的內容的結構。
exl-id: 8e3e4d00-34d3-4d4f-bc3a-43b8a322b986
source-git-commit: e81b852dc90e3cc5abc8b9f218f48d0fc1cc66eb
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 建立內容片段模型 — 無頭設定 {#creating-content-fragment-models}

通過使用內容片段模型，定義將建立和使用無AEM頭功能提供服務的內容的結構。

## 什麼是內容片段模型？ {#what-are-content-fragment-models}

[既然已建立配置，](create-configuration.md) 可以使用它建立內容片段模型。

內容片段模型定義要在中建立和管理的資料和內容的結AEM構。 它們是你內容的腳手架。 選擇建立內容時，作者將從您定義的內容片段模型中選擇，該模型將指導他們建立內容。

## 如何建立內容片段模型 {#how-to-create-a-content-fragment-model}

資訊架構師只會在需要新模型時偶爾執行這些任務。 為了完成本入門指南的目的，我們只需建立一個模型。

1. 登錄AEM到as a Cloud Service並從主菜單選擇 **工具 — >資產 — >內容片段模型**。
1. 按一下或按一下通過建立配置建立的資料夾。

   ![模型資料夾](../assets/models-folder.png)
1. 點擊或按一下 **建立**。
1. 提供 **模型標題**。 **標籤** 和 **說明**。 您也可以選擇/取消選擇 **啟用模型** 控制在建立時是否立即啟用模型。

   ![建立模型](../assets/models-create.png)
1. 在確認窗口中，點擊或按一下 **開啟** 來配置模型。

   ![確認窗口](../assets/models-confirmation.png)
1. 使用 **內容片段模型編輯器**，通過從 **資料類型** 的雙曲餘切值。

   ![拖放欄位](../assets/models-drag-and-drop.png)

1. 放置欄位後，必須配置其屬性。 編輯器將自動切換到 **屬性** 的子菜單。

   ![配置屬性](../assets/models-configure-properties.png)

1. 構建完模型後，點擊或按一下 **保存**。

1. 新建立模型的模式取決於是否選取 **啟用模型** 建立模型時：
   * 選定 — 新模型將已 **已啟用**
   * 未選定 — 將在中建立新模型 **草稿** 模式

1. 如果尚未啟用，則模型必須 **已啟用** 才能使用它。
   1. 選取剛建立的模型，然後點擊或按一下 **啟用**。

      ![啟用模型](../assets/models-enable.png)
   1. 按一下或按一下確認啟用模型 **啟用** 的子菜單。

      ![啟用確認對話框](../assets/models-enabling.png)
1. 模型現已啟用並可供使用。

   ![已啟用模型](../assets/models-enabled.png)

的 **內容片段模型編輯器** 支援許多不同的資料類型，如簡單文本欄位、資產引用、對其他模型的引用和JSON資料。

可以建立多個模型。 模型可以引用其他內容片段。 使用 [配置](create-configuration.md) 來組織模型。

## 後續步驟 {#next-steps}

現在，您已通過建立模型定義了內容片段的結構，您可以轉到入門指南的第三部分， [建立資料夾，您將在其中儲存片段。](create-assets-folder.md)

>[!TIP]
>
>有關內容片段模型的完整詳細資訊，請參閱 [內容片段模型文檔](/help/assets/content-fragments/content-fragments-models.md)
