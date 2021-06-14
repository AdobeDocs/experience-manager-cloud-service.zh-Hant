---
title: 保護作者階層
description: 保護作者階層
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: b2b319cf06bbad07add092059d3f093ce7336d4e
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 65%

---

# 保護作者階層 {#securing-the-author-tier}

以 AEM as a Cloud Service 建立新環境時，依預設可從網際網路存取產生的作者階層。您可以進一步設定網路原則，以保護對作者階層的存取權。如需詳細資訊，請參閱[套用IP允許清單](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=en) 。 此程序的基礎，是向應具備您作者環境存取權的 IP 範圍提供授權。

為了實施這些規則，請從[Adobe Admin Console](https://adminconsole.adobe.com/)中提交支援票證，並提供請求的資訊：

* 方案 ID
* 環境 ID
* 要授權的 IP 位址範圍

