---
title: 設定 Dynamic Media
description: 若要設定Dynamic Media，您必須設定Dynamic Media並管理影像和檢視器預設集。
mini-toc-levels: 3
contentOwner: Rick Brough
feature: Configuration,Viewer Presets,Image Presets,Dynamic Media
role: Admin,User
badgeSaas: label="AEM Assets" type="Positive" tooltip="適用於AEM Assets)。"
exl-id: 83b70b17-7ee3-41cb-be90-c92ca161660e
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 5%

---

# 設定 Dynamic Media {#setting-up-dynamic-media}

{{work-with-dynamic-media}}

[Dynamic Media](https://business.adobe.com/tw/products/experience-manager/assets/dynamic-media.html)可依需求提供豐富的視覺銷售和行銷資產，並自動針對網路、行動及社交網站的消費進行縮放，協助您管理資產。 Dynamic Media使用一組主要來源資產，透過其可擴充且效能最佳化的全域網路即時產生並傳送多種多樣的豐富內容。

<!--
 OBSOLETE UNTIL THE INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE

>[!NOTE]
>
>This documentation describes Dynamic Media capabilites, which are integrated directly into [!DNL Experience Manager]. If you are using Dynamic Media Classic (previously called Scene7) integrated into [!DNL Experience Manager], see [Dynamic Media Classic integration documentation](/help/sites-cloud/administering/integrating-scene7.md).
>
>See [Dual Use Scenario](/help/sites-cloud/administering/integrating-scene7.md#dual-use-scenario) for times when you may want to use [!DNL Experience Manager] integrated with Dynamic Media Classic along with Dynamic Media.

-->

如果您正在管理Dynamic Media，以下是您感興趣的主題：

* [設定 Dynamic Media](config-dm.md)
* [管理影像預設集](managing-image-presets.md)
* [管理檢視器預設集](managing-viewer-presets.md)
* [Dynamic Media 疑難排解](troubleshoot-dm.md)

另請參閱下列主題：

* [視訊編碼和視訊設定檔](video-profiles.md)
* [影像設定檔](image-profiles.md)

>[!NOTE]
>
>**如果您正在升級：**
>
>* Adobe [!DNL Experience Manager]啟動並執行後，您上傳的任何資產都會自動啟用Dynamic Media （除非系統管理員明確停用它）。 如果您在升級的[!DNL Experience Manager]執行個體上並且剛開始使用Dynamic Media，則可能必須重新處理您的資產，使其啟用Dynamic Media。 請參閱[重新處理資料夾](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets)中的資產。


## Dynamic Media憑證更新需要一次性DNS更新 {#dns-update-dynamic-media-certificate-renewals}

如果您的網域使用CAA （憑證授權單位） DNS記錄，您必須授權DigiCert允許繼續續約Dynamic Media主機名稱使用的TLS/SSL憑證。

在網域的根（頂端）新增下列CAA記錄：

```
<yourdomain> CAA 0 issue "digicert.com"
```

此為單次變更。

您可以使用您的DNS提供者工具或[CAA查詢公用程式](https://caatest.co.uk/)來驗證CAA記錄是否存在。

如果CAA記錄存在且DigiCert未獲授權，則憑證更新會在目前憑證過期時失敗，這可能會導致影像和視訊傳送的停機時間。 如果您的網域不存在CAA記錄，則不需要採取任何動作。
