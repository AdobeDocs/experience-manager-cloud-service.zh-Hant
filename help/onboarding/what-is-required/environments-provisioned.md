---
title: 環境資源調配 — 需要什麼
description: 環境資源調配 — 需要什麼
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---


# 已佈建的環境 {#environments-provisioning}

## 設定 {#provisioning}

客戶購AEM買的所有雲環境都將通過Adobe自動配置，並連結回他們在Cloud Manager中的程式。 這AEM些雲環境包括在每個Adobe托管服務訂閱中，通常由至少一個生產環境、一個階段環境以及可選的一個或多個開發或test環境組成。

## 歡迎電子郵件 {#welcome-email}

在完成環境配置過程後，指定的客戶管理員將收到一封歡迎電子郵件，並確認他們已獲准訪問Adobe Experience Cloud。 該電子郵件包含有關如何開始使用Experience Cloud服務和Cloud Manager自助服務門戶的詳細資訊。 此外，電子郵件還包含重要資訊，如支援資源、論壇或常見問題解答等。 在電子郵件中提供的資源清單中，您還將獲得有關如何訪問雲管理器或雲環境AEM的詳細資訊。

## 後續步驟 {#next-steps}

在收到歡迎電子郵件後，您可以使用Adobe IMS憑據以管理員身份登錄Cloud Manager。 登錄後，您將能夠驗證雲生產和AEM非生產環境是否可用，並且運行成功。

Cloud ManagerAEM將使用這些雲環境在部署代碼時執行CI/CD管道，從Cloud Manager的Git儲存庫開始，通過登台環境，直到生產AEM環境。 當您準備開始為Web屬性創AEM建數字型驗時，您還可以直接從Cloud Manager訪問雲環境。