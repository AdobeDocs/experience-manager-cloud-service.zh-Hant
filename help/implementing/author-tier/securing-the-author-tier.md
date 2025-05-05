---
title: 保護製作層
description: 瞭解如何設定網路原則，以保護對作者階層的存取。
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
feature: Configuring
role: Admin
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 31%

---

# 保護製作層 {#securing-the-author-tier}

使用AEM as a Cloud Service建立環境時，依預設可從網際網路存取產生的作者階層。 您可以進一步設定網路原則，以保護對作者階層的存取權。 如需詳細資訊，請參閱[套用IP允許清單](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=zh-Hant)。 此程序的基礎，是向應具備您作者環境存取權的 IP 範圍提供授權。

若要設定這些規則，請從[Adobe Admin Console](https://adminconsole.adobe.com/)提交支援票證並附上要求的資訊：

* 方案 ID
* 環境 ID
* 要授權的 IP 位址範圍

