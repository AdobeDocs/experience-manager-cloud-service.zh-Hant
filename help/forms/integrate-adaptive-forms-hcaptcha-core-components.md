---
title: 如何在AEM最適化表單核心元件中使用驗證碼&amp； reg；？
description: 使用 hCaptcha&reg; 服務輕鬆提升表單安全性。裡面有詳細的逐步指南！
topic-tags: Adaptive Forms, author
keywords: 驗證碼&amp；reg；服務，最適化Forms， CAPTCHA挑戰，機器人預防，核心元件，表單提交安全性，表單垃圾郵件預防
feature: Adaptive Forms, Core Components
exl-id: 6c559df2-7b6a-42fe-b44c-29a782570a0c
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 23%

---

# 使用hCaptcha連線您的AEM Forms環境® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview">此功能在早期採用者計畫下。 您可以使用官方電子郵件 ID 寫信至 aem-forms-ea@adobe.com，以加入早期採用者計劃並要求存取該功能。</span>

CAPTCHA （完全自動化公用圖靈測試來區分電腦和人之間的差異）是一種常用於線上交易的程式，以區分人和自動化程式或機器人。 它會提出質詢並評估使用者的回應，以判斷與網站互動的是真人還是機器人。它可防止使用者在測試失敗時繼續操作，並透過防止機器人發佈垃圾郵件或惡意目的來確保線上交易的安全。

AEM Forms as a Cloud Service支援下列驗證碼解決方案：

* [驗證碼](#integrate-aem-forms-environment-with-hcaptcha-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [驗證碼](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

## 將AEM Forms環境與hCaptcha驗證碼整合

hCaptcha® 服務可保護您的表單免受機器人、垃圾郵件和自動化濫用的侵擾。它會利用核取方塊小工具來提出質詢，並評估使用者的回應，以判斷與表單互動的是真人還是機器人。它可防止使用者在測試失敗時繼續操作，並透過防止機器人發佈垃圾郵件或惡意活動來確保線上交易的安全。

AEM Forms as a Cloud Service支援Adaptive Forms核心元件中的hCaptcha®。 您可以用它來在表單提交時顯示核取方塊Widget挑戰。

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### 將AEM Forms環境與hCaptcha整合的必要條件® {#prerequisite}

若要使用AEM Forms設定hCaptcha®，您必須從hCaptcha®網站取得[hCaptcha®網站金鑰和秘密金鑰](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key)。

### 設定驗證碼® {#steps-to-configure-hcaptcha}

若要將AEM Forms與hCaptcha®服務整合，請執行以下步驟：

1. 在您的AEM Forms as a Cloud Service環境中建立設定容器。 設定容器內含用來將AEM連線至外部服務的雲端設定。 若要建立並設定設定設定容器以使用hCaptcha連線您的AEM Forms環境®：
   1. 開啟您的AEM Forms as a Cloud Service執行個體。
   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. 在組態瀏覽器中，您可以選取現有資料夾或建立資料夾。 您可以建立檔案夾並為其啟用Cloud Configurations選項，或為現有檔案夾啟用Cloud Configurations選項：

      * 若要建立資料夾並為其啟用雲端設定選項：
         1. 在組態瀏覽器中，按一下&#x200B;**[!UICONTROL 建立]**。
         1. 在建立設定對話方塊中，指定名稱、標題，並選取&#x200B;**[!UICONTROL 雲端設定]**&#x200B;選項。
         1. 按一下「**[!UICONTROL 建立]**」。
      * 若要啟用現有資料夾的「雲端設定」選項：
         1. 在組態瀏覽器中，選取資料夾並選取&#x200B;**[!UICONTROL 屬性]**。
         1. 在[組態內容]對話方塊中，啟用&#x200B;**[!UICONTROL 雲端組態]**。
         1. 選取「**[!UICONTROL 儲存並關閉]**」，即可儲存設定並退出對話框。

1. 設定Cloud Service：
   1. 在您的AEM作者執行個體上，前往![tools-1](assets/tools-1.png) > **[!UICONTROL 雲端服務]**&#x200B;並選取&#x200B;**[!UICONTROL hCaptcha®]**。
      ui中的![hCaptcha®](assets/hcaptcha-in-ui.png)
   1. 選取已建立或已更新的設定容器，如上一節所述。 選取「**[!UICONTROL 建立]**」。
      ![組態hCaptcha®](assets/config-hcaptcha.png)
   1. 指定在Prerequisite **[!UICONTROL 中取得之hCaptcha®服務]**&#x200B;的&#x200B;**[!UICONTROL 標題]**、**[!UICONTROL 名稱]**、**[!UICONTROL 網站金鑰]**&#x200B;和[秘密金鑰](#prerequisite)。 選取「**[!UICONTROL 建立]**」。

      ![設定Cloud Service以使用hCaptcha連線您的AEM Forms環境®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > 使用者不需要修改[使用者端JavaScript驗證URL](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage)和[伺服器端驗證URL](https://docs.hcaptcha.com/#verify-the-user-response-server-side)，因為它們已預先填入hCaptcha®驗證。

   設定hCAPTCHA服務後，即可用於根據核心元件的[最適化表單](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/introduction)。

## 在最適化Forms核心元件中使用hCaptcha® {#using-hCaptcha&reg;-core-components}

1. 開啟您的AEM Forms as a Cloud Service執行個體。
1. 移至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
1. 選取最適化表單並選取&#x200B;**[!UICONTROL 屬性]**。 針對&#x200B;**[!UICONTROL 組態容器]**&#x200B;選項，選取包含連線AEM Forms與hCaptcha的雲端組態的組態容器®並選取&#x200B;**[!UICONTROL 儲存並關閉]**。

   如果您沒有這類設定容器，請參閱[使用hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service)連線您的AEM Forms環境一節，以瞭解如何建立設定容器。

   ![選取設定容器](/help/forms/assets/captcha-properties.png)

1. 選取最適化表單，然後選取&#x200B;**[!UICONTROL 編輯]**。 最適化表單會在最適化Forms編輯器中開啟。
1. 從元件瀏覽器中，拖放或新增&#x200B;**[!UICONTROL 最適化表單hCaptcha®]**&#x200B;元件至最適化表單。
1. 選取&#x200B;**[!UICONTROL 最適化表單hCaptcha®]**&#x200B;元件，然後按一下屬性![屬性圖示](assets/configure-icon.svg)圖示。 它會開啟屬性對話方塊。 指定下列屬性：

   ![hCaptcha® v2](assets/config-hcaptcha-v2.png)

   * **[!UICONTROL 名稱]：**&#x200B;指定驗證碼元件的名稱，您可以在表單和規則編輯器中以唯一名稱輕鬆識別表單元件。
   * **[!UICONTROL 標題]：**&#x200B;指定驗證碼元件的標題。
   * **[!UICONTROL 設定]：**&#x200B;選取已設定用於 hCaptcha® 的雲端設定。
   * **驗證碼大小：**&#x200B;您可以選取hCaptcha®挑戰對話方塊的顯示大小。 使用&#x200B;**[!UICONTROL 精簡]**&#x200B;選項可顯示小尺寸，使用&#x200B;**[!UICONTROL 正常]**&#x200B;選項可顯示相對大尺寸的 hCaptcha® 質詢對話框。<!-- or **[!UICONTROL Invisible]** to validate hCaptcha&reg; without explicitly rendering the checkbox widget on the user interface. -->
   * **[!UICONTROL 驗證訊息]：**&#x200B;提供表單提交時驗證碼驗證的驗證訊息。
   * **[!UICONTROL 指令碼驗證訊息]** - 此選項可讓您輸入訊息，以在指令碼驗證失敗時顯示。

     >[!NOTE]
     >基於類似目的，您的環境中可以有多個雲端設定。 因此，請謹慎選擇服務。 如果未列出任何服務，請參閱[使用hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service)連線您的AEM Forms環境，以瞭解如何建立將AEM Forms環境與hCaptcha®服務連線的Cloud Service。

   <!--* **Error Message:** Provide the error message to display to the user when the Captcha submission fails.-->

1. 選取「**[!UICONTROL 完成]**」。


現在，只有合法的表單，表單填寫者才能成功清除hCaptcha®服務帶來的挑戰，才能用於表單提交。 hCaptcha®

**hCaptcha® 是 Intuition Machines, Inc. 的註冊商標。**


## 常見問題

* **問：我可以在最適化表單中使用多個驗證碼元件嗎？**
* **Ans：**&#x200B;不支援在最適化表單中使用一個以上的Captcha元件。 此外，不建議在片段或標示為延遲載入的面板中使用驗證碼元件。

## 另請參閱 {#see-also}

{{see-also}}
