---
title: Unified Shell 上的 AEM as a Cloud Service
description: 了解有關 Unified Shell 上的 AEM as a Cloud Service 的權益
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
feature: Release Information
role: Admin
source-git-commit: 55cf6a10c2cb4c62aa8f89fac7f9d1fb4c012d26
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 95%

---

# Unified Shell 上的 AEM as a Cloud Service {#aem-as-a-cloud-service-on-unified-shell}

## 概觀 {#overview}

AEM as a Cloud Service (編寫服務) 與 Unified Shell 整合，以改進使用者體驗，並將其與所有其他 Experience Cloud 應用程式統一。這種整合的影響可以在應用程式的頂端標頭中看到，如下所示。

![影像](/help/overview/assets/unifiedshell_header.png)

此優點包括：

* 跨所有 Experience Cloud 應用程式的單一登入
* 更輕鬆地在組織之間切換，或切換至不同的應用程式
* 改進產品說明
* 簡單的產品內意見反應按鈕，用於向 Adobe 提報問題或分享想法
* 除了 AEM as a Cloud Service 特定的通知，可存取全球產品公告和通知

## 停用 Unified Shell {#disabling-unified-shell}

立即可用，AEM as a Cloud Service 已啟用 Unified Shell。但是，如果已自訂頂端標頭，建議停用 Unified Shell 以避免自訂項目出現任何問題。若要停用 Unified Shell，請按照以下步驟操作：

>[!NOTE]
>Unified Shell 只能由具有管理員權限的帳戶停用。

1. 按一下「**工具 > 雲端服務**」。

   管理員使用者會看到 Unified Shell 設定卡，如下所示：

   ![影像](/help/overview/assets/unifiedshell2.png)

1. 按一下「**Unified Shell 設定**」。然後，取消選取下方顯示的核取方塊以停用 Unified Shell：

   ![影像](/help/overview/assets/unifiedshell3.png)

>[!NOTE]
>
>您也可以在專案程式碼中停用Unified Shell。 請參閱[AEM UI的結構 — Unified Shell](/help/implementing/developing/introduction/ui-structure.md#unified-shell)。

## 變更為深色主題 {#changing-to-dark-theme}

若要變更為深色主題，請按一下您的個人資料圖示。此動作會顯示快顯視窗，如下所示。您可以使用切換按鈕切換到 Unified Shell 的深色主題。

>[!INFO]
>
>深色主題僅適用於 Unified Shell (頂端列)。

![影像](/help/overview/assets/unifiedshell4.png)

## 識別 AEM as a Cloud Service 環境 {#identify-aemaacs-environment}

AEM as a Cloud Service 提供三種類型環境：生產、中繼和開發。如需更多詳細資訊，請參閱[環境類型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html)。與 Unified Shell 整合，使用者在編寫服務上登入的環境類型會透過標籤顯示在頂端標頭上，如下所示。

![影像](/help/overview/assets/unifiedshell_header_label.png)

## 存取 AEM 收件匣 {#accessing-the-aem-inbox}

AEM 收件匣可以透過按一下 Unified Shell 中的鈴鐺圖示來存取。

>[!INFO]
>
> 鈴鐺圖示上的數字包含該 IMS 組織內所有解決方案的未讀通知以及 AEM 收件匣中列出的任務。

![影像](/help/overview/assets/unifiedshell5.png)

按一下快顯視窗中的收件匣按鈕以前往 AEM 收件匣：

![影像](/help/overview/assets/unifiedshell6.png)

