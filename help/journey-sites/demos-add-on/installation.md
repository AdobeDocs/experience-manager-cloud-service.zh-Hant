---
title: 瞭解參考演示附加程式安裝
description: 瞭解Cloud Manager及其如何用於安裝載入項。
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# 瞭解參考演示附加程式安裝 {#understand-installation}

瞭解Cloud Manager及其如何用於安裝載入項。

>[!TIP]
>
>如果您已經對Cloud Manager有了經驗，或希望直接跳至配置和使用該載入項，則可以跳至 [建立程式和管線](create-program.md)
>
>如果您想瞭解Cloud Manager和Cloud Manager如何AEM協同工作以建立您的演示環境以及如何設定和使用您自己的演示環境，請繼續閱讀當前文檔。

## 目標 {#objective}

本文檔幫助您瞭解「參考演示」載入項的安裝過程如何工作，並演示不同部分如何協同工作。 閱讀完後，您應：

* 對雲管理器有基本的瞭解。
* 瞭解管道如何將內容和配置傳送AEM到。
* 查看模板如何通過只需按一下幾下即可預先填充演示內容來建立新站點。

本文檔重點介紹參考演示附AEM加內容的這些基本部分，然後進入開始安裝的下一步。

儘管建議您逐步完成此過程，但如果您已經對Cloud Manager有經驗，或希望直接跳至配置和使用外接程式，您可以跳至 [建立程式和管線](create-program.md)

## 責任角色 {#responsible-role}

此行程適用於屬於以下元件的系統管理員 **業務所有者** 在您的組織的雲管理器中的角色。

## 要求和先決條件 {#requirements-prerequisites}

瞭解並開始使用「參考演示」附加模組，要求最低。

### 知識 {#knowledge}

* 雲管理器的基本知識

### 工具 {#tools}

* 是 **業務所有者** 在雲管理器中為您的組織提供角色

## 瞭解雲管理器 {#cloud-manager}

Cloud Manager是as a Cloud Service的AEM重要元件，是平台的單一入口點。

Cloud Manager用於管理支援您的項目的雲資源AEM，包括所需的環境和工具。 為了完成此旅程，不需要完全瞭解雲管理器。 但是，您需要熟悉一些基本概念。

>[!TIP]
>
>如果您想深入瞭解雲管理器，請參閱 [其他資源](#additional-resources) 的子菜單。

### 計劃 {#programs}

登錄雲管理器時，您可以訪問一個或多個 **方案**。 程式可以用多種不同的方式定義，但最容易將其視為與與一個品牌標識相關聯的站點和體驗相關聯。

如果您登錄Cloud Manager，表示 **WKND旅行和冒險企業**，您可以建立 **WKND夜生活** 和 **WKND後院項目** 的子菜單。 這兩個程式都具有管AEM理其關聯站點的環境。

### 沙箱 {#sandboxes}

程式可以是生產程式或沙盒程式。

* **生產程式** 建立時，它最終允許在您的程式準備就緒時進行即時通信。
* **沙盒程式** 為培訓、運行演示、支援、POC等建立 而且不適合現場交通。

要安裝「參考演AEM示」載入項，您需要建立新的沙盒程式。

>[!NOTE]
>
>「參AEM考演示載入項」僅在沙盒程式中可用。

## 安裝和使用流 {#installation-flow}

現在您瞭解了Cloud Manager的一些基本概念，因此安AEM裝參考演示載入項在概念上非常簡單。

1. 登錄到雲管理器。
1. 建立新沙盒程AEM序，將參AEM考演示載入項激活為程式的選項。
1. 演示內容和配置將部署到程式。 演示內容包含：
   * 用於使用的功能建立AEM各種站點的站AEM點模板，預填充了最佳實踐示例。
   * 用於管理演示內容的配置工具。
1. 登錄AEM到新沙盒程式，使用快速站點建立工具並基於模板建立演示站點。
1. 使用配置工具管理這些演示站點和模板，包括在不再需要時刪除它們。

## 站AEM點模板 {#site-templates}

站AEM點模板是包含站點預定義內容和結構的包。 站點模板可以自定義以滿足特定項目的需要，AEM這樣管理員在建立新站點時，就可以從應用於其業務案例的模板中進行選擇。

參考演AEM示附件包括多個模板，以滿足各種測試和演示需要。 建立程式並部署管道以安裝載入項後，您可以基於AEM許多演示模板登錄並建立站點

## 下一步是什麼 {#what-is-next}

現在，您已完成「參考演示附AEM加程式」的這一部分，您應：

* 對雲管理器有基本的瞭解。
* 瞭解管道如何將內容和配置傳送AEM到。
* 查看模板如何通過只需按一下幾下即可預先填充演示內容來建立新站點。

在此知識基礎上構建並繼AEM續快速建立網站的過程，方法是下次查看文檔 [建立程式和管道，](create-program.md) 您將在其中學習如何設定新程式和管道以部署載入項。

## 其他資源 {#additional-resources}

建議您通過審閱文檔進入快速站點建立過程的下一部分 [建立程式和管道，](create-program.md) 下面是一些附加的可選資源，這些資源對本文檔中提到的一些概念進行了更深入的瞭解，但不需要繼續旅行。

* [瞭解程式和程式類型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html)  — 從此處開始瞭解即時和沙盒程式之間的差異。
* [站點模板](/help/sites-cloud/administering/site-creation/site-templates.md)  — 如果您想瞭解有關站點模板的結構以及它們如何用於建立站點的詳細資訊，請參閱本文檔。
* [Cloud Manager文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html)  — 如果您想更詳細地瞭解Cloud Manager的功能，則可能需要直接查閱深入的技術文檔。
