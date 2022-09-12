---
title: 僅針對Adobe InDesign產生版位轉譯
description: 使用Experience Manager Assets工作流程和ImageMagick產生新資產和現有資產的FPO轉譯。
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: 7cc0bd5bbd51edb6f3bc2cfcccfa0a35a0d7a790
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 僅針對Adobe InDesign產生版位轉譯 {#fpo-renditions}

將大型資產從Experience Manager放入Adobe InDesign檔案時，創意專業人員必須等待一段長時間 [放置資產](https://helpx.adobe.com/indesign/using/placing-graphics.html). 同時，用戶被阻止使用InDesign。 這會中斷創意流程，並對使用者體驗造成負面影響。 Adobe可以暫時將小型格式副本放在InDesign文檔中以開頭。 如果需要最終輸出，例如針對列印和發佈工作流程，原始的全解析度資產會取代背景的暫時轉譯。 背景中的非同步更新可加快設計流程以提高生產力，並且不會阻礙創作流程。

Assets提供僅用於版位(FPO)的轉譯。 這些FPO轉譯的檔案大小很小，但外觀比例相同。 如果資產無法使用FPO轉譯，Adobe InDesign會改用原始資產。 此後援機制可確保創意工作流程持續進行，不會有任何中斷。

Experience Manageras a Cloud Service提供雲端原生資產處理功能，以產生FPO轉譯。 使用資產微服務產生轉譯。 您可以設定新上傳資產和Experience Manager中現有資產的轉譯產生。

以下是產生FPO轉譯的步驟：

1. [建立處理設定檔](#create-processing-profile).

1. 設定Experience Manager以使用此設定檔 [處理新資產](#generate-renditions-of-new-assets).
1. 使用設定檔來 [處理現有資產](#generate-renditions-of-existing-assets).

## 建立處理設定檔 {#create-processing-profile}

若要產生FPO轉譯，請建立 **[!UICONTROL 處理設定檔]**. 設定檔會使用雲端原生資產微服務來處理。 如需指示，請參閱 [建立資產微服務的處理設定檔](asset-microservices-configure-and-use.md).

選擇 **[!UICONTROL 建立FPO轉譯]** 生成FPO格式副本。 （可選）按一下 **[!UICONTROL 新增]** 將其他格式副本設定添加到同一配置檔案中。

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## 產生新資產的轉譯 {#generate-renditions-of-new-assets}

若要產生新資產的FPO轉譯，請套用 **[!UICONTROL 處理設定檔]** 到資料夾屬性中的資料夾。 在資料夾的「屬性」頁面中，按一下 **[!UICONTROL 資產處理]** 頁簽，選擇 **[!UICONTROL FPO配置檔案]** as a **[!UICONTROL 處理設定檔]**，並儲存變更。 上傳至資料夾的所有新資產都會使用此設定檔進行處理。

![add-fpo-rendition](assets/add-fpo-rendition.png)


## 產生現有資產的轉譯 {#generate-renditions-of-existing-assets}

若要產生轉譯，請選取資產並遵循下列步驟。

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## 查看FPO轉譯 {#view-fpo-renditions}

工作流程完成後，您可以檢查產生的FPO轉譯。 在Experience Manager Assets使用者介面中，按一下資產以開啟大型預覽。 開啟左側邊欄並選取 **[!UICONTROL 轉譯]**. 或者，使用鍵盤快速鍵 `Alt + 3` 預覽時顯示。

按一下 **[!UICONTROL FPO轉譯]** 以載入其預覽。 或者，您可以以滑鼠右鍵按一下轉譯，然後儲存至您的檔案系統。 在左側邊欄中檢查可用的轉譯。

![rendition_list](assets/list-renditions.png)
