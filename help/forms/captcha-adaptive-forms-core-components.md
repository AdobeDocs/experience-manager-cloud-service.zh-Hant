---
title: 根據核心元件在最適化表單中使用Google reCAPTCHA
description: 使用Google reCAPTCHA服務輕鬆增強表單安全性。 內的逐步指南！
topic-tags: Adaptive Forms, author
hide: true
hidefromtoc: true
Keywords: Google reCAPTCHA service, Adaptive Forms, CAPTCHA challenge, Bot prevention, Core Components, Form submission security, Form spam prevention
source-git-commit: 4f2a51502202fba3792cde370180d127f8e17418
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# 根據核心元件在最適化Forms中使用reCAPTCHA {#using-reCAPTCHA-in-adaptive-forms}

CAPTCHA （完全自動化公用圖靈測試來區分電腦和人之間的差異）是一種常用於線上交易的程式，以區分人和自動化程式或機器人。 這會帶來挑戰，並評估使用者的回應，以判斷其是否為人類或機器人與網站互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意目的來確保線上交易的安全。

[!DNL AEM Forms] as a [!DNL Cloud Service] 在最適化Forms中支援Google reCAPTCHA v2。 您可以用它來在表單提交時提出驗證碼質詢。 在最適化表單中使用reCAPTCHA：

1. [透過Google的reCAPTCHA服務連線您的AEM Forms環境](#connect-your-forms-environment-with-recaptcha-service-by-google)
1. [設定最適化表單，以在表單提交時顯示驗證碼質詢](#using-reCAPTCHA)

## 透過Google的reCAPTCHA服務連線您的AEM Forms環境 {#connect-your-forms-environment-with-recaptcha-service-by-google}

若要使用Google的reCAPTCHA服務連線您的AEM Forms環境

1. 取得 [reCAPTCHA API金鑰組](https://www.google.com/recaptcha/admin) 來自Google。 它包含 **網站金鑰** 和 **秘密金鑰**.

   ![建立Google網站的Google reCAPTCHA組態以取得reCAPTCHA金鑰](/help/forms/assets/google-captcha.gif)
1. 在您的AEM Formsas a Cloud Service環境中建立設定容器。 設定容器內含用來將AEM連線至外部服務的雲端設定。 若要建立並設定設定設定容器，以透過Google將您的AEM Forms環境與reCAPTCHA服務連線：
   1. 開啟您的AEM Formsas a Cloud Service執行個體。
   1. 前往 **[!UICONTROL 「工具」>「一般」>「設定瀏覽器」]**. 在設定瀏覽器中，您可以：
   1. 選取現有資料夾或建立資料夾。 您可以
      * 建立資料夾並為其啟用雲端設定選項：
         1. 在設定瀏覽器中，按一下 **[!UICONTROL 建立]**.
         1. 在建立組態對話方塊中，指定名稱、標題，然後選取 **[!UICONTROL 雲端設定]** 選項。
         1. 按一下 **[!UICONTROL 建立]**
            ![建立雲端設定，將您的AEM Forms環境與Google的reCAPTCHA服務連線](/help/forms/assets/create-configuration.png){width="50%"}
      * 啟用現有資料夾的「雲端設定」選項：
         1. 在設定瀏覽器中，選取資料夾並點選 **[!UICONTROL 屬性]**.
         1. 在組態內容對話方塊中，啟用 **[!UICONTROL 雲端設定]**.
         1. 點選 **[!UICONTROL 儲存並關閉]** 以儲存組態並結束對話方塊。

1. 設定Cloud Service：
   1. 在您的AEM編寫執行個體上，前往 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** 然後點選 **[!UICONTROL reCAPTCHA]**.
   1. 選取在前一節中建立或更新的「設定容器」。 點選「**[!UICONTROL 建立]**」。
   1. 指定 **[!UICONTROL 標題]**， **[!UICONTROL 名稱]**， **[!UICONTROL 網站金鑰]**、和 **[!UICONTROL 秘密金鑰]** reCAPTCHA服務（在步驟1取得）。 點選「**[!UICONTROL 建立]**」。
      ![設定Cloud Service以透過Google使用reCAPTCHA服務連線您的AEM Forms環境](/help/forms/assets/captcha-configuration.gif)

   在設定reCAPTCHA服務後，就可在調適型表單中使用。 如需詳細資訊，請參閱 [在最適化表單中使用Google reCAPTCHA](#using-reCAPTCHA).


## 在最適化表單中使用Google reCAPTCHA {#using-reCAPTCHA}

若要在最適化Forms中使用reCAPTCHA：

1. 開啟您的AEM Formsas a Cloud Service執行個體。
1. 前往 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取最適化Forms並點選 **[!UICONTROL 屬性]**. 對於 **[!UICONTROL 設定容器]** 選項，選取包含雲端設定的設定容器，此雲端設定會透過Google將AEM Forms與reCAPTCHA服務連線，然後點選 **[!UICONTROL 儲存並關閉]**.

   如果您沒有這類設定容器，請參閱區段 [透過Google的reCAPTCHA服務連線您的AEM Forms環境](#connect-your-forms-environment-with-recaptcha-service-by-google) 以瞭解如何建立這類設定容器。

   ![選取設定容器](/help/forms/assets/captcha-properties.png)
1. 選取最適化Forms並點選 **[!UICONTROL 編輯]**. 最適化表單會在最適化Forms編輯器中開啟。
1. 在元件瀏覽器中，拖放 **[!UICONTROL 最適化表單reCAPTCHA]** 元件至最適化表單。

   Google reCAPTCHA驗證常有時效性，約一分鐘後過期。 因此，Adobe建議將 **[!UICONTROL 最適化表單reCAPTCHA]** 元件位於 **[!UICONTROL 提交]** 按鈕。

1. 選取 **[!UICONTROL 最適化表單reCAPTCHA]** 元件並點選屬性 ![屬性圖示](assets/configure-icon.svg) 圖示。 它會開啟屬性對話方塊。 指定下列強制屬性：
   * **[!UICONTROL 名稱]：** 在表單和規則編輯器中，您可以使用表單元件的唯一名稱輕鬆識別表單元件，但名稱不得包含空格或特殊字元。
   * **[!UICONTROL 驗證碼組態]：** 選取雲端設定，設定為顯示表單的Google reCAPTCHA對話方塊。 基於類似目的，您的環境中可以有多個雲端設定。 因此，請謹慎選擇服務。 若未列出任何服務，請參閱 [透過Google的reCAPTCHA服務連線您的AEM Forms環境](#connect-your-forms-environment-with-recaptcha-service-by-google) 以瞭解如何建立一個Cloud Service，將您的AEM Forms環境與Google的reCAPTCHA服務連線起來。
   * **驗證碼大小：** 您可以選取Google reCAPTCHA挑戰對話方塊的顯示大小。 使用 **[!UICONTROL 精簡]** 顯示小尺寸和 **[!UICONTROL 一般]** 用於顯示相對較大的Google reCAPTCHA挑戰對話方塊的選項。

1. 點選 **[!UICONTROL 完成]**.

   現在， **受reCAPTCHA保護** 會顯示在您的Adaptive Form上。 它會顯示在所有設定為可使用Google reCAPTCHA服務的最適化Forms上。

   現在，僅允許提交合法表單，其中表單填寫者成功清除Google reCAPTCHA服務帶來的挑戰。
   ![Google受reCAPTCHA徽章保護](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Tap the component, select ![edit rules](assets/edit-rules-icon.svg), and tap **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Tap the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## 常見問答

**問：我可以在最適化表單中使用多個驗證碼元件嗎？**
**Ans：** 不支援在最適化表單中使用多個驗證碼元件。 此外，不建議在標籤為延遲載入的片段或面板中使用驗證碼元件。

