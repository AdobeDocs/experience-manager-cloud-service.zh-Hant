---
title: 保護作者階層
description: 保護作者階層
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 35%

---

# 保護作者階層 {#securing-the-author-tier}

使用AEMas a Cloud Service建立環境時，預設可從網際網路存取產生的作者階層。 您可以進一步設定網路原則，以保護對作者階層的存取。 另請參閱 [套用IP允許清單](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=en) 以取得更多詳細資料。 此程序的基礎，是向應具備您作者環境存取權的 IP 範圍提供授權。

若要設定這些規則，請由 [Adobe Admin Console](https://adminconsole.adobe.com/) 包含要求的資訊：

* 方案 ID
* 環境 ID
* 要授權的 IP 位址範圍

