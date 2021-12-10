---
title: 使用元件的最佳實務
seo-title: Best practices for working with components
description: 使用最適化表單元件時應注意的一些最佳實務和要點
seo-description: Some best practices and key points to remember when working with Adaptive Form components
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# 使用元件的最佳實務{#best-practices-for-working-with-components}

使用適用性表單元件時應記住的一些最佳實務和要點如下：

* 每個元件都具有控制其外觀和功能的關聯屬性。 若要設定元件的屬性，請點選元件並點選 ![屬性](assets/Smock_Wrench_18_N.svg) 在「屬性」瀏覽器中開啟元件屬性。
* 元件以其元素名稱來識別。 當您點選 ![屬性](assets/Smock_Wrench_18_N.svg)，您可以變更 **[!UICONTROL 元素名稱]** 屬性瀏覽器中的欄位值。 「元素名稱」欄位僅接受字母、數字、連字型大小(-)和底線(_)。 不允許使用其他特殊字元，元素名稱應以字母開頭。

* 只要表單上顯示標題，您就可以修改表單編輯器中內嵌的適用性表單元件的標題屬性，而不需開啟「屬性」瀏覽器。 若要這麼做：

   1. 點選以選取具有 **[!UICONTROL 標題]** 屬性及其 **[!UICONTROL 隱藏標題]** 屬性已停用。

   1. 點選 ![編輯圖示](assets/Smock_Edit_18_N.svg) 讓標題可編輯。

   1. 修改標題並點選「Return（返回）」鍵，或點選元件外部的任何位置以儲存變更。 點選Esc鍵以捨棄變更。

* 有些適用性表單元件（例如電子郵件和電話）包含現成可用的驗證模式。 不過，您可以更新 **[!UICONTROL 驗證模式]** 欄位（位於元件屬性中的「模式」設定追蹤器下）。 請參閱上表中的元件說明，以取得預設驗證的詳細資訊。

* 適用性Forms欄位（例如數值方塊和電子郵件）可設定為包含專用的HTML5輸入類型。 當這些欄位集中在移動設備和平板電腦上時，鍵盤會在前面顯示通常用於輸入欄位資訊的特定字母、數字和字元。 它可幫助用戶快速輸入資訊，而無需在鍵盤上的字元集之間切換。 若要允許元件的專用輸入，請啟用 **[!UICONTROL 使用HTML類型編號]** 複選框。

* 您可以啟用文本框元件以接受RTF。 若要啟用文字方塊的RTF文字，請啟用 **[!UICONTROL 允許RTF文字]** 核取元件屬性中的方塊。

* 您可以啟用文本框、電子郵件和電話元件，從儲存在瀏覽器自動填充設定中的資訊自動填充名稱、地址、信用卡、電話和電子郵件等欄位的值。 若要啟用此功能，請選取 **[!UICONTROL 啟用自動填充]** 在元件屬性中，選取 **[!UICONTROL 自動填充屬性]**. 當使用者填入適用性表單時，系統會根據使用者先前填入的值，從瀏覽器中的自動填入設定檔建議值。 請注意，如果開啟了使用者瀏覽器中的自動填入設定，自動填入即可運作。

* 指定選項按鈕和 `{value}={text}` 格式。
* 預設情況下，檔案附件元件允許用戶僅附加一個檔案。 不過，您可以配置元件屬性以支援多個附件。 此外，如果用戶附加了多個檔案，且檔案名相同，則附件可能會造成一些問題。 因此，建議在提交表單時，為每個已提交的附件建立唯一識別碼。 若要這麼做：

   1. 在 [!DNL AEM Forms] 伺服器，導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web主控台]**.
   1. 尋找和點選 **[!UICONTROL 適用性Forms Configuration Service]**.
   1. 在適用性Forms設定服務對話方塊中，啟用 **[!UICONTROL 使檔案名稱唯一]**. 預設為停用。

* 若要讓使用者能使用Safari瀏覽器附加PDF，請確定 **application/pdf** 已添加到「檔案附件」元件的「受支援的檔案類型」屬性中。 使用先前版本建立的適用性Forms [!DNL AEM Forms] 版本可包含 **.pdf** 而非 **application/pdf** 在「支援的檔案類型」屬性中。

>[!NOTE]
>
>適用性表單元件不支援從右到左(RTL)語言。 例如，希伯來語。