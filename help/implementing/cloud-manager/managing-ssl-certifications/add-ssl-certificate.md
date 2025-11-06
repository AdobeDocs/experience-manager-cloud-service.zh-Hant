---
title: 新增 SSL 憑證
description: 瞭解如何使用Cloud Manager的自助服務工具新增您自己的SSL憑證或Adobe管理的DV （網域驗證）憑證。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 6%

---


# 新增SSL憑證 {#add-ssl-cert}

瞭解如何使用雲端新增您自己的SSL憑證或Adobe管理的DV （網域驗證）憑證

>[!NOTE]
>
>如果您使用客戶管理的(OV/EV) SSL憑證和客戶管理的CDN提供者，您可以略過新增SSL憑證，並在就緒後直接前往[新增網域對應](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。

布建憑證可能需要幾天時間。 因此，Adobe建議您在任何期限或上線日期之前及早布建自己的憑證，以避免延遲。

若要瞭解如何在Cloud Manager中更新及管理SSL憑證，請參閱[管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)。

如果您在新增或管理憑證時遇到問題，請參閱[疑難排解SSL憑證錯誤](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md)。


## 先決條件 {#prerequisites}

* 使用者必須是&#x200B;**企業所有者**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的成員才能新增SSL憑證。
* 如果您正在安裝自己的憑證，請參閱&#x200B;**管理SSL憑證簡介**&#x200B;中的[憑證需求](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)。

## 選擇要新增的SSL憑證 {#which-ssl-to-add}

在[在AEM Cloud Manager中新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)後，下一步將取決於您選擇使用Adobe受管理(DV) SSL憑證（建議）還是客戶受管理(OV/EV) SSL憑證。

* **若為Adobe Managed (DV) SSL憑證：**
   * 在新增自訂網域並在Cloud Manager中驗證後，網域驗證程式就會完成。
   * 現在，您必須[新增Adobe Managed (DV) SSL憑證](#add-adobe-managed-ssl-cert)。
新增至Cloud Manager後，請等待Adobe代表您核發及安裝DV SSL憑證。
   * 當憑證作用中時，您的自訂網域就可供使用。

* **對於客戶管理的(OV/EV) SSL憑證：**

   * 從憑證授權單位取得您的OV/EV SSL憑證。 如需詳細資訊，請檢閱客戶管理的OV/EV SSL憑證的[需求](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)。
   * 取得憑證後，[在Cloud Manager中新增您客戶管理的(OV/EV) SSL憑證的](#add-customer-managed-ssl-cert)詳細資料。
   * 新增後，自訂網域名稱將標籤為已驗證，並套用SSL憑證。

無論哪種情況，在驗證並安裝憑證後，自訂網域都可在您的環境中安全使用。 請務必定期[在Cloud Manager介面中檢查網域狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)，確認一切都如預期般運作。

另請參閱[SSL憑證簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)。

## 新增Adobe managed (DV) SSL憑證 {#add-adobe-managed-ssl-cert}

需要協助您選擇搭配您的網域使用Adobe管理的SSL憑證（建議）或客戶管理的SSL憑證嗎？ 請參閱[選擇要新增的SSL憑證](#which-ssl-to-add)

**若要新增Adobe Managed (DV) SSL憑證：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的方案。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。
1. 在頁面的左上角，按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以顯示側邊功能表。

1. 在&#x200B;**服務**&#x200B;標題下，按一下![鎖定已關閉圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL憑證**。

   ![正在新增SSL憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. 在[SSL憑證]頁面的右上角附近，按一下[新增SSL憑證]。**&#x200B;**

1. 在&#x200B;**新增SSL憑證**&#x200B;對話方塊中，根據[您的特定使用案例](#which-ssl-to-add)，選取&#x200B;**Adobe Managed (DV)**。

   ![新增DV憑證](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. 在&#x200B;**憑證名稱**&#x200B;欄位中，輸入您要與DV SSL憑證關聯的名稱。

1. 在&#x200B;**選取網域**&#x200B;下拉式清單中，選取一或多個要與DV SSL憑證關聯的已驗證網域。
   * 沒有要選取的網域？ 若是如此，您必須先[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)並確保它經過驗證，然後才能新增Adobe管理的SSL憑證。
   * 新增完自訂網域名稱后，請返回本主題並從步驟1重新開始。

1. 在對話框右下角，按一下「**儲存**」。

   成功發行SSL憑證後，**SSL憑證**&#x200B;表格中會顯示綠色的有效核取記號。

您現在已為專案新增有效的Adobe Managed DV SSL憑證。 此步驟通常是第一個設定自訂網域名稱的步驟。

您現在已準備好新增[CDN設定](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。

## 新增客戶管理的(OV/ED) SSL憑證 {#add-customer-managed-ssl-cert}

<!-- IF THIS TOPIC GET UPDATED, REMEMBER TO UPDATE THE STEPS ALSO IN THE "MANAGE SSL CERTIFICATES TOPIC TOO -->

需要協助您選擇搭配您的網域使用Adobe管理的SSL憑證（建議）或客戶管理的SSL憑證嗎？ 請參閱[選擇要新增的SSL憑證](#which-ssl-to-add)

>[!IMPORTANT]
>
>新增或更新SSL憑證時，請勿在憑證鏈結中包含新憑證。 如果包含此引數，上傳將無法成功完成。

**若要新增客戶管理的(OV/EV) SSL憑證：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的方案。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 在頁面的左上角，按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以顯示側邊功能表。

1. 在&#x200B;**服務**&#x200B;標題下，按一下![鎖定已關閉圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL憑證**。

   ![正在新增SSL憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. 在[SSL憑證]頁面的右上角附近，按一下[新增SSL憑證]。**&#x200B;**

1. 在&#x200B;**新增SSL憑證**&#x200B;對話方塊中，根據[您的特定使用案例](#which-ssl-to-add)，選取&#x200B;**客戶管理(OV/EV)**。

1. 在&#x200B;**憑證名稱**&#x200B;欄位中，輸入憑證的名稱。
此欄位僅供參考，可以是任何有助於您輕鬆參考SSL憑證的名稱。

1. 在&#x200B;**憑證**、**私密金鑰**&#x200B;和&#x200B;**憑證鏈**&#x200B;欄位中，複製OV或EV SSL憑證的必要值，並將其貼到對話方塊中各自的欄位中。

   將顯示值中偵測到的任何錯誤。 您必須先解決所有錯誤，才能儲存憑證。 請參閱[憑證錯誤](#certificate-errors)，深入了解疑難排解常見錯誤。

   ![新增SSL憑證對話方塊](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)|

1. 在對話框右下角，按一下「**儲存**」。

   >[!NOTE]
   >
   >* 如果您在&#x200B;**新增自訂網域名稱**&#x200B;時選取[客戶管理的憑證](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)，會在&#x200B;***之後驗證網域***&#x200B;新增並儲存客戶管理的(OV/EV) SSL憑證。 另請參閱[檢查自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to)的狀態。

   成功發行SSL憑證後，**SSL憑證**&#x200B;表格中會顯示綠色的驗證核取記號。

您現在已為專案新增有效的SSL憑證。 此步驟通常是第一個設定自訂網域名稱的步驟。

您現在已準備好新增[CDN設定](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。























<!--
## Add an SSL certificate {#add-ssl-cert}

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate program.
1. On the **[My Programs](/help/implementing/cloud-manager/navigation.md#my-programs)** console, select the program.
1. In the upper-left corner of the page, click ![Show menu icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) to reveal the side menu. 
1. Under the **Services** heading, click ![Lock closed icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL Certificates**. 

   ![Adding an SSL certificate](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Near the upper-right corner of the SSL Certificates page, click **Add SSL Certificate**.

1. In the **Add SSL certificate** dialog box, based on [your particular use case](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), do one of the following:

    | | Use case | Steps |
    | --- | --- | --- |
    | 1 | **Add an Adobe managed (DV) certificate** | **To add an Adobe managed (DV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Adobe managed (DV)**.<br>![Add a DV certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. In the **Certificate name** field, enter a name you want associated with the certificate.<br>c. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV SSL certificate.<br>No domains to select? If so, it means that you must first add a custom domain name and ensure it is verified before you can add an SSL certificate. See [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). When you are finished adding a custom domain name, return to this topic and begin at step 1 again.<br>d. Continue to step 7. |
    | 2 | **Add a customer managed (OV/EV) certificate** | **To add a customer managed (OV/EV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Customer managed (OV/EV)**.<br>b. In the **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your SSL certificate easily.<br>c. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.<br>![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate Errors](#certificate-errors) to learn more about troubleshooting common errors.<br>d. Continue to step 7. | 

1. In the lower-right corner of the dialog box, click **Save**.

    >[!NOTE]
    >
    >* If you selected **Adobe managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified with the added certificate when the custom domain is added. 
    >
    >* If you selected **Customer managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified ***after*** the customer managed (OV/EV) SSL certificate is added and saved. See also [Check the status of a custom domain name](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

    After the SSL certificate is successfully issued, it is displayed with a green verified check mark in the **SSL Certificates** table. 

    You now have added a working SSL certificate for your project. This step is often the first to set up a custom domain name. 
    

* To learn about updating and managing your SSL certificates in Cloud Manager, see [Manage SSL certificates](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

* If you are having issues adding or managing your certificates, see [Troubleshoot SSL certificate errors](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md). -->
