---
title: 使用內容片段AJO外部參考擴充功能
description: 瞭解內容片段AJO外部參考擴充功能
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: 79c90e6b-91da-4f5a-ac96-a98ef7f8d4cd
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# 內容片段AJO外部參考擴充功能 {#content-fragment-external-references-extension}

若要在其他Adobe產品上預覽來自AEM的體驗，您可以啟用UI擴充功能：

* **AJO外部參考**

AJO外部參考擴充功能的運作方式是，從與預先定義標籤相關的所有組織和沙箱中擷取內容片段的參考。 擴充功能接著會顯示詳細資料。

例如，若要與Adobe Journey Optimizer (AJO)整合，詳細資訊取決於參考為行銷活動、歷程或範本。

>[!NOTE]
>
>如需如何啟用擴充功能的詳細資訊，請參閱[AEM Experience Manager中的Extension Manager。](https://developer.adobe.com/uix/docs/extension-manager/)

例如，若要搭配AJO使用擴充功能：

>[!NOTE]
>
>另請參閱[AJO整合](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/integrations/aem-fragments)。

1. 開啟[內容片段主控台](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)。

1. 導覽至您的內容片段 — 在各種AJO頻道中建立和使用的片段。

1. 在[編輯器](/help/sites-cloud/administering/content-fragments/managing.md#editing-the-content-of-your-fragment)中開啟您的內容片段。

1. AJO外部參考擴充功能可在右側面板中作為索引標籤使用。 選取索引標籤以開啟擴充功能：

   ![AJO外部參考擴充功能](/help/sites-cloud/administering/content-fragments/assets/cf-ajo-fragment-external-references-extension.png)

   選取參照型別後，擴充功能會將對應的外部參照顯示為包含欄的表格：

   * **名稱**：使用內容片段的參考名稱
   * **預覽**&#x200B;選取此連結以開始預覽
   * **狀態**：參考的狀態

1. 您可以從下拉式清單中選取&#x200B;**參考型別**，以在三種參考型別之間切換：

   * **行銷活動**
      * 顯示所有行銷活動的清單，其中包含目前內容片段的連結。
      * 然後您可以預覽選取的行銷活動。
      * 預設
   * **歷程**
      * 顯示最新的歷程。
      * 接著，您可以選取並預覽選取的歷程。
   * **範本**
      * 顯示與內容片段相關的範本。
      * 然後，您可以選取並預覽選取的範本。
