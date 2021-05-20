---
title: 環境布建 — 必要條件
description: 環境布建 — 必要條件
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---


# 已佈建的環境 {#environments-provisioning}

## 布建 {#provisioning}

Adobe會自動布建客戶購買的所有AEM雲端環境，並連結回其Cloud Manager中的計畫。 這些AEM雲端環境包含在每個Adobe Managed Services訂閱中，通常由至少一個生產環境、一個階段環境，以及選用的一或多個開發或測試環境組成。

## 歡迎電子郵件{#welcome-email}

完成環境布建程式後，指定的客戶管理員會收到歡迎電子郵件，確認他們已獲得Adobe Experience Cloud的存取權。 此電子郵件包含如何開始使用Experience Cloud服務和Cloud Manager自助服務入口網站的詳細資訊。 此外，電子郵件還包含重要資訊，例如支援資源、論壇或常見問題集的去向等。 在電子郵件中提供的資源清單中，您也會取得如何存取Cloud Manager或AEM雲端環境的詳細資訊。

## 後續步驟{#next-steps}

收到歡迎電子郵件後，您就可以使用您的AdobeIMS憑證，以管理員身分登入Cloud Manager。 登入後，您將可以確認您的AEM雲端生產及非生產環境可供使用，並成功執行。

部署程式碼時，Cloud Manager會使用這些AEM雲端環境，從Cloud Manager的Git存放庫開始、透過中繼環境，直到您的AEM生產環境，執行CI/CD管道。 當您準備好為Web屬性建立數位體驗時，您也可以直接從Cloud Manager存取AEM雲端環境。