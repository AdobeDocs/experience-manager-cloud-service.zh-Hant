---
title: 移轉公用程式工具/AEM現代化工具，將基於基礎元件的最適化Forms轉換為基於核心元件的表單
description: 瞭解如何安裝並使用移轉公用程式/AEM現代化工具，將基於基礎元件的最適化Forms轉換為基於核心元件的表單。
Keywords: Migration Utility Tool, Convert Adaptive Forms based on Foundation Components to Core Component based forms, Convert Foundation forms to Core Components forms, Using Modernizer Tool to convert Foundation Components to Core Components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
exl-id: ee71a576-96a7-4c81-b3a3-1d678f010cba
feature: Adaptive Forms, Core Components
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 4%

---

# 簡介

<span class="preview">此功能可在早期採用者方案下使用。 您可以從您的官方電子郵件ID寫信到aem-forms-ea@adobe.com ，以加入率先採用者計畫並請求存取該功能。</span>

Forms轉換公用程式是[AEM現代化工具](https://opensource.adobe.com/aem-modernize-tools/)套裝的一部分，可協助您輕鬆地將使用舊版基礎元件建立的最適化Forms轉換為運用核心元件現代支援功能的表單。

## 什麼是AEM現代化工具？

[AEM Modernize Tools](https://opensource.adobe.com/aem-modernize-tools/)是指一組公用程式或軟體應用程式，這些應用程式旨在促進Adobe Experience Manager (AEM)專案的現代化或更新程式。 這些工具通常會協助將AEM中的舊元件或功能轉換為更新、更有效率且受支援的替代方案。 Forms轉換公用程式安裝在「AEM現代化工具」下，以將基於基礎元件的最適化Forms轉換為基於核心元件的表單。

Forms轉換公用程式會將以舊版基礎元件為基礎的最適化Forms轉換為以新版核心元件為基礎的表單。 此轉換流程可確保表單符合現代標準和功能，潛在地改善效能、相容性，以及AEM環境中的易維護性。

![AEM現代化工具](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
>建議您在本機AEM設定上安裝AEM現代化工具。 將以基礎元件為基礎的最適化Forms移轉至以核心元件為基礎的表單。 下載表單及其資產。 然後，將表單及其資產上傳到所需的環境。

## 使用AEM現代化工具時的注意事項 {#considerations}

* 成功轉換後，套用至表單的所有規則都會被移除。 規則不會自動移轉。 您應手動重新建立這些規則，並將其套用至轉換後的表單。
* 原始表單中使用的翻譯設定不會延續。 重新設定轉換表單的翻譯。
* 如果以Foundation元件建置的表單包含指令碼或自訂函式規則，您必須根據核心元件將這些指令碼或規則重寫為轉換後的表單。
* 核心元件尚未支援下列OOTB基礎元件，因此會以轉換後的形式刪除：

   * Adobe Sign 區塊
   * 圖表
   * 檔案附件清單
   * 註腳預留位置
   * 影像選擇
   * 下一個按鈕
   * 前一個按鈕
   * 草寫簽名
   * 摘要步驟
   * 工具列

## 使用AEM現代化工具的先決條件

* [設定AEM Forms的本機開發環境](/help/forms/setup-local-development-environment.md)。
* 安裝最新的Far，為AEM Cloud Service環境啟用最適化Forms核心元件。
* 將您的使用者新增至[!DNL forms-users]群組。 [!DNL forms-users]群組的成員具有建立最適化表單的許可權。
* 具有下列角色的使用者有權在AEM環境中安裝AEM現代化工具：

   * 開發人員角色
   * 管理員角色

如需表單特定使用者群組的詳細清單，請參閱[群組與許可權](forms-groups-privileges-tasks.md)。

## 安裝及設定AEM現代化工具

若要安裝和設定AEM現代化工具：

1. [安裝AEM現代化工具至您的本機AEM Forms環境](#install-aem-modernize-Tools)
1. [為您本機AEM Forms環境啟用AEM現代化工具](#enable-aem-modernize-Tools)

### 安裝AEM現代化工具至您的本機AEM Forms環境 {#install-aem-modernize-Tools}

執行以下步驟，將AEM現代化工具安裝至您的本機AEM Forms環境：

1. 開啟命令提示或終端機。
1. 啟動本機AEM作者服務。 例如，從執行以下程式碼，以啟動本機AEM Author例項：

   `java -jar aem-author-p4502.jar`

1. 在本機系統中複製[AEM現代化工具](https://github.com/adobe/forms-modernizer)存放庫。

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tool]
   ```

   成功執行命令後，您的電腦上會有AEM Modernize Tool存放庫的本機副本。

1. 導覽至本機系統中的`[AEM Modernize Tool Repository]`。
1. 執行以下命令：

   ```Shell
       mvn clean install 
   ```

![成功安裝映像](/help/forms/assets/aem-modernize-install-steps.png)

成功安裝後，AEM現代化工具將可供您的環境使用。

![啟用AEM移轉公用程式工具](/help/forms/assets/enable-aem-modernizer-tools.png)


### 為您本機AEM Forms環境啟用AEM現代化工具{#enable-aem-modernize-Tools}

若要為您的AEM環境啟用並使用AEM現代化工具，請務必對應將基礎元件移轉至核心元件的規則：

1. 登入您的作者執行個體。
1. 導覽至 `http://[host]:[port]/system/console/configMgr`
1. 尋找並編輯`AEM Modernize Tools - Component Rewrite Rule Service`。
1. 將`Component Rule Paths`新增為`/apps/forms-modernizer/rules`。
1. 按一下「**儲存**」以儲存變更。

![AEM現代化元件規則](/help/forms/assets/aem-modernize-tools-component-rule.png)

## 執行表單轉換公用程式，將基礎元件式表單轉換為核心元件式表單

1. 前往&#x200B;**[!UICONTROL 工具> AEM現代化工具> Forms轉換]**。

   ![選取AEM現代化工具](/help/forms/assets/aem-modernize-tools-select-form.png)

1. 選取&#x200B;**[!UICONTROL Forms轉換]**&#x200B;選項。

   ![選取Forms轉換選項](/help/forms/assets/aem-modernize-forms-conversion.png)

1. 按一下&#x200B;**建立**&#x200B;以建立新工作。

   ![AEM現代化工具建立工作](/help/forms/assets/aem-modernize-tools-create-job.png)

1. 指定&#x200B;**[!UICONTROL 工作名稱]**。
1. 在&#x200B;**[!UICONTROL 表單]**&#x200B;索引標籤中，您可以選取下列其中一個選項：

   * **無** ：如果您不想在開始表單轉換之前建立以Foundation元件為基礎的表單副本，請選取選項。
   * **還原** ：選取選項，將表單還原至開始表單轉換前的狀態。
   * **複製到Target**：選取選項，在開始表單轉換之前建立Foundation元件式表單的副本。

   在本例中，已選取&#x200B;**複製到目標**&#x200B;選項。 如果選取&#x200B;**複製到目標**&#x200B;選項，**[!UICONTROL Source路徑]**&#x200B;和&#x200B;**[!UICONTROL 目標路徑]**&#x200B;選項就會變成可見。

1. 在`source folder`Source路徑&#x200B;**[!UICONTROL 中指定]**&#x200B;名稱。
1. 在`target folder`目標路徑&#x200B;**[!UICONTROL 中指定]**&#x200B;名稱。
1. 選取&#x200B;**[!UICONTROL 「下一步」]**。
1. 按一下&#x200B;**[!UICONTROL 新增Forms]**。 `source folder`中的所有表單都會出現在畫面上。
1. 選取以基礎元件為基礎的最適化Forms ，以將它轉換為以核心元件為基礎的表單。 您也可以選取多個表單。

   ![AEM現代化工具選取表單](/help/forms/assets/aem-modernize-tools-select-form.png)

1. 按一下「**[!UICONTROL 選取]**」。
1. 按一下&#x200B;**[!UICONTROL 排程工作]**&#x200B;以開始轉換程式。
1. 從&#x200B;**[!UICONTROL 轉換頁面]**&#x200B;對話方塊按一下&#x200B;**[!UICONTROL 轉換]**。

   ![AEM現代化工具轉換頁面](/help/forms/assets/aem-modernize-tools-convert-form.png)

   處理序的狀態變更為`success`時。 導覽至`target folder`以檢視轉換後的表單。

   ![AEM現代化工具成功](/help/forms/assets/aem-modernize-tools-success.png)

1. 選取最適化表單，然後選取> **[!UICONTROL 屬性]**。 此時會開啟「表單屬性」頁面。

   ![AEM現代化工具目的地資料夾](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**以再次儲存轉換表單的內容。
   ![AEM現代化工具最適化表單屬性](/help/forms/assets/aem-modernize-tools-af-properties.png)

您現在可以看到，以Foundation Components為基礎的最適化表單已轉換為以核心元件為基礎的最適化表單。

## 最佳做法 {#best-practices}

* 確定您的Foundation元件式表單，僅使用具有同等可用[核心元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type)的元件。 若您使用沒有對等核心元件的基礎元件，則不會轉換基礎元件。 因此，它在編寫表單時無法正常運作
* 請確定將基礎元件轉換為核心元件的規則已格式化為XML。
