---
title: 了解 Cloud Manager 和快速建立網站工作流程
description: 了解 Cloud Manager 以及它與快速建立網站的新流程如何連結在一起。
exl-id: 5d264078-e552-48ca-8d82-294a646e6b1f
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: ht
source-wordcount: '1113'
ht-degree: 100%

---

# 了解 Cloud Manager 和快速建立網站工作流程 {#understand-cloud-manager}

{{traditional-aem}}

了解 Cloud Manager 以及它與快速建立網站的新流程如何連結在一起。

>[!TIP]
>
>如果您的角色專門負責前端開發，您可以跳至本歷程中的文章「[擷取 Git 存放庫存取資訊](retrieve-access.md)」。
>
>如果您是 AEM 管理員、Cloud Manager 管理員、同時負責前端開發和管理任務，或者只是想了解在 AEM 執行前端開發從開始到結束的流程，請繼續閱讀本文件並繼續這個歷程。

## 目標 {#objective}

本文件協助您了解 AEM 快速建立網站工具的工作原理，並概觀從開始到結束的流程。閱讀本文件後，您應該：

* 了解 AEM Sites 和 Cloud Manager 如何共同運作以促進前端開發
* 了解前端自訂步驟如何與 AEM 完全分離並且不需要瞭解 AEM 亦可操作。

本文件的重點在於先瞭解快速建立網站解決方案的這些基本部分，然後再繼續歷程的下一步，即開始設定。

雖然建議您逐步完成此歷程，但如果您已經了解 AEM Sites 和 Cloud Manager 如何共同運作並想直接開始設定，您可以[跳至歷程的下一步](create-site.md)。

## 負責角色 {#responsible-role}

歷程的這個部分同時適用於 AEM 管理員和 Cloud Manager 管理員。

## 要求和先決條件 {#requirements-prerequisites}

在開始使用快速建立網站工具來建立和自訂網站之前，您必須先滿足數個要求。

因為此歷程適用於前端開發人員、管理員以及所有角色的組合，因此這裡列出兩者的要求。

請務必了解，前端開發人員並不需要 AEM 存取權或其相關知識。

### 知識 {#knowledge}

| 知識 | 角色 |
|---|---|
| 了解前端開發的標準工具與流程 | 前端開發人員 |
| 有關如何在 AEM 中建立和管理網站的基本知識 | AEM 管理員 |
| Cloud Manager 基本知識 | Cloud Manager 管理員 |

前端開發人員並不需要關於 AEM 的知識。

### 工具 {#tools}

| 工具 | 角色 |
|---|---|
| 偏好的前端開發環境 | 前端開發人員 |
| npm | 前端開發人員 |
| webpack | 前端開發人員 |
| 存取 Cloud Manager | Cloud Manager 管理員 |
| 成為 Cloud Manager 中&#x200B;**業務負責人**&#x200B;角色的一員 | Cloud Manager 管理員 |
| 成為 Cloud Manager 的系統管理員 | Cloud Manager 管理員 |
| 存取 Admin Console | Cloud Manager 管理員 |
| 成為 Cloud Manager 中&#x200B;**部署管理員**&#x200B;角色的一員 | Cloud Manager 管理員 |
| 成為 Cloud Manager 中&#x200B;**部署管理員**&#x200B;角色的一員 | 前端開發人員 |

前端開發人員並不需要使用 AEM。

>[!TIP]
>
>如果您不熟悉 Cloud Manager 角色和角色管理，請參閱「[其他資源](#additional-resources)」區段中的「角色型權限」文件。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要元件，是使用平台的單一入口。

若要支援客戶進行企業開發設定，AEM as a Cloud Service 與 Cloud Manager 及其專門建置的 CI/CD 管道完全整合。快速建立網站工具擴展這些功能以支援前端開發的專用管道。

針對本歷程的目的而言，您無需完全了解 Cloud Manager。從較高的層面來看，Cloud Manager 由多個層次的結構所組成。

![Cloud Manager 結構](assets/cloud-manager-structure.png)

* **租用戶** - 每個客戶都佈建了一個租用戶。
* **方案** - 每個租用戶都有一個或多個方案，這些方案通常反映了客戶的授權解決方案。
* **環境** - 每個方案都有多種環境，例如用於即時內容的生產、一種用於測試、一種用於開發目的。
* **存放庫** - 環境有一個或多個 Git 存放庫，可用於維護應用程式和前端程式碼。
* **工具和工作流程** - 管道管理從存放庫到環境的方案碼部署。

範例通常有助於內容化此階層。

* WKND Travel and Adventure Enterprises 可能是專注於旅遊相關媒體的&#x200B;**租用戶**。
* WKND Travel and Adventure Enterprises 租用戶可能有兩個&#x200B;**方案**：一個用於 WKND Magazine 的 Sites 方案，和一個用於 WKND Media 的 Assets 方案。
* WKND Magazine 和 WKND Media 方案都將有開發、測試和製作&#x200B;**環境**。

## 快速建立網站前端開發流程 {#flow}

整體流程簡單且容易操作，即使您尚未具備 Cloud Manager 豐富經驗亦可操作。

1. AEM 管理員登入 AEM 環境，並使用網站範本建立新網站。
1. Cloud Manager 管理員在 Cloud Manager 中建立前端管道。此管道會協調將程式碼從 git 存放庫部署到 AEM 環境的過程。
1. AEM 管理員從方案的 AEM 執行個體中匯出網站主題並提供給前端開發人員。
1. Cloud Manager 管理員授予前端開發人員存取 AEM Git 存放庫的權限，以便在其中提交自訂內容。
1. 前端開發人員擷取存取權認證來存取 git 和管道。
1. 前端開發人員自訂主題，利用使用 Proxy 的網站上的實際內容進行測試，然後將變更提交至 Git 存放庫。
1. 前端開發人員執行管道將主題自訂內容部署到方案的生產環境。

![快速建立網站流程](assets/qsc-flow.png)

使用快速建立網站工具的主要優點是前端開發人員只需要負責實際的自訂內容。前端開發人員與 AEM 沒有任何互動，也不需要任何 AEM 知識。

{{add-cm-allowlist-frontend-pipeline}}

## 下一步 {#what-is-next}

現在您已完成 AEM 快速建立網站歷程的這個部分，您應該：

* 了解 AEM Sites 和 Cloud Manager 如何共同運作以促進前端開發
* 了解前端自訂步驟如何與 AEM 完全分離並且不需要瞭解 AEM 亦可操作。

以此知識為基礎並繼續您的 AEM 快速建立網站歷程，接著檢閱文件「[使用範本建立網站](create-site.md)」，您可以在此了解如何使用範本快速建立新的 AEM 網站。

## 其他資源 {#additional-resources}

雖然建議您檢閱文件「[自訂網站主題](create-site.md)」以繼續快速建立網站歷程的下一部分，但下列是一些其他選用資源，深入探究了本文件提到的一些概念，不過這些資源並非繼續該歷程的必要條件。

* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=zh-Hant) - 如果您想要 Cloud Manager 功能的更多詳細資訊，您可能想直接查閱深入的技術文件。
* [角色型權限](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html?lang=zh-Hant) - Cloud Manager 已預先設定角色並授予適當權限。有關這些角色以及如何管理它們的詳細資訊，請參閱本文件。
* [npm](https://www.npmjs.com) - 用於快速建立網站的 AEM 主題以 npm 為基礎。
* [webpack](https://webpack.js.org) - 用於快速建立網站的 AEM 主題以 webpack 為基礎。
