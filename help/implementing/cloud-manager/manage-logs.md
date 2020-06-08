---
title: 管理記錄檔——雲端服務
description: 管理記錄檔——雲端服務
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 11%

---


# 存取和管理記錄檔 {#manage-logs}

用戶可以使用環境卡訪問選定環境的可用日誌檔案清單。  用戶可以訪問選定環境的可用日誌檔案清單。

這些檔案可透過UI從「概述」頁面 **下載** 。

![](assets/manage-logs1.png)

或者，「環 **境** 」頁：

![](assets/manage-logs2.png)

>[!Note]
>不論其開啟位置為何，都會出現相同的對話方塊，並允許下載個別記錄檔。

![](assets/manage-logs3.png)


## 透過API記錄檔 {#logs-thorugh-api}

除了透過UI下載記錄檔外，記錄檔也可透過API和命令列介面使用。

例如，要下載特定環境的日誌檔案，命令將是

```java
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

以下命令允許跟蹤日誌：

```java
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

為了獲得環境ID（在本例中為1884）和可用的服務或日誌名稱選項，您可以使用：

```java
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

>[!Note]
>雖 **然「記錄下載** 」將可透過UI和API使用，但 **「記錄追蹤** 」僅限API/CLI。

### 其他資源 {#resources}

請參閱下列其他資源，以進一步瞭解Cloud Manager API和Adobe I/O CLI:

* [Cloud Manager API檔案](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)