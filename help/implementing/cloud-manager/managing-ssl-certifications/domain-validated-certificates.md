---
title: 網域驗證 (DV) 憑證
description: 瞭解如何在Cloud Manager中管理網域驗證(DV)憑證。
exl-id: 7f2c71b6-15c3-4919-9f51-a3e26d0d48d4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 7%

---

# 網域驗證 (DV) 憑證 {#domain-validated-certificates}

瞭解如何在Cloud Manager中管理網域驗證(DV)憑證。

>[!NOTE]
>
>此功能僅適用於[早期採用者方案。](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## 簡介 {#introduction}

Cloud Manager可讓您自助服務產生和管理網域已驗證(DV) SSL憑證。 這為您提供最快、最簡單且最具成本效益的解決方案，為您的線上業務建立安全的網站。

[生產和沙箱程式都可以使用網域驗證的憑證。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## 新增自訂網域 {#adding-domain}

若要新增網域驗證(DV)憑證，您必須先設定自訂網域。 程式與檔案[自訂網域名稱簡介中的詳細程式大致相同。](/help/implementing/cloud-manager/custom-domain-names/introduction.md)不過，此功能已稍作擴充。

1. 驗證網域時，您可以選擇將Adobe管理或自我管理的憑證用於網域。 選擇&#x200B;**AdobeManaged憑證**，以便稍後新增DV憑證。

   ![選擇Adobe管理](assets/verify-domain-dialog.png)

1. 若要使用Adobe管理的憑證，您必須依照&#x200B;**驗證網域**&#x200B;對話方塊中的說明，將CNAME記錄新增至您的DNS。

   ![新增CNAME專案](assets/verify-domain-dialog-adobe-managed.png)

1. 網域建立後，點選或按一下網域清單中的省略符號按鈕，然後選取&#x200B;**驗證**&#x200B;以驗證網域。

   ![驗證網域](assets/verify-domain.png)

## 新增DV憑證 {#adding}

在正確設定您的網域後，若要新增DV憑證，請點選或按一下「SSL憑證」視窗中的&#x200B;**新增SSL憑證**&#x200B;按鈕。

![正在新增DC憑證](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. 選取選項&#x200B;**受管理的Adobe(DV)**。
1. 在&#x200B;**選取網域**&#x200B;下拉式清單中指定網域名稱。
1. 點選或按一下&#x200B;**儲存**。

一旦成功新增，憑證在&#x200B;**SSL憑證**&#x200B;視窗中的名稱將會有黃色警告符號的擱置狀態。

![擱置中的DV憑證](assets/pending-dv-certificate.png)

成功發行憑證後，憑證在&#x200B;**SSL憑證**&#x200B;視窗中的名稱會有綠色勾號。

![已核發的DV憑證](assets/issued-dv-certificate.png)

如需有關新增SSL憑證和SSL憑證視窗的詳細資訊，請參閱檔案[新增SSL憑證。](add-ssl-certificate.md)

## 新增CDN設定 {#add-cdn}

必須完成此步驟才能使用Fastly CDN使用SSL設定網域。

請依照這些步驟，使用Cloud Manager新增CDN設定。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 選取「**CDN設定**」標籤，然後按一下或點選工具列中的「**新增**」。

1. 在&#x200B;**設定CDN**&#x200B;對話方塊中，提供必要資訊。

   * 選取&#x200B;**來源**。 這可以是：
      * Cloud Service環境
      * Edge Delivery Services網站
   * 選取您的CDN型別。
   * 選取網域。
   * 選取SSL憑證。
      * 僅適用於Adobe管理的CDN。

   ![設定CDN對話方塊](assets/configure-cdn-dialog.png)

>
>
>對於Adobe管理的CDN，使用DV憑證時，只允許具有ACME驗證的網站。
