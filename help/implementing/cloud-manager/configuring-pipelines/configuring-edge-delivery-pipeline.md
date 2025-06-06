---
title: 新增Edge Delivery管道
description: 瞭解如何新增Edge Delivery管道以建置計畫碼並將其部署到生產環境。
index: false
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="早期採用者" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: acb919474bfe4285c889b8646f731285f5b759ba
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 38%

---



# 新增Edge Delivery管道 {#configure-production-pipeline}

瞭解如何設定Edge Delivery管道以建置計畫碼並將其部署到生產環境。 生產管道會先將計畫碼部署到中繼環境。 在核准後，會將相同的程式碼部署到生產環境。

使用者必須擁有&#x200B;**[部署管理員](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能設定生產管道。

>[!NOTE]
>
>在發生以下情況之前，無法設定生產管道：
>
>* 程式隨即建立。
>* Git存放庫至少有一個分支。
>* 生產和中繼環境隨即建立。

開始部署程式碼之前，請從[!UICONTROL Cloud Manager]設定您的管道設定。

>[!NOTE]
>
>你可以在初始設定後[編輯管道設定](managing-pipelines.md)。

## 新增Edge Delivery管道 {#adding-production-pipeline}

設定好計畫並擁有至少一個使用 [!UICONTROL Cloud Manager] UI 的環境後，您就可以依照以下步驟著手新增非生產管道了。

>[!TIP]
>
>在設定前端管道之前，請參閱[AEM Quick Site建立歷程](/help/journey-sites/quick-site/overview.md)，以透過易於使用的AEM Quick Site建立工具取得端到端指南。 此歷程可幫助您簡化AEM網站的前端開發，讓您無需AEM後端知識即可快速自訂網站。

**若要新增新的Edge Delivery管道：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**方案總覽**&#x200B;頁面瀏覽至&#x200B;**管道**&#x200B;卡片，然後按一下&#x200B;**新增**&#x200B;以選取&#x200B;**新增生產管道**。

   ![專案管理員概觀中的管道卡](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **新增生產管道**&#x200B;對話框隨即顯示。提供&#x200B;**管道名稱**&#x200B;以識別您的管道以及以下選項。按一下&#x200B;**「繼續」**。

   **部署觸發計畫** - 在定義部署觸發計畫以啟動管道時，有以下選項。

   * **手動** — 手動啟動管道。
   * **在Git變更上** — 只要將認可新增到已設定的Git分支，就會啟動CI/CD管道。 使用此選項，您仍然可以在需要時手動啟動管道。

   **重要量度失敗行為** - 在管道設定或編輯期間，**部署管理員**&#x200B;可選擇對任何品質閘道中遭遇重要失敗時的管道行為進行定義。可使用的選項包括：

   * **每次都詢問** — 預設設定。 任何重要失敗都需要手動介入。
   * **立即失敗** - 如果選取，則每當重要失敗發生時，會取消管道。此程式基本上是模擬使用者手動拒絕每次失敗。
   * **立即繼續** — 如果選取，則每當重要失敗發生時，管道會自動繼續。 此程式基本上是模擬使用者手動核准每次失敗。

   ![生產管道設定](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 在&#x200B;**Source程式碼**&#x200B;索引標籤上，選取管道應處理的程式碼型別。

   * **[設定完整棧疊計畫碼管道](#full-stack-code)**
   * **[設定目標部署管道](#targeted-deployment)**

如需有關管道型別的詳細資訊，請參閱[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

完成建立生產流水線的步驟因所選原始計畫碼型別而異。 按照上面的連結跳到本文件的下一部分以便完成管道的設定。

