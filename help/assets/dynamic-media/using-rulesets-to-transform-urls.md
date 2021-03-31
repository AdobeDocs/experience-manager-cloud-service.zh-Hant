---
title: 使用規則集轉換URL
description: 瞭解如何在Dynamic Media部署規則集以轉換URL。 規則集是以指令碼語言（例如JavaScript™）編寫的指令集，可評估XML資料，並在資料符合特定條件時採取特定動作。
topic: 業務從業人員
role: 業務從業人員
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 6%

---


# 使用規則集轉換URL {#using-rulesets-to-transform-urls}

您可以在Dynamic Media部署規則集以轉換URL。 規則集是以指令碼語言（例如JavaScript™）編寫的指令集，可評估XML資料，並在資料符合特定條件時採取特定動作。 每個規則都包含至少一個條件和至少一個動作。 規則會根據條件評估XML資料，如果符合條件，則會採取適當的動作。 規則集的範例包括：

* 添加MIME類型尾碼。 許多服務和網站都需要影像字尾，例如將`.jpg`新增至URL。
* 建立URL的資料夾路徑以用於搜尋引擎最佳化(SEO)。

   請參閱[Dynamic Media經典Adobe如何支援SEO](/help/assets/dynamic-media/assets/s7_seo.pdf)。

* 新增中繼資料至URL，以利搜尋引擎最佳化(Search Engine Optimization)。

   請參閱[Dynamic Media經典Adobe如何支援SEO](/help/assets/dynamic-media/assets/s7_seo.pdf)。

* 設定內容配置以觸發下載。
* 簡化影像伺服範本URL以利個人化。 例如，將`rgb{XX,YY,ZZ}`轉換為RTF-ready `\redXX\greenYY\blueZZ`

* 請求某些要編碼的字元（例如`$`、`{`和`}`），以及某些要解碼的字元（例如要解碼至ImageServer）。 例如，Facebook在包含特殊字元的URL上無法正常運作。

   請參閱[從URL中移除特殊字元。](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html)

在Dynamic Media，使用XML系統來管理資產資訊的網站可將XML檔案上傳至Dynamic Media。 您可以指定其中一個檔案為預先處理規則集檔案，以供Dynamic Media資產使用。 該檔案重構標準URL協定格式，以滿足與Dynamic Media整合的系統的業務邏輯。 您可以指定XML檔案作為規則集定義檔案路徑。

>[!CAUTION]
>
>使用規則集時請謹慎；它們可防止Dynamic Media內容顯示在您的網站上。

有可用的範例規則集可協助您建立自己的規則集。
請參閱[規則集參考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html)。

如同建立所有規則集一樣，請使用XMLVALID等XML驗證程式，在上傳XML檔案之前，先確定其有效性。
另請參閱[疑難排解規則集](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)。

此外，請務必先在測試環境中測試規則集，而不會影響您的即時生產環境。
生產環境和測試環境通常需要不同的登入。

請參閱[AdobeDynamic Media經典案頭應用程式以取得登入資訊](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app)。

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

另請參閱[在規則集](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)中使用&#39;asset&#39;而非&#39;is&#39;影像。

**要部署XML規則集：**

1. 開啟[Dynamic Media經典案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   您的認證和登入詳細資訊是由布建時的Adobe提供。 如果您沒有此資訊，請聯絡技術支援。

1. 執行下列動作，上傳規則集檔案：

   * 在全域導覽列上，按一下&#x200B;**[!UICONTROL Upload]**。
   * 在&#x200B;**[!UICONTROL Upload]**&#x200B;頁面的左上角附近，按一下&#x200B;**[!UICONTROL Browse]**。
   * 在&#x200B;**[!UICONTROL 開啟]**&#x200B;對話方塊中，瀏覽至您的規則集檔案(XML)。
   * 選擇檔案，然後按一下&#x200B;**[!UICONTROL 開啟]**。
   * 在&#x200B;**[!UICONTROL Upload]**&#x200B;頁的右側，為規則集檔案選擇目標資料夾。
   * 在頁面底部附近，請確定已勾選「上傳後發佈」。
   * 在頁面的右下角，按一下「提交上傳」。****
   * 在全局導航欄上，按一下&#x200B;**[!UICONTROL Jobs]**&#x200B;以檢查上載作業的狀態。 當&#x200B;**[!UICONTROL Job]**&#x200B;頁面上的&#x200B;**[!UICONTROL Status]**&#x200B;欄顯示「上傳完成」時，請繼續下一步驟。

1. 在頁面頂部的導覽列上，按一下「設定>應用程式設定>發佈設定>影像伺服器」。****
1. 在「映 **[!UICONTROL 像伺服器發佈]** 」頁的「目錄管理」組下，找到「規則集定義檔案路徑」 **[!UICONTROL ，然後按一下]**********「選擇」。
1. 在「選 **[!UICONTROL 擇規則集定義檔案(XML)]** 」頁上，瀏覽到規則集檔案，然後在頁的右下角按一下「選 **[!UICONTROL 擇」]**。
1. 在「設定」頁面的右下角，按一下「關閉」。****
1. 執行影像伺服器發佈工作。

   規則集條件會套用至即時Dynamic Media影像伺服器的請求。

   如果您變更規則集檔案，在您重新上傳並重新發佈更新的規則集檔案時，會立即套用變更。

