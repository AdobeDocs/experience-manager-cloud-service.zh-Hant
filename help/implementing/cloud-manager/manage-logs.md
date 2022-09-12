---
title: 存取和管理記錄檔
description: 了解如何存取和管理記錄，以協助您在AEMas a Cloud Service中進行開發程式。
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---


# 存取和管理記錄檔 {#manage-logs}

了解如何存取和管理記錄，以協助您在AEMas a Cloud Service中進行開發程式。

您可以使用 **環境** 卡片 **概述** 頁面或環境詳細資料頁面。

## 正在下載日誌 {#download-logs}

請依照下列步驟下載記錄檔。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **環境** 卡片 **概述** 頁面。

1. 選擇 **下載記錄檔** 從刪節號菜單。

   ![下載日誌菜單項](assets/download-logs1.png)

1. 在 **下載記錄檔** 對話框，選擇相應的 **服務** 從下拉式功能表

   ![「下載日誌」對話框](assets/download-preview.png)

1. 選取服務後，按一下您要擷取之記錄旁的下載圖示。

您也可以從 **環境** 頁面。

![從「環境」畫面記錄](assets/download-logs.png)

## 透過API記錄 {#logs-through-api}

除了透過UI下載記錄檔外，記錄檔也可透過API和命令列介面使用。

若要下載特定環境的記錄檔，命令將類似下列。

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

您也可以透過命令列介面追蹤記錄。

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

為了獲得環境ID（本示例中為1884）和可用的服務或日誌名稱選項，可以使用以下命令。

```shell
$ aio cloudmanager:list-environments
Environment Id Name                     Type  Description                          
1884           FoundationInternal_dev   dev   Foundation Internal Dev environment  
1884           FoundationInternal_stage stage Foundation Internal STAGE environment
1884           FoundationInternal_prod  prod  Foundation Internal Prod environment
 
 
$ aio cloudmanager:list-available-log-options 1884
Environment Id Service    Name         
1884           author     aemerror     
1884           author     aemrequest   
1884           author     aemaccess    
1884           publish    aemerror     
1884           publish    aemrequest   
1884           publish    aemaccess    
1884           dispatcher httpderror   
1884           dispatcher aemdispatcher
1884           dispatcher httpdaccess
```

### 其他資源 {#resources}

請參考下列其他資源，以進一步了解Cloud Manager API和Adobe I/OCLI:

* [Cloud Manager API檔案](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [Adobe I/OCLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)
