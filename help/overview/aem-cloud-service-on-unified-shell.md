---
title: AEMas a Cloud Service於Unified Shell
description: AEMas a Cloud Service於Unified Shell
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
source-git-commit: 53e22737e62835872e47ac07530078c3d1dfcf31
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---

# AEMas a Cloud Service於Unified Shell {#aem-as-a-cloud-service-on-unified-shell}

>[!NOTE]
>此功能於2022年7月在發行前管道提供。
>
>這是2022年8月發行版本中全面推出的新功能的簡介。
>
>請參閱 [發行前管道檔案](/help/release-notes/prerelease.md#enable-prerelease) 以取得如何為環境啟用功能的資訊。

## 總覽 {#overview}

AEMas a Cloud Service（作者服務）與Unified Shell整合，以改善使用者體驗，並與所有其他Experience Cloud應用程式統一。 此整合的影響可在應用程式的頂端看到，如下所示。

![影像](/help/overview/assets/unifiedshell_header.png)

其優點如下：

* 跨所有Experience Cloud應用程式單一登入
* 在組織之間輕鬆切換或切換到不同的應用程式
* 改善產品說明
* 輕鬆的產品內意見回饋按鈕，可回報問題或與Adobe分享意見
* 存取全球產品公告和通知，以及AEMas a Cloud Service專屬通知

## 禁用統一殼層 {#disabling-unified-shell}

現成可用的AEMas a Cloud Service已啟用統一殼層。 但是，如果已自訂頂端標題，建議停用統一殼層，以避免自訂的任何問題。 要禁用統一殼，請執行以下步驟：

>[!NOTE]
>只有具有管理權限的帳戶才能停用統一殼層。

1. 前往 **工具 — Cloud Services**.

   管理員使用者會看到「統一殼層設定」卡，如下所示：

   ![影像](/help/overview/assets/unifiedshell2.png)

1. 按一下 **統一殼配置**. 然後，取消選取下列核取方塊以停用「統一殼層」：

   ![影像](/help/overview/assets/unifiedshell3.png)

## 變更為深色主題 {#changing-to-dark-theme}

若要變更為深色主題，請按一下您的設定檔圖示。 這會顯示快顯視窗，如下所示。 您可以使用切換按鈕，切換至「統一殼層」的深色主題。

>[!INFO]
>
>深色主題僅適用於「統一殼層」（頂端列）。

![影像](/help/overview/assets/unifiedshell4.png)

## 識別AEMas a Cloud Service環境 {#identify-aemaacs-environment}

AEMas a Cloud Service提供三種環境：生產、預備和開發。 請參閱 [環境類型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en) 以取得更多詳細資訊。 透過與Unified Shell的整合，使用者登入Author服務的環境類型會透過標籤顯示在頂端標題上，如下所示。

![影像](/help/overview/assets/unifiedshell_header_label.png)


## 存取AEM收件匣 {#accessing-the-aem-inbox}

按一下統一殼層中的鈴聲圖示，即可存取AEM收件匣。

>[!INFO]
>
> 鐘鈴圖示上指示的數字包含該IMS組織內所有解決方案的未讀通知，以及列在AEM收件匣中的工作。

![影像](/help/overview/assets/unifiedshell5.png)

按一下快顯視窗中的「收件匣」按鈕，前往您的AEM收件匣：

![影像](/help/overview/assets/unifiedshell6.png)
