---
title: 新增SSL憑證
description: 瞭解如何使用Cloud Manager的自助服務工具新增您自己的SSL憑證或DV （網域驗證）憑證。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8e2fc0d4ee82e79d1a822a528b1a46acce3c192a
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 9%

---


# 新增SSL憑證 {#add-ssl-cert}

瞭解如何使用Cloud Manager的自助服務工具新增客戶管理的SSL憑證或Adobe產生和管理的DV （網域驗證）憑證。

另請參閱[疑難排解SSL憑證錯誤](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md)。

## 新增SSL憑證 {#adding-an-ssl-certificate}

提供憑證可能需要幾天時間。因此，Adobe建議在任何截止日期或上線日期之前提供憑證。

請務必在[管理SSL憑證簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)中檢閱&#x200B;**憑證需求**，以確定AEM as a Cloud Service支援您要新增的憑證。

使用者必須是&#x200B;**企業所有者**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的成員才能完成此工作。

>[!NOTE]
>
>不允許客戶上傳DV （網域驗證）憑證。

**若要新增SSL憑證：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從「**概觀**」頁面，瀏覽到「**環境**」畫面。

1. 從左側導覽面板的&#x200B;**服務**&#x200B;下，按一下&#x200B;**SSL憑證**。 如果您看不到下圖所示的左側導覽面板，您可能需要按一下左上角的漢堡圖示。

   ![正在新增SSL憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. 在頁面的右上角附近，按一下&#x200B;**新增SSL憑證**。

1. 在&#x200B;**新增SSL憑證**&#x200B;對話方塊中，根據[您的特定使用案例](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)，執行下列其中一項作業：

   | | 使用案例 | 步驟 |
   | --- | --- | --- |
   | 1 | **新增Adobe管理的憑證(DV)** | **若要新增Adobe管理的憑證(DV)：**<br> a。選取憑證型別&#x200B;**受管理的Adobe(DV)**。<br>![新增DV憑證](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b。在&#x200B;**憑證名稱**&#x200B;欄位中，輸入您要與憑證關聯的名稱。<br>c。在&#x200B;**選取網域**&#x200B;下拉式清單中，選取一或多個要與DV憑證關聯的網域。<br>沒有要選取的網域？ 若是如此，表示您必須新增自訂網域。 請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 新增完自訂網域名稱后，請返回本主題並從步驟1重新開始。<br>天。繼續步驟7。 |
   | 2 | **新增客戶管理的憑證(OV/EV)** | **若要新增客戶管理的憑證(OV/EV)：**<br> a。選取憑證型別&#x200B;**客戶管理的(OV/EV)**。<br>b。在&#x200B;**憑證名稱**&#x200B;欄位中，輸入憑證的名稱。 此欄位僅供參考，可以是任何有助於您輕鬆引用憑證的名稱。<br>c。在&#x200B;**憑證**、**私密金鑰**&#x200B;和&#x200B;**憑證鏈**&#x200B;欄位中，將必要的值貼到各自的欄位中。<br>![新增SSL憑證對話方塊](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>顯示值中偵測到的任何錯誤。 您必須先解決所有錯誤，才能儲存憑證。 請參閱[憑證錯誤](#certificate-errors)，深入了解疑難排解常見錯誤。<br>天。繼續步驟7。 |

<!--
    **Add an SSL certificate:**
    1. Select the certificate type **Customer managed (OV/EV)**.
    1. In **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your certificate easily.
    1. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.

        ![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)
  
    Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate errors](#certificate-errors) to learn more about troubleshooting common errors.

    **Add a DV certificate:**
    1. Select the certificate type **Adobe managed (DV)**.

        ![Adding a DC certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

    1. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV certificate.

        No domains to select? If so, it means that you must add a custom domain. See [Add a custom domain](#add-custom-domain). When you are finished, resume the steps from the beginning again. -->

1. 在對話框右下角，按一下「**儲存**」。

   成功發行憑證後，**SSL憑證**&#x200B;資料表中會顯示綠色核取記號。

您現在已為專案新增有效的SSL憑證。 此步驟通常是第一個設定自訂網域名稱的步驟。

* 若要設定自訂網域名稱，請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
* 若要瞭解如何在Cloud Manager中更新及管理SSL憑證，請參閱[管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)。

<!--
### Add a custom domain {#add-custom-domain}

Before you can add an Adobe generated and managed Domain Validated (DV) certificate, you must first add a custom domain. The process for doing so is nearly the same as detailed in [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) and [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). However, that functionality is now slightly expanded, as described below.

1. When adding a custom domain name, in the **Verify domain** dialog box, select an **Adobe managed certificate**.

    ![Choose Adobe-managed](assets/verify-domain-dialog.png)

1. In the **Verify domain** dialog box, add a CNAME verification record to your DNS.

    ![Add CNAME entry](assets/verify-domain-dialog-adobe-managed.png)

1. After the domain is created, click the ellipsis button in the list of domains and select **Verify** to verify the domain.

    ![Verify domain](assets/verify-domain.png) 

1. Resume the task [Add a DV certificate](#adding-an-ssl-certificate). -->


