---
title: 產生Adobe InDesign的「僅供刊登」轉譯
description: 使用Experience Manager Assets工作流程和ImageMagick產生新資產和現有資產的FPO （僅供刊登）轉譯。
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 10%

---

# 產生Adobe InDesign的「僅供刊登」轉譯 {#fpo-renditions}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/assets/administer/configure-fpo-renditions) |
| AEM as a Cloud Service  | 本文章 |

將大型資產從Experience Manager置入Adobe InDesign檔案時，創意專業人士在[置入資產](https://helpx.adobe.com/tw/indesign/using/placing-graphics.html)後，必須等候相當長的時間。 同時，使用者被封鎖而無法使用InDesign。 這會中斷創意流程，並對使用者體驗產生負面影響。 Adobe一開始可讓您將小型轉譯暫時放入InDesign檔案。 當需要最終輸出時（例如對於列印和發佈工作流程），原始的完整解析度資產會取代背景中的暫時轉譯。 這種背景的非同步更新可加快設計流程以提高生產力，且不會影響創作流程。

Assets提供僅用於刊登(FPO)的轉譯。 這些FPO轉譯的檔案大小較小，但外觀比例相同。 如果資產無法使用FPO轉譯，Adobe InDesign會改用原始資產。 此遞補機制可確保創意工作流程無任何中斷地進行。

Experience Manager as a Cloud Service提供雲端原生資產處理功能，可產生FPO轉譯。 使用資產微服務來產生轉譯。 您可以設定轉譯產生新上傳的資產以及Experience Manager中存在的資產。

以下是產生FPO轉譯的步驟：

1. [建立處理設定檔](#create-processing-profile)。

1. 設定Experience Manager以使用此設定檔來[處理新資產](#generate-renditions-of-new-assets)。
1. 使用設定檔[處理現有資產](#generate-renditions-of-existing-assets)。

## 建立處理設定檔 {#create-processing-profile}

若要產生FPO轉譯，請建立&#x200B;**[!UICONTROL 處理設定檔]**。 設定檔使用雲端原生資產微服務進行處理。 如需指示，請參閱[建立資產微服務的處理設定檔](asset-microservices-configure-and-use.md)。

選取&#x200B;**[!UICONTROL 建立FPO轉譯]**&#x200B;以產生FPO轉譯。 或者，按一下[新增] **&#x200B;**&#x200B;將其他轉譯設定新增至相同的設定檔。

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## 產生新資產的轉譯 {#generate-renditions-of-new-assets}

若要產生新資產的FPO轉譯，請將&#x200B;**[!UICONTROL 處理設定檔]**&#x200B;套用至資料夾屬性中的資料夾。 在資料夾的[內容]頁面中，按一下[資產處理]索引標籤&#x200B;**，選取**&#x200B;[!UICONTROL &#x200B; FPO設定檔&#x200B;]&#x200B;**做為**&#x200B;[!UICONTROL &#x200B;處理設定檔&#x200B;]&#x200B;**，然後儲存變更。**&#x200B;所有上傳至資料夾的新資產都會使用此設定檔進行處理。

![add-fpo-rendition](assets/add-fpo-rendition.png)


## 產生現有資產的轉譯 {#generate-renditions-of-existing-assets}

若要產生轉譯，請選取資產，然後依照下列步驟進行。

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## 檢視FPO轉譯 {#view-fpo-renditions}

您可以在工作流程完成後檢查產生的FPO轉譯。 在Experience Manager Assets使用者介面中，按一下資產以開啟大型預覽。 開啟左側邊欄並選取&#x200B;**[!UICONTROL 轉譯]**。 或者，在預覽開啟時使用鍵盤快速鍵`Alt + 3`。

按一下&#x200B;**[!UICONTROL FPO轉譯]**&#x200B;以載入其預覽。 或者，您也可以用滑鼠右鍵按一下轉譯，並將其儲存至您的檔案系統。 檢查左側邊欄中是否有可用的轉譯。

![rendition_list](assets/list-renditions.png)

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)