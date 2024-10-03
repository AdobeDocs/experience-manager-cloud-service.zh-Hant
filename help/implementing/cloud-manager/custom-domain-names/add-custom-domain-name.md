---
title: 新增自訂網域名稱
description: 瞭解如何使用Cloud Manager中的網域設定來新增自訂網域名稱。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ff8c7fb21b4d8bcf395d28c194a7351281eef45b
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 17%

---


# 新增自訂網域名稱 {#adding-cdn}

瞭解如何使用Cloud Manager中的&#x200B;**網域設定**&#x200B;來新增自訂網域名稱。

## 要求 {#requirements}

在Cloud Manager中新增自訂網域名稱之前，請先滿足這些要求。

* 在新增自訂網域名稱之前，您必須先為要新增的網域新增網域SSL憑證，如檔案[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)中所述。
* 您必須擁有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色，才能在Cloud Manager中新增自訂網域名稱。
* 使用Fastly或其他CDN （內容傳遞網路）。

>[!IMPORTANT]
>
>即使您使用非AdobeCDN，仍需要將網域新增至Cloud Manager。

## 新增自訂網域名稱的位置 {#where-to-add-cdn}

您可以在Cloud Manager中從以下兩個位置新增自訂網域名稱：

* [網域設定頁面](#adding-cdn-settings)
* [環境頁面](#adding-cdn-environments)

新增自訂網域名稱時，會使用最明確的有效憑證提供網域。 如果多個憑證具有相同的網域，則選擇最近更新的憑證。 Adobe建議您管理憑證，以免網域重疊。

本檔案中描述的任一方法的步驟均以Fastly為基礎。 如果您使用不同的CDN （內容傳遞網路），請使用您選擇要使用的CDN來設定網域。

## 新增自訂網域名稱 {#adding-cdn-settings}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 在側邊功能表的&#x200B;**服務**&#x200B;底下，選取![設定圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) **網域設定**。

   ![域設定窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 在&#x200B;**網域設定**&#x200B;頁面的右上角附近，按一下&#x200B;**新增網域**。

1. 在&#x200B;**新增網域**&#x200B;對話方塊的&#x200B;**網域名稱**欄位中，輸入您正在使用的自訂網域名稱。
不包括`http://`,`https://`, 或輸入您的域時的空格。

1. 按一下&#x200B;**建立**。

1. 在&#x200B;**驗證網域**&#x200B;對話方塊中，在&#x200B;**您打算搭配此網域使用哪種憑證型別？**&#x200B;下拉式清單，選取下列其中一個選項：

   | 憑證型別選項 | 說明 |
   | --- | --- |
   | Adobe 管理的憑證 | 如果您要使用DV （網域驗證）憑證，請選取此憑證型別。 此選項適用於大多數的情況，可提供基本網域驗證。 Adobe會自動管理和更新憑證。 |
   | 客戶管理的憑證 | 如果您要使用EV/OV憑證，請選取此憑證型別。 此選項提供EV （延伸驗證）或OV （組織驗證）的增強式安全性。 若需要更嚴格的驗證、更高的信任層級或自訂的憑證控制，請使用。 |

1. 在&#x200B;**驗證網域**&#x200B;對話方塊中，根據您選取的憑證型別，執行下列其中一項作業：

   | 如果您選取憑證型別 | 說明 |
   | --- | ---  |
   | Adobe 管理的憑證 | 請先完成[Adobe受管理憑證步驟](#adobe-managed-cert-steps)，再繼續步驟9。 |
   | 客戶管理的憑證 | 請先完成[客戶管理的憑證步驟](#customer-managed-cert-steps)，再繼續步驟9。 |

1. 按一下&#x200B;**驗證**。

1. 您現在已準備好[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。

   >[!NOTE]
   >
   >如果您使用客戶管理的SSL憑證和客戶管理的CDN提供者，您可以略過新增SSL憑證，並在準備就緒後直接移至[新增CDN設定](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。


### Adobe受管理憑證步驟 {#adobe-managed-cert-steps}

如果您選取憑證型別&#x200B;*Adobe受管理憑證*，請在&#x200B;**驗證網域**&#x200B;對話方塊中完成下列步驟。

![AdobeManaged憑證步驟](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

若要驗證使用中的網域，您必須新增及驗證CNAME。

`CNAME`或記錄一旦布建，就會將網域的所有網際網路流量路由到它指向的任何地方。 如果未佈建該位置來處理流量，則會發生中斷。如果未經測試，內容可能會存在錯誤。這就是為什麼這個步驟總是在完成測試且準備好上線之後才完成。

若要設定這些設定，請確定是否必須設定`CNAME`或Apex記錄以將您的自訂網域名稱指向Cloud Manager網域名稱。 本檔案的下列章節可協助您判斷適合您DNS設定的記錄型別。

>[!NOTE]
>
>對於Adobe管理的CDN，使用DV （網域驗證）憑證時，只允許具有ACME驗證的網站。

#### 要求 {#adobe-managed-cert-dv-requirements}

在設定您的DNS記錄之前，請先滿足這些要求。

* 如果您還不知道您的網域主機或註冊商，請確定它。
* 能夠編輯組織網域的DNS記錄，或聯絡可以編輯的適當人員。
* 您必須已驗證您設定的自訂網域名稱，如檔案[檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)中所述。

#### CNAME記錄 {#adobe-managed-cert-cname-record}

正式名稱或 CNAME 記錄是一種將別名對應到真實或正式網域名稱的 DNS 記錄。CNAME 記錄通常用於將子網域 (例如 `www.example.com`) 對應到託管該子網域內容的網域。

登入您的DNS服務提供者並建立`CNAME`記錄，將您的自訂網域名稱指向目標，如下表所示。

| CNAME | 自訂網域名稱指向目標 |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### APEX記錄 {#adobe-managed-cert-apex-record}

Apex 網域是不包含子網域的自訂網域，例如`example.com`。Apex網域已透過您的DNS提供者設定`A`、`ALIAS`或`ANAME`記錄。 Apex 網域必須指向特定的 IP 位址。

透過您的網域提供者將下列`A`記錄新增到您網域的DNS設定中。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

>[!TIP]
>
>可在管理DNS伺服器上設定&#x200B;*CNAME*&#x200B;或&#x200B;*A記錄*，以節省您的時間。


### 客戶管理的憑證步驟 {#customer-managed-cert-steps}

如果您選取憑證型別&#x200B;*客戶管理的憑證*，請完成下列步驟。

1. 在&#x200B;**驗證網域**&#x200B;對話方塊中，上傳涵蓋選取網域的新EV/OV憑證。

   ![驗證客戶管理的EV/OV憑證的網域](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png)

1. 按一下&#x200B;**「確定」**。

   上傳有效的EV/OV憑證後，**網域設定**&#x200B;表格中的網域狀態會標籤為&#x200B;**已驗證**。

   ![顯示驗證狀態的網域設定資料表。](/help/implementing/cloud-manager/assets/domain-settings-verified.png)

<!--
![Customer managed certificate steps](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

To verify the domain in use, you are required to add and verify a TXT record.

A text record (also known as a TXT record) is a type of resource record in the Domain Name System (DNS). It lets you associate arbitrary text with a hostname. This text could include human-readable details like server or network information.

Cloud Manager uses a specific TXT record to authorize a domain to be hosted in a CDN service. Create a DNS TXT record in the zone that authorizes Cloud Manager to deploy the CDN service with the custom domain and associate it with the backend service. This association is entirely under your control and authorizes Cloud Manager to serve content from the service to a domain. This authorization may be granted and withdrawn. The TXT record is specific to the domain and the Cloud Manager environment.

#### Requirements {#customer-managed-cert-requirements}

Fulfill these requirements before adding a TXT record.

* Identify your domain host or registrar if you do not know it already.
* Be able to edit the DNS records for your organization's domain, or contact the appropriate person who can.
* First, add a custom domain name as described earlier in this article.

#### Add a TXT record for verification {#customer-managed-cert-verification}

1. In the **Verify domain** dialog box, Cloud Manager displays the name and TXT value to use for verification. Copy this value.

1. Log in to your DNS service provider and find the DNS records section. 

1. Add `aemverification.[yourdomainname]` as the **Name** of the value and add the TXT value exactly as it appears in the **Domain Name** field.

   **TXT record examples**

   | Domain | Name | TXT Value |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Save the TXT record to your domain host.

#### Verify TXT record {#customer-managed-cert-verify}

When you are done, you can verify the result by running the following command.

```shell
dig _aemverification.[yourdomainname] -t txt
```

The expected result should display the TXT value provided on the **Verification** tab of the **Add Domain Name** dialog of the Cloud Manager UI.

For example, if your domain is `example.com`, then run:

```shell
dig TXT _aemverification.example.com -t txt
```


>[!TIP]
>
>There are several [DNS lookup tools](https://www.ultratools.com/tools/dnsLookup) available. Google DoH can be used to look up TXT record entries and identify if the TXT record is missing or erroneous.

-->

>[!NOTE]
>
>由於 DNS 傳播延遲，DNS 驗證可能需要幾個小時才能完成。
>
>Cloud Manager會驗證所有權並更新狀態，可在&#x200B;**網域設定**&#x200B;資料表中看到該狀態。 如需詳細資訊，請參閱[檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。

<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->


><!-- The TXT entry and the CNAME or A Record can be set simultaneously on the governing DNS server, thus saving time. -->
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->

