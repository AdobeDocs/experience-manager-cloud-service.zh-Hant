---
title: 沙盒程式——雲端服務
description: 沙盒程式——雲端服務
translation-type: tm+mt
source-git-commit: 168b3d28a36e4ec5258b2d2f391af25c466be6c6
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---


# 沙盒程式 {#sandbox-programs}

## 簡介 {#introduction}

沙盒程式是AEM Cloud Service中提供的兩種程式類型之一，另一種是一般程式。

建立沙盒通常是為了提供訓練、執行示範、啟用或概念驗證(POC)的目的。 他們不是要載著現場交通的。

沙盒程式包括「網站」和「資產」，並自動填入Git分支，其中包含范常式式碼、開發環境和非生產管道。

請參閱了 [解方案和方案類型](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html) ，以進一步瞭解方案類型。

### 沙盒程式的屬性 {#attributes-sandbox}

「沙盒程式」具有下列屬性：

1. **方案建立：** 建立沙盒程式包括自動：
   * 使用范常式式碼和內容設定專案
   * 開發環境的創造
   * 建立非生產性管道以部署至開發環境（主分支部署至開發環境）

1. **解決方案：** 沙盒程式包括AEM Sites和Assets。

1. **AEM更新：** AEM更新可手動套用至沙盒程式中的環境，且不會自動推送。

1. **休眠：** 如果在某段時間內未偵測到任何活動，則沙盒程式中的環境會自動休眠。 休眠的環境可以手動解除休眠。

### 建立沙盒程式 {#creating-sandbox-program}

程式建立精靈可讓您建立沙盒程式。

若要瞭解如何建立沙盒程式，請參閱「 [建立沙盒程式」](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)。

### 建立沙盒環境 {#creating-sandbox-environments}

「沙盒程式」是在程式建立時以自動建立的方式提供開發環境。 依預設，開發環境包含作者和發佈層。

當使用者準備好設定生產管線時，可手動將生產階段環境集新增至沙盒程式。

要瞭解如何手動建立環境，請參閱添加環 [境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments) ，以瞭解詳細資訊。

### 刪除沙盒環境  {#deleting-sandbox-environments}

具備必要權限的使用者可以刪除開發或生產／階段環境或集。

要刪除環境，請參閱刪除 [環境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment) ，以瞭解詳細資訊。


## 冬眠和冬眠沙盒環境 {#hibernating-introduction}

如果在某段時間內未 *檢測到任何活動* ，沙盒程式環境將進入休眠模式。

>[!NOTE]
>Hibernation是沙盒程式環境獨有的。 常規程式環境不休眠。

### 冬眠 {#hibernation-introduction}

休眠可以自動或手動進行。 沙盒程式環境進入休眠模式可能需要幾分鐘 *的時間*。 資料會在冬眠期間保留。

冬眠分為：

* **自動** 「沙盒程式」環境在閒置8小時後會自動休眠，這表示作者和發佈服務都不會收到要求。

* **手動**: 作為用戶，您可以手動為沙盒程式環境休眠，但無需這樣做，因為休眠將在某段時間（8小時）不活動後自動發生。

#### 使用手動休眠 {#using-manual-hibernation}

您可以使用下列兩種不同方式，從「開發人員主控台」手動讓沙盒程式休眠：

* 環境細節螢幕
* 環境清單螢幕

請依照下列步驟，手動讓沙盒程式環境休眠：

1. 導覽至「開 **發人員主控台」**。
請參閱 [存取Developer Console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) ，瞭解如何從「環境」卡存取 **Developer Console****** 。

1. 按一下「休眠」，如下圖所示

   ![](assets/hibernate-1.png)
1. 按一下 **Hibernate** 以確認步驟。

   ![](assets/hibernate-2.png)

1. 當休眠成功時，您會在「開發人員控制台」畫面中看到您環境的休眠程式完 **整通知** 。

   ![](assets/hibernate-4.png)

#### 訪問休眠環境 {#accessing-hibernated-environment}

當針對休眠環境的作者或發佈層提出任何瀏覽器請求時，使用者會遇到一個描述該環境休眠狀態的登陸頁面，如下所示：

使用 **** Cloud Manager - Developer Role的使用者可以按一下「Developer Console」（開發人員主控台）按鈕，存取開發人員主控台並解除環境休眠。 有關設定角色的資訊，請參閱Cloud Manager檔案。

如果組織中的使用者無法按一下「開發人員主控台」按鈕以進入「開發人員主控台」，則可能需要給予他們「雲端管理員——開發人員角色」。


### 解除休眠 {#de-hibernation-introduction}

1. 導覽至「開 **發人員主控台」**。
請參閱 [存取Developer Console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) ，瞭解如何從「環境」卡存取 **Developer Console****** 。

   >[!IMPORTANT]
   >Admin Console的存取權由「管理控制台」中 **的「雲端管理員——開發人員角色** 」 **定義**。 具有開發人員角色權限的使用者可以解除沙盒程式環境的休眠。

1. 按一下「 **De-hibernate**（解除休眠）」，如下圖所示：

   ![](assets/de-hibernation-img1.png)

1. 按一下 **De Hibernate** （刪除休眠）確認步驟。

   ![](assets/de-hibernation-img2.png)

1. 您將會收到解除休眠程式已啟動的通知，並會隨進度更新。

   ![](assets/de-hibernation-img3.png)

1. 程式完成後，沙盒程式環境將再次激活。

   ![](assets/de-hibernation-img4.png)


## AEM沙盒環境更新 {#aem-updates-sandbox}


請參閱 [AEM版本更新](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates) ，以取得詳細資訊。

使用者可以手動將AEM更新套用至沙盒程式中的環境（請參閱下圖）。 當顯示的狀態為「可用更新」時，可 **以執行此操作**。

「環境卡」上的下拉式選單提供「更新」 **選項** 。 如果您從「環境」卡上按一下「詳細資訊」(Details **** ) **，也可從「管理」(** Manage **)按鈕使用此選項** 。

>[!NOTE]
>必 *須配置部署到所關注開發環境的非生產管道* ，以便啟動手動更新管道。

>[!NOTE]
>必 *須配置Production Pipeline* ，才能啟動對Production+Stage環境設定的手動更新管線。

>[!NOTE]
>手動更新至 *Production* 或 *Stage* 環境會自動更新其他環境。 Production+Stage環境集必須位於相同的AEM版本。





