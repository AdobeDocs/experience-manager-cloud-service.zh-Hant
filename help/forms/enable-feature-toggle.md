---
title: 啟用功能切換以整合早期採用者和發行前功能
description: 功能切換是AEM中的一項功能，可讓管理員在執行階段環境中啟用新功能。
feature: Adaptive Forms, Foundation Components, Core Components
role: User, Developer
source-git-commit: cc4fccc51f487170bf6c14e4b302a8d5912c33a0
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# 在Adobe Experience Software Development Kit (AEM SDK)上啟用功能切換

AEM中的「功能切換」可讓管理員在執行階段啟用或停用功能，非常適合在不變更程式碼的情況下管理早期採用者和發行前功能。 它支援逐步轉出、A/B測試和快速停用不穩定的功能。

本文介紹如何在AEM本機SDK設定中啟用功能切換，該設定使用SDK和Dispatcher模擬AEM as a Cloud Service。 此設定可協助團隊在部署到雲端之前，先在類似生產的環境中進行測試。

## 為何要在AEM SDK設定中使用功能切換？

在AEM SDK設定中工作時，功能會切換以下協助：

* 安全地測試實驗功能。

* 分階段推出新元件。

* 跨多個環境維護單一程式碼基底。

* 減少部署和升級期間的風險。

## 先決條件

在AEM SDK設定中啟用功能切換之前，請確定以下事項：

* 使用者是`forms-users`群組的成員。

* 導覽至`http://<author-instance-url>:portnumber/system/console/bundles`，並檢查&#x200B;**(com.adobe.granite.toggle.impl.dev-1.1.2.jar)**&#x200B;套件組合是否存在。 若不存在，請[從連結](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/com.adobe.granite.toggle.impl.dev-1.1.2%20.jar)下載套件。

  ![功能切換](/help/forms/assets/aem-web-console-bundle.png)

### 啟用功能切換

請依照下列步驟，在AEM SDK例項中啟用功能切換：

1. 登入您的AEM Forms執行個體。

1. 導覽至 `http://author-instance-url:portnumber/system/console/configMgr`。

1. 在Configuration Manager中搜尋Adobe Granite動態切換提供者。

   ![功能切換](/help/forms/assets/aem-web-console-confi.png)

1. 按一下圖示✏️ 。
1. 在「已啟用切換」區段中，按一下「➕」 。
1. 新增功能的功能切換ID，如下圖所示。
   ![功能切換](/help/forms/assets/feature-toggle.png)

1. 按一下「儲存」

>[!NOTE]
>
> 您可在檔案中找到早期採用者功能的特定功能切換ID。


### 停用功能切換

若要針對已啟用切換功能的功能停用功能切換，請遵循下列步驟：

1. 登入您的AEM Forms執行個體。
1. 導覽至 `http://author-instance-url:portnumber/system/console/configMgr`。
1. 在Configuration Manager中搜尋Adobe Granite動態切換提供者。
1. 按一下圖示✏️。
1. 在[已停用的切換]區段中，按一下➕。
1. 為要停用的功能新增切換號碼。

   ![功能切換](/help/forms/assets/disable-toggle-feature.png)

### 技術考量

功能切換由執行階段管理，最適合開發或測試設定。 在AEM SDK設定中，請確定切換是由版本控制，並與CI/CD同步。 可能需要重新整理頁面或清除快取，變更才會反映。

>[!NOTE]
>
> 若要為生產環境啟用功能切換，請聯絡Adobe支援團隊。

