---
title: 如何在AEM最適化表單中使用Turnstile？
description: 透過Turnstile服務輕鬆增強表單安全性。 內的逐步指南！
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
exl-id: 644c351b-a167-4d18-8b99-b7cae6be48d5
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 2%

---

<span class="preview"> 此功能在早期採用者計畫下。 您可以從您的官方電子郵件ID寫信到aem-forms-ea@adobe.com ，以加入率先採用者計畫並請求存取該功能。 </span>

CAPTCHA （完全自動化公用圖靈測試來區分電腦和人之間的差異）是一種常用於線上交易的程式，以區分人和自動化程式或機器人。 這會帶來挑戰，並評估使用者的回應，以判斷其是否為人類或機器人與網站互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意目的來確保線上交易的安全。

AEM Formsas a Cloud Service支援下列CAPTCHA解決方案：

* [Cloudflare Turnstile](#integrate-aem-forms-environment-with-turnstile-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms.md)
* [驗證碼](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## 將AEM Forms環境與Turnstile驗證碼整合

Cloudflare的Turnstile驗證碼是一種安全性措施，旨在保護表單和網站免受自動化機器人、惡意攻擊、垃圾郵件和不需要的自動化流量的傷害。 在允許提交表單前，它會在表單提交上顯示核取方塊，以驗證使用者是否為人類。 AEM Formsas a Cloud Service支援Adaptive Forms核心元件中的Turnstile驗證碼。

<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

### 整合AEM Forms環境與Turnstile驗證碼的必要條件 {#prerequisite}

若要設定AEM Forms核心元件的Turnstile，您必須取得 [轉門式網站金鑰與秘密金鑰](https://developers.cloudflare.com/turnstile/get-started/) 來自Turnstile網站。

### 為AEM Forms設定Turnstile的步驟{#steps-to-configure-turnstile}

1. 在您的AEM Formsas a Cloud Service環境中建立設定容器。 設定容器內含用來將AEM連線至外部服務的雲端設定。 若要建立並設定設定設定容器，以將您的AEM Forms環境與Turnstile連線：
   1. 開啟您的AEM Formsas a Cloud Service執行個體。
   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. 在組態瀏覽器中，您可以選取現有資料夾或建立資料夾。 您可以建立檔案夾並為其啟用「雲端設定」選項，或為現有檔案夾啟用「雲端設定」選項：

      * **若要建立資料夾並啟用其雲端設定選項**：
         1. 在設定瀏覽器中，按一下 **[!UICONTROL 建立]**.
         1. 在建立組態對話方塊中，指定名稱、標題，然後選取 **[!UICONTROL 雲端設定]** 選項。
         1. 按一下&#x200B;**[!UICONTROL 建立]**。
      * 若要啟用現有資料夾的「雲端設定」選項：
         1. 在組態瀏覽器中，選取資料夾並選取 **[!UICONTROL 屬性]**.
         1. 在組態內容對話方塊中，啟用 **[!UICONTROL 雲端設定]**.
         1. 選取 **[!UICONTROL 儲存並關閉]** 以儲存組態並結束對話方塊。

1. 設定Cloud Service：
   1. 在您的AEM編寫執行個體上，前往 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** 並選取 **[!UICONTROL Turnstile]**.
      ![Ui中的Turnstile](assets/turnstile-in-ui.png)
   1. 選取已建立或已更新的設定容器，如上一節所述。 選取「**[!UICONTROL 建立]**」。
      ![組態旋轉門](assets/config-hcaptcha.png)
   1. 指定 **[!UICONTROL Widget型別]** 若為Managed，Widget型別可能會變更，這取決於先決條件、 **[!UICONTROL 標題]**， **[!UICONTROL 名稱]**， **[!UICONTROL 網站金鑰]**、和 **[!UICONTROL 秘密金鑰]** 用於Turnstile服務 [取得於先決條件](#prerequisite). 選取「**[!UICONTROL 建立]**」。

      ![設定Cloud Service以將AEM Forms環境與Turnstile連線](assets/config-turntstile.png)

>[!NOTE]
> 使用者不需要修改使用者端JavaScript驗證URL和伺服器端驗證URL，因為已預先填入Turnstile驗證。

設定Turnstile驗證碼服務後，就可在調適型表單中使用。

## 在最適化表單中使用 Turnstile{#using-turnstile-foundation-components}

1. 開啟您的AEM Formsas a Cloud Service執行個體。
1. 前往 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取最適化表單並選取 **[!UICONTROL 屬性]**. 對於 **[!UICONTROL 設定容器]** 選項，選取包含將AEM Forms與Turnstile連線的雲端設定的設定容器，然後選取 **[!UICONTROL 儲存並關閉]**.

   如果您沒有這類設定容器，請參閱區段 [使用Turnstile連線您的AEM Forms環境](#connect-your-forms-environment-with-turnstile-service) 以瞭解如何建立設定容器。

   ![選取設定容器](/help/forms/assets/captcha-properties.png)

1. 選取最適化表單並選取 **[!UICONTROL 編輯]**. 最適化表單會在最適化Forms編輯器中開啟。
1. 在元件瀏覽器中，拖放 **[!UICONTROL 驗證碼]** 元件至最適化表單。
1. 選取 **[!UICONTROL 驗證碼]** 元件並按一下屬性 ![屬性圖示](assets/configure-icon.svg) 圖示。 它會開啟屬性對話方塊。

   ![設定](assets/turnstile-setting-v1.png)

   指定下列屬性：

   * **[!UICONTROL 標題]：** 指定驗證碼元件的標題，您可以在表單和規則編輯器中以表單元件的唯一名稱輕鬆識別表單元件。
   * **[!UICONTROL 驗證訊息]：** 提供驗證訊息，用於驗證表單提交時的驗證碼。
   * **[!UICONTROL 驗證碼驗證]：** 您可以選取其中一個選項來驗證驗證碼：
      * 在提交表單時
      * 使用者動作時。
   * **[!UICONTROL 驗證碼服務]：** 選取您的驗證碼服務，在這裡您選取Cloudfare Turnstile驗證碼服務。
   * **[!UICONTROL 驗證碼組態]：** 選取為Turnstile設定的雲端設定。 例如，您可在此選取 **Managed金鑰**.
     >[!NOTE]
     >基於類似目的，您的環境中可以有多個雲端設定。 因此，請謹慎選擇服務。 若未列出任何服務，請參閱 [使用Turnstile連線您的AEM Forms環境](#connect-your-forms-environment-with-turnstile-service) 瞭解如何建立將AEM Forms環境與Turnstile服務連結的Cloud Service。

   * **錯誤訊息：** 提供驗證碼提交失敗時向使用者顯示的錯誤訊息。
   * **驗證碼大小：** 您可以選取Turnstile challenge對話方塊的顯示大小。 使用 **[!UICONTROL 精簡]** 顯示小尺寸和 **[!UICONTROL 一般]** 可顯示相對較大的Turnstile挑戰對話方塊的選項。


     >[!NOTE]
     >這適用於Widget型別「受管理」和「非互動」。 如果Widget型別不可見，則不需要使用size屬性，且會停用。

1. 選取「**[!UICONTROL 完成]**」。

現在，只有合法的表單，表單填寫者才能成功清除Turnstile服務帶來的挑戰，才能提交表單。

![Turnstile挑戰](assets/turnstile-challenge.png)

## 常見問題

* **問：我可以在最適化表單中使用多個驗證碼元件嗎？**
* **Ans：** 不支援在最適化表單中使用多個驗證碼元件。 此外，不建議在片段或標示為延遲載入的面板中使用驗證碼元件。

## 另請參閱 {#see-also}

{{see-also}}
