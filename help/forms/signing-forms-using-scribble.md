---
title: 如何使用手寫簽名將電子簽章套用至表單？
description: 瞭解如何使用手寫簽名將電子簽章套用至表單。
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 9%

---

# 使用手寫簽名對表單進行電子簽章{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/creating-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html) |
| AEM as a Cloud Service  | 本文章 |


您可以使用&#x200B;**草寫簽章**&#x200B;元件和&#x200B;**簽章步驟**&#x200B;元件，在最適化表單上繪製（草寫）簽章。 簽章步驟元件會顯示最適化表單的PDF版本。 您需要啟用記錄檔案選項或表單範本式的最適化Forms ，才能使用簽名步驟元件。

![手寫簽名對話方塊](assets/scribble-signature.png)

## 簽章視窗中可用的各種選項

* **A：**&#x200B;按一下&#x200B;**繪圖筆刷**&#x200B;圖示，在畫布上繪製您的簽名。
* **B：**&#x200B;按一下&#x200B;**清除**&#x200B;圖示以清除畫布上的簽章。
* **C：**&#x200B;按一下&#x200B;**地理位置**&#x200B;圖示以新增地理位置以及簽章。
* **D：**&#x200B;按一下&#x200B;**鍵盤**&#x200B;圖示，在畫布上輸入您的名稱。

一旦您在「草寫簽名」視窗中選取「完成![aem_forms_save](assets/aem_forms_save.png)」圖示，便無法編輯簽名。 如果想要編輯簽名，則必須忽略目前的簽名，並使用上面的「繪圖筆刷/鍵盤」選項重新簽名。

您可以選取&#x200B;**設定** ![設定圖示](assets/configure.png)圖示來設定手寫簽名畫布的外觀比例。
* 當「草寫簽名」畫布的外觀比例小於1時，地理位置資訊會新增至「草寫簽名」畫布底部。


* 當Scribble Signature畫布的外觀比例大於1時，地理位置資訊會新增到Scribble Signature畫布的右側。


![手寫簽章 — 底部](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>簽名一律以PNG格式儲存。
>

## 設定最適化表單以使用草寫簽名 {#configure-an-adaptive-form-to-use-scribble-signature}

1. 建立已啟用記錄檔案選項或表單範本式的最適化表單。 如需逐步資訊，請參閱[建立最適化表單](creating-adaptive-form.md)。
1. 將&#x200B;**手寫簽章**&#x200B;元件從元件瀏覽器拖放至最適化表單。
1. 選取&#x200B;**設定** ![設定](assets/configure.png)圖示。 它會開啟屬性瀏覽器並顯示草寫簽名元件的屬性。 設定手寫簽名元件的屬性。
1. 將簽章步驟元件從元件瀏覽器拖放至調適型表單。

   >[!NOTE]
   >
   >簽章步驟元件會佔據表單可用的完整寬度。 建議在包含簽章步驟元件的區段上不要有任何其他元件。

1. 在內容瀏覽器中，選取&#x200B;**表單容器**，然後選取&#x200B;**設定** ![設定圖示](assets/configure.png)圖示。 它會開啟屬性瀏覽器並顯示最適化表單容器屬性。 導覽至&#x200B;**最適化表單容器** > **電子簽章**，並取消選取&#x200B;**啟用Adobe Sign**&#x200B;選項。 選取「完成![aem_forms_save](assets/aem_forms_save.png)」圖示以儲存變更。

   >[!NOTE]
   >
   >將簽名步驟元件新增至最適化表單時，會自動選取「啟用Adobe Sign」選項。

1. 選取&#x200B;**設定** ![設定](assets/configure.png)圖示。 它會開啟屬性瀏覽器並顯示簽章步驟屬性。 設定下列屬性：

   * **元素名稱**：指定元件的名稱。

   * **標題：**&#x200B;指定元件的唯一標題。
   * **範本訊息：**&#x200B;指定載入簽章PDF時要顯示的訊息。 Adobe Sign服務需要一些時間準備和載入簽名PDF。
   * **簽署服務：**&#x200B;選取&#x200B;**草寫簽章**&#x200B;選項。

   * **CSS類別**：指定使用者端程式庫的CSS類別（如果有的話）。 Adobe建議使用[主題](themes.md)和[內嵌樣式](inline-style-adaptive-forms.md)，而非CSS類別。

   選取「完成![aem_forms_save](assets/aem_forms_save.png)」圖示以儲存變更。 已成功設定簽章。

   現在，當您填寫表單時，會顯示最適化表單的PDF版本，並提供簽署PDF檔案的選項。 如需詳細資訊，請參閱[使用草寫簽章簽署最適化表單](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)。

## 使用草寫簽名簽署調適型表單 {#sign-an-adaptive-form-using-scribble-signature}

1. 填寫最適化表單並到達簽名步驟頁面後，簽名畫面會隨即顯示。

   EchoSign頁面的![簽章畫面](assets/esignscribblesign.jpg)

1. 按一下&#x200B;**[!UICONTROL 簽署]**。 會出現scribble sign對話方塊。 簽署表單，然後按一下「完成![aem_forms_save](assets/aem_forms_save.png)」圖示以儲存簽名。

   ![手寫簽名對話方塊](assets/scribblewidget.png)

1. 按一下[完成]完成簽署程式。

   ![完成簽署程式](assets/scribblecomplete.jpg)

簽名會新增至表單，而表單控制項會移至下一個面板。

## 另請參閱 {#see-also}

{{see-also}}