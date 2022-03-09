---
title: 存取和管理記錄檔
description: 瞭解如何訪問和管理日誌以幫助您在as a Cloud Service中開AEM發過程。
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---


# 存取和管理記錄檔 {#manage-logs}

瞭解如何訪問和管理日誌以幫助您在as a Cloud Service中開AEM發過程。

您可以使用 **環境** 卡 **概述** 頁或「環境詳細資訊」頁。

## 正在下載日誌 {#download-logs}

按照以下步驟下載日誌。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **環境** 卡 **概述** 的子菜單。

1. 選擇 **下載日誌** 中。

   ![下載日誌菜單項](assets/download-logs1.png)

1. 在 **下載日誌** 對話框，選擇相應的 **服務** 下拉菜單中

   ![「下載日誌」對話框](assets/download-preview.png)

1. 選擇服務後，按一下要檢索的日誌旁邊的下載表徵圖。

您也可以從 **環境** 的子菜單。

![「環境」螢幕中的日誌](assets/download-logs.png)

## 通過API記錄 {#logs-through-api}

除了通過UI下載日誌外，日誌還可通過API和命令行介面獲得。

要下載特定環境的日誌檔案，該命令類似於以下命令。

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

也可以通過命令行介面跟蹤日誌。

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

為了獲得環境ID（本例中為1884）和可用的服務或日誌名稱選項，可以使用以下命令。

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

請參閱以下其他資源以瞭解有關Cloud Manager API和Adobe I/OCLI的詳細資訊：

* [Cloud Manager API文檔](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [Adobe I/OCLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)
