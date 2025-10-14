---
title: 建立資產資料夾 - Headless 設定
description: 使用 AEM 內容片段模型定義內容片段的結構，這是 Headless 內容的基礎。
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 97%

---

# 建立資產資料夾 - Headless 設定 {#creating-an-assets-folder}

使用 AEM 內容片段模型定義內容片段的結構，這是 Headless 內容的基礎。然後將內容片段儲存在資產資料夾中。

## 什麼是資產資料夾？ {#what-is-an-assets-folder}

[現在您已經建立內容片段模型](create-content-model.md)，它定義您未來內容片段所需的結構，您可能很想建立一些片段。

但是，您首先需要建立可以儲存片段的資產資料夾。

資產資料夾用於[組織傳統內容資產](/help/assets/manage-digital-assets.md)，例如影像和影片，連同內容片段。

## 如何建立資產資料夾 {#how-to-create-an-assets-folder}

管理員只需要偶爾建立資料夾來組織建立的內容。出於本快速入門指南的目的，我們只需要建立一個資料夾。

1. 登入 AEM as a Cloud Service，然後從主選單中選取&#x200B;**導覽 > 資產 -> 檔案**。
1. 選取「**建立 > 資料夾**」。
1. 為您的資料夾提供 **標題**&#x200B;和&#x200B;**名稱**。
   * **標題** 應該是描述性的。
   * **名稱**&#x200B;會成為存放庫中的節點名稱。
      * 它會根據標題自動產生，並根據 [AEM 命名慣例](/help/implementing/developing/introduction/naming-conventions.md)進行調整。
      * 如有需要，可加以調整。

   ![建立資料夾](../assets/assets-folder-create.png)
1. 透過將游標停留並點選核取記號來選取剛建立的資料夾。然後從工具列中選取「**屬性**」(或使用 `p`[&#x200B; 鍵盤快速鍵](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md))。
1. 在&#x200B;**屬性**&#x200B;視窗中，選擇&#x200B;**雲端服務**&#x200B;索引標籤。
1. 針對&#x200B;**雲端設定**，選取您先前建立的[設定](create-configuration.md)。
   ![設定資產資料夾](../assets/assets-folder-configure.png)
1. 選取「**儲存並關閉**」。
1. 在確認視窗中選取「**確定**」。

   ![確認視窗](../assets/assets-folder-confirmation.png)

您可以在剛建立的資料夾中建立其他子資料夾。子資料夾將繼承父資料夾的&#x200B;**雲端設定**。但是，如果您想使用來自另一個設定的模型，可以覆寫此設定。

如果您使用的是當地語系化網站結構，則可以在新資料夾下[建立語言根](/help/assets/translate-assets.md)。

## 後續步驟 {#next-steps}

現在您已經為內容片段建立資料夾，您可以繼續進行快速入門指南的第四部分並[建立內容片段](create-content-fragment.md)。

>[!TIP]
>
>如需有關管理內容片段的完整詳細資訊，請參閱[內容片段文件](/help/sites-cloud/administering/content-fragments/overview.md)
