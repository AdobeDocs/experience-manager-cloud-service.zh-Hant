---
title: 使用元件的最佳做法
seo-title: Best practices for working with components
description: 使用Adaptive Form元件時需要注意的一些最佳做法和要點
seo-description: Some best practices and key points to remember when working with Adaptive Form components
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# 使用元件的最佳做法{#best-practices-for-working-with-components}

使用「自適應表單」元件時要記住的一些最佳做法和要點如下：

* 每個元件都具有控制其外觀和功能的關聯屬性。 要配置元件的屬性，請點擊該元件並點擊 ![屬性](assets/Smock_Wrench_18_N.svg) 在「屬性」瀏覽器中開啟元件屬性。
* 元件用其元素名稱標識。 點擊 ![屬性](assets/Smock_Wrench_18_N.svg)，可通過更改 **[!UICONTROL 元素名稱]** 屬性瀏覽器中的欄位值。 「元素名稱」欄位僅接受字母、數字、連字元(-)和下划線(_)。 不允許使用其他特殊字元，元素名稱應以字母開頭。

* 只要表單上的標題可見，您就可以在表單編輯器中內聯修改Adaptive Form元件的Title屬性，而不開啟「屬性」瀏覽器。 為此：

   1. 點擊以選擇具有 **[!UICONTROL 標題]** 財產 **[!UICONTROL 隱藏標題]** 屬性已禁用。

   1. 點擊 ![編輯表徵圖](assets/Smock_Edit_18_N.svg) 的子菜單。

   1. 修改標題並點擊「Return（返回）」鍵，或點擊元件外部的任何位置以保存更改。 按一下Esc鍵放棄更改。

* 一些自適應表單元件（如電子郵件和電話）包括開箱驗證模式。 但是，可以通過更新 **[!UICONTROL 驗證模式]** 欄位。 有關預設驗證的詳細資訊，請參閱上表中的元件說明。

* 自適應Forms欄位（如數字框和電子郵件）可配置為包括專用HTML5輸入類型。 當這些欄位集中在移動設備和平板電腦上時，鍵區會預先顯示通常用於輸入欄位中資訊的特定字母、數字和字元。 它幫助用戶快速輸入資訊，而無需在鍵盤上的字元集之間切換。 要允許對元件進行專用輸入，請啟用 **[!UICONTROL 使用HTML類型編號]** 的子菜單。

* 您可以啟用文本框元件來接受富格文本。 要為文本框啟用RTF，請啟用 **[!UICONTROL 允許富格文本]** 的子菜單。

* 您可以啟用文本框、電子郵件和電話元件，以便從瀏覽器自動填充設定中儲存的資訊自動填充欄位（如名稱、地址、信用卡、電話和電子郵件）的值。 要啟用此功能，請選擇 **[!UICONTROL 啟用自動填充]** 在元件屬性中，選擇 **[!UICONTROL 自動填充屬性]**。 當用戶填充自適應表單時，這些值會從瀏覽器中的自動填充配置檔案中或基於用戶先前填充的值進行建議。 請注意，如果開啟了用戶瀏覽器中的自動填充設定，自動填充將起作用。

* 指定中單選按鈕和複選框項的值 `{value}={text}` 的子菜單。
* 預設情況下，「檔案」附件元件允許用戶僅附加一個檔案。 但是，您可以配置元件屬性以支援多個附件。 此外，如果用戶附加了多個具有相同檔案名的檔案，則附件可能會導致一些問題。 因此，建議在提交表單時為每個已提交附件關聯唯一標識符。 為此：

   1. 在 [!DNL AEM Forms] 伺服器，導航至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
   1. 查找並點擊 **[!UICONTROL 自適應Forms配置服務]**。
   1. 在「自適應Forms配置服務」對話框中，啟用 **[!UICONTROL 使檔案名唯一]**。 預設情況下，它是禁用的。

* 要使用戶能夠使用Safari瀏覽器附加PDF，請確保 **應用程式/pdf** 添加到「檔案」附件元件的「支援的檔案類型」屬性。 自適應Forms使用上一個 [!DNL AEM Forms] 版本包含 **.pdf** 而不是 **應用程式/pdf** 在「支援的檔案類型」屬性中。

>[!NOTE]
>
>自適應表單元件不支援從右到左(RTL)語言。 例如，希伯來語。