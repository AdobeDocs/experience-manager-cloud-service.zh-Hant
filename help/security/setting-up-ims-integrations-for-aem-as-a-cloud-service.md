---
title: 為AEMas a Cloud Service設定IMS整合
description: 瞭解如何為AEMas a Cloud Service設定IMS整合
source-git-commit: e6749b9a5e97634a4706db5656b1e11dba4442c9
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---


# 為AEMas a Cloud Service設定IMS整合 {#setting-up-ims-integrations-for-aemaacs}

Adobe Experience Manager (AEM) as a Cloud Service可與許多其他Adobe解決方案整合。 例如，Adobe Target、Adobe Analytics和其他。

這些整合使用IMS整合，並以S2S OAuth設定。

* 建立後：

   * [開發人員控制檯中的認證](#credentials-in-the-developer-console)

* 然後，您可以：

   * 建立（新） [OAuth設定](#creating-oauth-configuration)

   * [將現有JWT設定移轉至OAuth設定](#migrating-existing-JWT-configuration-to-oauth)

>[!CAUTION]
>
>之前，設定是使用 [Adobe Developer Console中現在會淘汰的JWT憑證](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md).
>
>此類設定無法再建立或更新，但可移轉至OAuth設定。

## 開發人員控制檯中的認證 {#credentials-in-the-developer-console}

第一步，您需要在Adobe Developer主控台中設定OAuth認證。

如需如何執行此動作的詳細資訊，請參閱開發人員控制檯檔案，視您的需求而定：

* 概觀：

   * [伺服器對伺服器驗證](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

* 建立新的OAuth認證：

   * [OAuth伺服器對伺服器認證實作指南](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)

* 將現有JWT認證移轉至OAuth認證：

   * [從服務帳戶(JWT)認證移轉至OAuth伺服器對伺服器認證](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)

例如：

![開發人員控制檯中的OAuth認證](assets/ims-configuration-developer-console.png)

## 建立OAuth設定 {#creating-oauth-configuration}

若要使用OAuth建立新的Adobe IMS整合：

1. 在AEM中導覽至 **工具**， **安全性**， **Adobe IMS整合**.

1. 選取「**建立**」。

1. 根據的詳細資料完成設定 [開發人員主控台](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). 例如：

   ![建立OAuth設定](assets/ims-create-oauth-configuration.png)

1. **儲存** 您的變更。

## 將現有JWT設定移轉至OAuth設定 {#migrating-existing-JWT-configuration-to-oauth}

若要根據JWT憑證移轉現有的Adobe IMS整合：

>[!NOTE]
>
>此範例顯示Launch IMS設定。

1. 在AEM中導覽至 **工具**， **安全性**， **Adobe IMS整合**.

1. 選取需要移轉的JWT設定。 JWT設定會標示警告 **JWT認證（已棄用）**.

1. 選取 **屬性**：

   ![選取JWT設定](assets/ims-migrate-jwt-select-configuration.png)

1. 設定將以唯讀方式開啟：

   ![設定屬性 — 唯讀](assets/ims-migrate-jwt-properties-read-only.png)

1. 選取 **OAuth** 從 **驗證型別** 下拉式清單：

   ![選取驗證型別](assets/ims-migrate-jwt-authentication-type.png)

1. 可用的屬性將會更新。 使用開發人員控制檯中的詳細資訊完成這些作業：

   ![完成OAuth詳細資料](assets/ims-migrate-jwt-complete-oauth-details.png)

1. 使用 **儲存並關閉** 以持續儲存您的更新。
當您返回主控台時， **JWT認證（已棄用）** 警告將會消失。