---
title: 將 [!DNL AEM Assets] 與 [!DNL Figma]整合。
description: 瞭解如何將 [!DNL AEM Assets] 與 [!DNL Figma] 整合，以在您的 [!DNL Figma] 設計工作流程中存取和使用您組織的資產。
hide: false
role: User
exl-id: 530561ca-497b-4331-a014-72c561e1ca84
source-git-commit: 3603a98dfee62db49f3201c8d75aa8eee4909cc1
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# 將[!DNL AEM Assets]與[!DNL Figma]整合{#integrate-aem-assets-with-figma}

[!DNL AEM Assets]與[!DNL Figma]原生整合，可讓設計人員從[!DNL Figma]使用者介面直接存取[!DNL AEM Assets]中儲存的資產。 您可以將受管理的內容放在[!DNL Figma]畫布的[!DNL AEM Assets]中，然後將新內容或已編輯的內容儲存在[!DNL AEM Assets]存放庫中。

## 開始之前{#prerequisites-for-aem-assets-and-figma-integration}

* 最低必要的AEM發行版本為`19149`。

* 您必須具備有效的[!DNL AEM Assets]和[!DNL Figma]授權，才能將[!DNL AEM Assets]與[!DNL Figma]整合。

## 存取[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]{#access-aem-assets-connector}

執行以下步驟來存取[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]：

1. 在您的[!DNL Figma]首頁上，從畫布底部的工具列按一下&#x200B;**[!UICONTROL 動作]**，然後在對話方塊中可用的搜尋列中搜尋[!DNL Adobe Experience Manager (AEM) Assets Connector]。
1. 選取[!DNL Adobe Experience Manager (AEM) Assets Connector]以顯示[!DNL Adobe Experience Manager (AEM) Assets Connector]面板。 使用此面板[將 [!DNL AEM] 資產匯入 [!DNL Figma] 畫布](#import-aem-assets-into-figma-workflow)。
   ![動作](/help/assets/assets/actions-on-figma.png)
或者，也可以存取[!DNL Figma]社群上可用的[[!DNL Adobe Experience Manager (AEM) Assets Connector]](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector)，按一下&#x200B;**[!UICONTROL 開啟位置……]**，選取最近的檔案或建立新檔案，然後按一下&#x200B;**[!UICONTROL 執行]**&#x200B;以存取[!DNL Adobe Experience Manager (AEM) Assets Connector]面板。
   ![plugin-page-on-figma-community](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> 如果您在登入您的[!DNL AEM]環境後看到&#x200B;**[!UICONTROL 網路錯誤]**&#x200B;訊息，請[聯絡Adobe支援](https://helpx.adobe.com/contact.html)以取得協助。

## 將[!DNL AEM]資產匯入[!DNL Figma]畫布{#import-aem-assets-into-figma-workflow}

在您的[!DNL Figma]設計介面中[存取[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]面板](#access-aem-assets-connector)，並執行下列動作：

1. 在[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]面板中搜尋資產。 如需詳細資訊，請參閱[使用Asset Selector](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector)。

1. 將資產拖放至畫布或選取資產，然後按一下「選取&#x200B;**[!UICONTROL 」]**&#x200B;將資產放到畫布上。

1. 按一下資料夾路徑中的![三個點](/help/assets/assets/three-dots.svg)以顯示目前階層中的所有父資料夾和子資料夾。 選取要導覽至該位置的資料夾。
   ![三個點](/help/assets/assets/assets-folder-structure.png)

您的Figma設計就緒後，您可以[將資產匯出至AEM Assets存放庫](#export-figma-design-to-aem-assets-folder)。

## 將資產匯出至[!DNL AEM Assets]存放庫{#export-figma-design-to-aem-assets-folder}

在您的[!DNL Figma]設計介面中[存取[!UICONTROL Adobe Experience Manager (AEM) Assets Connector]面板](#access-aem-assets-connector)，並執行下列步驟將您的設計匯出至[!DNL AEM Assets]存放庫：

1. 導覽至您要儲存[!DNL Figma]設計的目的地資料夾。 如果您已經在資料夾內，請按一下資料夾路徑中的[更多]選項（![三個點](/help/assets/assets/three-dots.svg)），以選取不同的目的地資料夾。
1. 可選：將畫布上的資產分組，以將它們選取為單一單位，以便上傳至您的資料夾。
1. 按一下![檔案上傳](/help/assets/assets/upload-icon.svg) **[!UICONTROL 上傳]**&#x200B;以顯示&#x200B;**[!UICONTROL 上傳資產]**&#x200B;對話方塊。
1. 在對話方塊中，指定檔案名稱、選擇檔案格式、選取&#x200B;**[!UICONTROL 選取的專案]**&#x200B;或&#x200B;**[!UICONTROL 頁面]**，然後按一下&#x200B;**[!UICONTROL 上傳]**，將選取的資產或整個設計上傳至目的地資料夾。
   ![上傳figma設計](/help/assets/assets/upload-figma-design.png)

## 需要注意的重要事項{#Limitations-of-using-aem-assets-into-figma}

此整合目前有下列限制：

* 若要將[!DNL AEM]資產匯入Figma，支援的格式為&#x200B;**JPEG**、**PNG**。
* 將設計從[!DNL Figma]匯出至[!DNL AEM Assets]，支援的格式為&#x200B;**PNG**、**PDF**、**JPG**、**SVG**。
