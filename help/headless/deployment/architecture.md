---
title: AEM無頭架構
description: 了解Adobe Experience Manager的高階架構，因為它與無頭部署相關。 了解AEM製作、預覽和發佈服務的角色，以及無頭應用程式的建議部署模式。
feature: Content Fragments,GraphQL API
exl-id: 5ba6921f-b06e-463d-b956-d1fb434090c9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# AEM無頭架構

一般的AEM環境由製作服務、發佈服務和選用的預覽服務組成。

* **作者服務** 是內部使用者建立、管理和預覽內容的位置。

* **發佈服務** 會視為「即時」環境，且通常是使用者與之互動的環境。 內容在Author服務上經過編輯和核准後，會分發至Publish服務。 AEM無頭式應用程式最常見的部署模式是讓生產版本的應用程式連線至AEM發佈服務。

* **預覽服務** 在功能上與 **發佈服務**. 不過，它僅供內部使用者使用。 這使得核准者在將內容變更上線給使用者之前，能先檢閱即將進行的內容變更，成為理想的系統。

* **Dispatcher** 是與AEM dispatcher模組增強的靜態Web伺服器。 它提供快取功能和另一層安全性。 此 **Dispatcher** 坐在 **發佈** 和 **預覽** 服務。

在AEMas a Cloud Service方案中，您可以有多個環境：開發、階段和生產。 每個環境都有各自的獨特 **作者**, **發佈**，和 **預覽** 服務。 您可以進一步了解管理 [這裡的環境](/help/implementing/cloud-manager/manage-environments.md)

## 作者發佈模型

AEM無頭式應用程式最常見的部署模式是讓生產版本的應用程式連線至AEM發佈服務。

![作者發佈架構](assets/autho-publish-architecture-diagram.png)

上圖描述了此通用部署模式。

1. A **內容作者** 使用AEM製作服務來建立、編輯和管理內容。
1. 此 **內容作者** 而其他內部使用者可以直接在Author服務上預覽內容。 可設定應用程式的預覽版本，以連線至製作服務。
1. 內容一經核准後，即可發佈至AEM Publish服務。
1. 此 **Dispatcher** 是前面的一層 **發佈** 可快取特定請求並提供安全層的服務。
1. 一般使用者與應用程式的生產版本互動。 生產應用程式會透過Dispatcher連線至發佈服務，並使用GraphQL API來請求和使用內容。

## 製作預覽發佈部署

無頭部署的另一個選項，是將 **AEM預覽** 服務。 透過此方法，內容可先發佈至 **預覽** 服務和無頭應用程式的預覽版本可以連接到它。 此方法的優點在於 **預覽** 可使用與 **發佈** 更輕鬆地模擬生產體驗。

![作者預覽與發佈架構](assets/author-preview-publish-architecture-diagram.png)

1. A **內容作者** 使用AEM製作服務來建立、編輯和管理內容。
1. 內容會先發佈至AEM預覽服務。
1. 可以設定應用程式的預覽版本，以連接到預覽服務。
1. 內容經過審核後，即可發佈至AEM Publish Service。
1. 一般使用者與應用程式的生產版本互動。 生產應用程式會透過Dispatcher連線至發佈服務，並使用GraphQL API來請求和使用內容。
