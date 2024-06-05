---
title: 建立頁面
description: 瞭解如何使用Sites主控台為您的網站建立新頁面。
exl-id: 77264562-e76a-40c8-9878-847a8878fb8e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# 建立頁面 {#creating-pages}

瞭解如何使用為您的網站建立新頁面 **網站** 主控台。

>[!TIP]
>
>開始建立新頁面之前，請先熟悉 [AEM中頁面的組織方式。](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

## 存取許可權 {#access-privileges}

您的帳戶需要適當的存取許可權才能建立頁面。

如果您遇到任何問題，請聯絡您的系統管理員。

## 建立新頁面 {#creating-a-new-page}

除非所有頁面都已預先為您建立，否則您必須先建立頁面，然後才能開始建立內容：

1. 開啟 [此 **網站** 主控台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 導覽至您要建立新頁面的位置。
1. 使用開啟下拉式選擇器 **建立** 在工具列中選取「 」 **頁面** 從清單：

   ![建立頁面](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. 從精靈的第一階段，您可以：

   * 選取您要用來建立新頁面的範本，然後選取 **下一個** 以繼續進行。

   * **取消** 以中止程式。

   ![為新頁面選取範本](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. 從精靈的最後階段開始，您可以：

   * 使用三個索引標籤來輸入 [頁面屬性](/help/sites-cloud/authoring/sites-console/page-properties.md) 您想要指派給新頁面，然後選取 **建立** 以實際建立頁面。

   * 使用 **返回** 以返回範本選取。

   主要欄位包括：

   * **標題**：

      * 這會向使用者顯示，且是強制性的。

   * **名稱**：

      * 這會用來產生URI。 如果未指定，則會從標題衍生名稱。
      * 如果您提供頁面 **名稱** 建立頁面時，AEM [根據慣例驗證名稱](/help/implementing/developing/introduction/naming-conventions.md) 由AEM和JCR所強制。
      * 您 **無法提交無效的字元** 在 **名稱** 欄位。 當AEM偵測到無效字元時，該欄位會反白顯示，並顯示說明訊息，指出需要移除/取代的字元。

   >[!TIP]
   >
   >另請參閱 [頁面命名慣例](#page-naming-conventions).

   建立頁面所需的最低資訊為 **標題**.

   ![提供頁面標題](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. 點選或按一下 **建立** 以完成程式並建立您的新頁面。 確認對話方塊會詢問您是否要 **開啟** 立即頁面或返回主控台(**完成**)。 選取一個以結束頁面建立程式。

   ![頁面建立成功](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   * 如果您選擇 **開啟**，則 **網站** console會根據新頁面的範本，開啟適當的編輯器：
      * [頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)
      * [通用編輯器](/help/sites-cloud/authoring/universal-editor/authoring.md)

如果您返回主控台，便可看到新頁面：

![產生的新頁面](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!NOTE]
>
>如果您使用相同位置已存在的名稱來建立頁面，AEM會以附加編號所指定之名稱的變數來建立頁面。 例如，如果 `beach` 已存在，則新頁面會變成 `beach1`.

>[!CAUTION]
>
>建立頁面後，無法變更其範本，除非您 [使用新範本建立啟動項](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)，但會遺失任何現有內容。
