---
title: 使用手寫簽名將電子簽名應用到表單
seo-title: Apply electronic signatures to a form using scribble signatures
description: 使用手寫方式簽署表單
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# 使用手寫簽名將電子簽名應用到表單{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

您可以使用 **手寫簽名** 元件與 **簽名步驟** 在最適化表單上繪製（手寫）簽名的元件。 簽章步驟元件會顯示最適化表單的PDF版本。 您需要啟用記錄檔選項或基於表單範本的適用性Forms，才能使用簽名步驟元件。

這兩個元件都提供一個窗口，如下所示，用於簽署表單。 您也可以按一下地理位置圖示 ![aem_6_3_geolocation](assets/aem_6_3_geolocation.png) 將地理位置添加到簽名。

![手寫簽名對話框](assets/scribble-signature.png)

## 設定最適化表單以使用手寫簽名 {#configure-an-adaptive-form-to-use-scribble-signature}

1. 啟用「建立記錄檔案」選項或基於表單模板的最適化表單。 如需逐步資訊，請參閱 [建立最適化表單](creating-adaptive-form.md).
1. 拖放 **手寫簽名** 元件（從元件瀏覽器）到最適化表單。
1. 點選 **設定** ![設定](assets/configure.png) 表徵圖。 它會開啟屬性瀏覽器並顯示手寫簽名元件的屬性。 配置手寫簽名元件的屬性。
1. 將「簽名步驟」元件從元件瀏覽器拖放至最適化表單。

   >[!NOTE]
   >
   >簽名步驟元件佔用表單可用的全寬。 建議在包含簽名步驟元件的區段上不要有任何其他元件。

1. 在內容瀏覽器中，點選 **表單容器**，然後點選 **設定** ![](assets/configure.png) 表徵圖。 它會開啟屬性瀏覽器並顯示適用性表單容器屬性。 導覽至 **適用性表單容器** > **電子簽名** 並取消選取 **啟用Adobe Sign** 選項。 點選完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示以儲存變更。

   >[!NOTE]
   >
   >將簽名步驟元件新增至適用性表單時，會自動選取啟用Adobe Sign選項。

1. 點選 **設定** ![設定](assets/configure.png) 表徵圖。 它會開啟屬性瀏覽器並顯示簽名步驟屬性。 設定下列屬性：

   * **元素名稱**:指定元件的名稱。

   * **標題：** 指定元件的唯一標題。
   * **範本訊息：** 指定在載入簽名PDF時要顯示的消息。 Adobe Sign服務需要一些時間來準備和載入簽名PDF。
   * **簽名服務：** 選取 **手寫簽名** 選項。

   * **CSS類**:指定用戶端程式庫的CSS類別（如果有）。 建議使用 [主題](themes.md) 和 [行內樣式](inline-style-adaptive-forms.md) 而非CSS類別。

   點選完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示以儲存變更。 已成功配置簽名。

   現在，當您填寫表單時，會顯示PDF版適用性表單，並提供簽署PDF檔案的選項。 如需詳細資訊，請參閱 [使用手寫簽名簽署最適化表單](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## 使用手寫簽名簽署最適化表單 {#sign-an-adaptive-form-using-scribble-signature}

1. 填寫適用性表單並進入簽名步驟頁面後，會顯示簽名螢幕。

   ![EchoSign頁面的簽名螢幕](assets/esignscribblesign.jpg)

1. 按一下 **[!UICONTROL Sign]**. 手寫符號對話框出現。 簽署表單，然後按一下完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 表徵圖保存簽名。

   ![手寫簽名對話框](assets/scribblewidget.jpg)

1. 按一下「完成」以完成簽署程式。

   ![完成簽署程式](assets/scribblecomplete.jpg)

簽名將添加到表單中，表單控制項將移到下一個面板。

