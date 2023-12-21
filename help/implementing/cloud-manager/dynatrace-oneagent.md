---
title: Dynatrace OneAgent
description: 瞭解如何將Dynatrace的OneAgent與AEMas a Cloud Service搭配使用
source-git-commit: 9379e6a1ec323ff4f05e994e9265da1363b4a3df
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---


# Dynatrace OneAgent {#dynatrace-oneagent}

Adobe功能可讓您使用Dynatrace的OneAgent，在企業部署過程中監控AEMas a Cloud Service，找出任何潛在問題的原因，並視需要採取措施加以修正。 <!-- When GA, add: Read this [Dynatrace article](https://www.dynatrace.com/hub/detail/adobe-experience-manager/) about AEM monitoring to learn more. -->

## 將OneAgent與AEMas a Cloud Service整合 {#integrating-oneagent-with-aem-as-a-cloud-service}

Dynatrace OneAgent客戶可透過客戶支援票證要求連線，以監控其AEM使用情況。

連線要求所需的詳細資訊如下：

| **欄位** | **說明** |
|---|---|
| Dynatrace環境URL | 您的Dynatrace環境URL。<br><br>對於Dynatrace SaaS客戶，格式為 `https://<you-environment-id>.live.dynatrace.com`.<br><br>若為Dynatrace管理的客戶，格式為 `https://<your-managed-url>/e/<environmentId>` |
| Dynatrace環境ID | 您可以在環境URL中找到您的Dynatrace環境ID |
| Dynatrace環境權杖 | 您的OneAgent環境權杖。 請參閱Dynatrace檔案，瞭解如何建立此功能。<br><br>這應視為秘密，因此請使用適當的安全實務。 例如，密碼可在網站中加以保護，例如 **zerobin.net**，客戶支援票證可參考以及密碼。 |
| Dynatrace API存取權杖 | Dynatrace環境的API存取Token。 請參閱Dynatrace檔案，瞭解如何建立此功能。<br><br>這應視為秘密，因此請使用適當的安全實務。 例如，密碼可在網站中加以保護，例如 **zerobin.net**，客戶支援票證可參考以及密碼。<br><br>注意：只有Dynatrace Managed才需要此專案。 |
| Dynatrace ActiveGate連線埠 | OneAgent應連線至您的Dynatrace ActiveGate連線埠。<br><br>注意：只有Dynatrace Managed才需要此專案。 |
| AEM環境ID | Dynatrace要監控的AEM環境ID。 |


