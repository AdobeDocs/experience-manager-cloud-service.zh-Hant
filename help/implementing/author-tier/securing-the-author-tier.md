---
title: 保護作者層
description: 保護作者層
translation-type: tm+mt
source-git-commit: cd35b7b4dbdd434f367871ae5d6584b1ad1de341
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 保護作者層 {#securing-the-author-tier}

當以AEM為雲端服務建立新環境時，產生的作者層預設可從網際網路存取。

您可以進一步配置網路原則，以確保對作者層的存取安全。 此程式基於授權應授予您作者環境網路訪問權限的IP範圍。

為了落實這些規則，請將支援票證（從Adobe Admin Console）填入要求的資訊：
- 程式ID
- 環境ID
- 授權的IP位址範圍