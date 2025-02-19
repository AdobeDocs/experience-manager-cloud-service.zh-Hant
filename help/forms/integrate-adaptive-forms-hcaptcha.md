---
title: 如何在AEM最適化表單中使用hCaptcha&amp； reg；？
description: 使用hCaptcha&amp；reg；服務輕鬆增強表單安全性。 內的逐步指南！
topic-tags: Adaptive Forms, author
keywords: 驗證碼&amp；reg；服務，最適化Forms， CAPTCHA挑戰，機器人預防，表單提交安全性，表單垃圾郵件預防
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: dc7ca723-1008-472a-b6eb-8e9ed6332a16
source-git-commit: 914139a6340f15ee77024793bf42fa30c913931e
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---

# 使用hCaptcha連線您的AEM Forms環境® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview">此功能在早期採用者計畫下。 您可以從您的官方電子郵件ID寫信到aem-forms-ea@adobe.com ，以加入率先採用者計畫並請求存取該功能。</span>

CAPTCHA （完全自動化公用圖靈測試來區分電腦和人之間的差異）是一種常用於線上交易的程式，以區分人和自動化程式或機器人。 這會帶來挑戰，並評估使用者的回應，以判斷其是否為人類或機器人與網站互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意目的來確保線上交易的安全。

AEM Forms as a Cloud Service支援下列驗證碼解決方案：

* [驗證碼](#integrate-aem-forms-environment-with-hcaptcha-captcha)
* [Cloudflare Turnstile](/help/forms/integrate-adaptive-forms-turnstile.md)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms.md)

## 將AEM Forms環境與hCaptcha驗證碼整合

hCaptcha®服務可保護您的表單免受機器人、垃圾郵件和自動濫用的侵擾。 這會提出核取方塊Widget質詢，並評估使用者回應，以判斷它是人類還是機器人與表單互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意活動來確保線上交易的安全。

AEM Forms as a Cloud Service支援最適化Forms中的hCaptcha®。 您可以用它來在表單提交時顯示核取方塊Widget挑戰。

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->

## 將AEM Forms環境與hCaptcha整合的必要條件® {#prerequisite}

若要使用AEM Forms設定hCaptcha®，您必須從hCaptcha®網站取得[hCaptcha®網站金鑰和秘密金鑰](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key)。

## 設定hCaptcha的步驟® {#steps-to-configure-hcaptcha}

1. 在您的AEM Forms as a Cloud Service環境中建立設定容器。 設定容器內含用來將AEM連線至外部服務的雲端設定。 若要建立並設定設定設定容器以使用hCaptcha連線您的AEM Forms環境®：
   1. 開啟您的AEM Forms as a Cloud Service執行個體。
   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. 在組態瀏覽器中，您可以選取現有資料夾或建立資料夾。 您可以建立檔案夾並為其啟用「雲端設定」選項，或為現有檔案夾啟用「雲端設定」選項：

      * **若要建立資料夾並啟用其雲端組態選項**：
         1. 在組態瀏覽器中，按一下&#x200B;**[!UICONTROL 建立]**。
         1. 在建立設定對話方塊中，指定名稱、標題，並選取&#x200B;**[!UICONTROL 雲端設定]**&#x200B;選項。
         1. 按一下&#x200B;**[!UICONTROL 建立]**。
      * 若要啟用現有資料夾的「雲端設定」選項：
         1. 在組態瀏覽器中，選取資料夾並選取&#x200B;**[!UICONTROL 屬性]**。
         1. 在[組態內容]對話方塊中，啟用&#x200B;**[!UICONTROL 雲端組態]**。
         1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並結束對話方塊。

1. 設定Cloud Service：
   1. 在您的AEM作者執行個體上，前往![tools-1](assets/tools-1.png) > **[!UICONTROL 雲端服務]**&#x200B;並選取&#x200B;**[!UICONTROL hCaptcha®]**。
      ui中的![hCaptcha®](assets/hcaptcha-in-ui.png)
   1. 選取已建立或已更新的設定容器，如上一節所述。 選取「**[!UICONTROL 建立]**」。
      ![組態hCaptcha®](assets/config-hcaptcha.png)
   1. 指定在先決條件](#prerequisite)中取得之hCaptcha®服務[的&#x200B;**[!UICONTROL 標題]**、**[!UICONTROL 名稱]**、**[!UICONTROL 網站金鑰]**&#x200B;和&#x200B;**[!UICONTROL 秘密金鑰]**。 選取「**[!UICONTROL 建立]**」。

      ![設定Cloud Service以使用hCaptcha連線您的AEM Forms環境®](assets/create-hcaptcha-config.png)

>[!NOTE]
> 使用者不需要修改[使用者端JavaScript驗證URL](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage)和[伺服器端驗證URL](https://docs.hcaptcha.com/#verify-the-user-response-server-side)，因為它們已預先填入hCaptcha®驗證。 對於某些國家/地區，端點可能會有所不同，如需詳細資訊，請造訪[驗證碼®常見問題集](https://docs.hcaptcha.com/faq#does-hcaptcha-support-access-by-users-in-china)。

設定hCAPTCHA服務後，就可在調適型表單中使用。

## 在最適化表單{#using-hCaptcha®-foundation-components}中使用hCaptcha®

1. 開啟您的AEM Forms as a Cloud Service執行個體。
1. 移至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
1. 選取最適化表單並選取&#x200B;**[!UICONTROL 屬性]**。 針對&#x200B;**[!UICONTROL 組態容器]**&#x200B;選項，選取包含連線AEM Forms與hCaptcha®的雲端組態的組態容器，然後選取&#x200B;**[!UICONTROL 儲存並關閉]**。

   如果您沒有這類設定容器，請參閱[使用hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service)連線您的AEM Forms環境一節，以瞭解如何建立設定容器。

   ![選取設定容器](/help/forms/assets/captcha-properties.png)

1. 選取最適化表單，然後選取&#x200B;**[!UICONTROL 編輯]**。 最適化表單會在最適化Forms編輯器中開啟。
1. 從元件瀏覽器中，將&#x200B;**[!UICONTROL 驗證碼]**&#x200B;元件拖放至最適化表單上。
1. 選取&#x200B;**[!UICONTROL 驗證碼]**&#x200B;元件並按一下屬性![屬性圖示](assets/configure-icon.svg)圖示。 它會開啟屬性對話方塊。

   ![替代文字](assets/hcaptcha-properties.png)

   指定下列屬性：

   * **[!UICONTROL 標題]：**&#x200B;指定驗證碼元件的標題，您可以在表單和規則編輯器中以唯一名稱輕鬆識別表單元件。
   * **[!UICONTROL 驗證訊息]：**&#x200B;提供表單提交時驗證碼驗證的驗證訊息。
   * **[!UICONTROL 驗證碼驗證]：**&#x200B;您可以選取下列其中一個選項來驗證驗證碼：
      * 在提交表單時
      * 使用者動作時。
   * **[!UICONTROL 驗證碼服務]：**&#x200B;選取您的驗證碼服務，這裡選取hCaptcha®服務。
   * **[!UICONTROL 驗證碼組態]：**&#x200B;選取為hCaptcha®設定的雲端組態。

     >[!NOTE]
     >
     > 基於類似目的，您的環境中可以有多個雲端設定。 因此，請謹慎選擇服務。 如果未列出任何服務，請參閱[使用hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service)連線您的AEM Forms環境，以瞭解如何建立將AEM Forms環境與hCaptcha®服務連線的Cloud Service。

   * **錯誤訊息：**&#x200B;提供驗證碼提交失敗時向使用者顯示的錯誤訊息。
   * **驗證碼大小：**&#x200B;您選取hCaptcha®挑戰對話方塊的顯示大小。 使用&#x200B;**[!UICONTROL Compact]**&#x200B;選項可顯示較小的大小，使用&#x200B;**[!UICONTROL Normal]**&#x200B;選項可顯示相對較大的hCaptcha®挑戰對話方塊，或使用&#x200B;**[!UICONTROL Invisible]**&#x200B;驗證hCaptcha®而不需在使用者介面上明確轉譯核取方塊Widget。

1. 選取「**[!UICONTROL 完成]**」。

現在，只有合法的表單，表單填寫者才能成功清除hCaptcha®服務帶來的挑戰，才能用於表單提交。

**hCaptcha®是Intuition Machines， Inc.的註冊商標。**

## 常見問題

* **問：我可以在最適化表單中使用多個驗證碼元件嗎？**
* **Ans：**&#x200B;不支援在最適化表單中使用一個以上的Captcha元件。 此外，不建議在片段或標示為延遲載入的面板中使用驗證碼元件。

## 另請參閱 {#see-also}

{{see-also}}
