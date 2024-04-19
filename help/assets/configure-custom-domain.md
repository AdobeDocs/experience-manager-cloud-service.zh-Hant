---
title: 設定發佈層的自訂網域
description: 瞭解如何在Adobe Cloud Manager中設定發佈層的自訂網域。
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---


# 設定發佈層的自訂網域{#configure-custom-domain}

在Adobe Cloud Manager中，您可以新增自訂網域，讓您的網站脫穎而出。 雖然AEMas a Cloud Service隨附預設網域，但您可以視需求加以自訂。
<!-- For example, AEM sites can use `sites.custom_domain.com`, and the AEM publish domain can be accessed via `assets.custom_domain.com`. Additionally, getting an SSL certificate for assets.pmi.com with a SAN entry for `delivery.custom_domain.com` improves security and trustworthiness. -->

## 開始之前

* 您必須擁有多個SAN （主體替代名稱） TLS或SSL憑證。
* SSL憑證應該有針對相同網域內發佈層對應之憑證的不同SAN。
* 憑證原則必須符合擴展驗證(EV)或組織驗證(OV)，而不是網域驗證(DV)原則。


## 新增自訂網域

若要為發佈層級設定自訂網域，請執行以下步驟：

1. 前往 **[!UICONTROL AdobeCloud Manager]** > **[!UICONTROL 計畫總覽]** > **[!UICONTROL SSL憑證]**，並新增您的SSL憑證。
   ![影像](/help/assets/assets/ssl-certificate.png)
瞭解如何新增 [SSL憑證](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) AdobeCloud Manager中的。

1. 新增SSL憑證後，請新增自訂網域。 按一下 **[!UICONTROL 網域設定]** 並指定針對的自訂網域 **[!UICONTROL 發佈服務]** 選項。
   <br> 進一步瞭解 [自訂網域](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html?lang=en).

1. 在您的DNS記錄中新增與發佈網域相對應的2個CNAME記錄。
   <br> 由於DNS傳播延遲，DNS驗證可能需要幾個小時才能處理。

1. 記錄支援案例以協助設定自訂網域，確保將其導向傳送階層。

>[!NOTE]
>
> 請務必新增自訂網域，以至資產選擇器的IMS使用者端中允許的重新導向URL清單。<br>提供自訂網域字串，與個別Adobe團隊協調以執行此工作。
