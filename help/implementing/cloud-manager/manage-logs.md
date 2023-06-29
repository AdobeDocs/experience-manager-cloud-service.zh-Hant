---
title: 存取和管理記錄檔
description: 了解如何存取和管理記錄檔以協助進行 AEM as a Cloud Service 中的開發流程。
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 70%

---


# 存取和管理記錄檔 {#manage-logs}

了解如何存取和管理記錄檔以協助進行 AEM as a Cloud Service 中的開發流程。

您可以從&#x200B;**總覽**&#x200B;頁面或環境詳細資訊頁面使用&#x200B;**環境**&#x200B;卡，存取所選環境的可用記錄檔清單。

## 正在下載記錄檔 {#download-logs}

若要下載記錄檔，請執行下列動作。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 從&#x200B;**總覽**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;卡。

1. 從省略符號選單，選取&#x200B;**「下載記錄檔」**。

   ![下載記錄檔專案](assets/download-logs1.png)

1. 在&#x200B;**下載記錄**&#x200B;對話框，從下拉式選單中選擇合適的&#x200B;**服務**

   ![下載記錄檔對話框](assets/download-preview.png)

1. 選擇服務後，按一下要擷取記錄旁邊的下載圖示。

您也可以從&#x200B;**環境**&#x200B;頁面存取記錄檔。

![環境畫面的記錄檔](assets/download-logs.png)

## 透過 API 的記錄檔 {#logs-through-api}

除了透過UI下載記錄外，還可以透過API和命令列介面取得記錄。

若要下載特定環境的記錄文件，該命令會類似於以下內容。

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

此外，您也可以透過命令列介面追蹤記錄。

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

若要取得環境ID （在此範例中為1884）和可用的服務或記錄名稱選項，您可以使用以下命令。

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

請參閱下列其他資源，深入瞭解Cloud Manager API和Adobe I/OCLI：

* [Cloud Manager API 文件](https://developer.adobe.com/experience-cloud/cloud-manager/)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)
