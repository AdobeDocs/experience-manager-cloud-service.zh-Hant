---
title: 新增自訂網域名稱
description: 了解如何使用 Cloud Manager 新增自訂網域名稱。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: dd696580758e7ab9a5427d47fda4275f9ad7997f
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 20%

---


# 新增自訂網域名稱 {#adding-cdn}

了解如何使用 Cloud Manager 新增自訂網域名稱。

## 要求 {#requirements}

在Cloud Manager中新增自訂網域名稱之前，請先滿足這些要求。

* 在新增自訂網域名稱之前，您必須先為要新增的網域新增網域SSL憑證，如檔案[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)中所述。
* 您必須擁有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色，才能在Cloud Manager中新增自訂網域名稱。
* 正在使用Fastly CDN。

>[!IMPORTANT]
>
>即使您使用非AdobeCDN，仍需要將網域新增至Cloud Manager。

## 在何處新增自訂網域名稱{#}

您可以從 Cloud Manager 中的兩個位置新增自訂網域名稱：

* [從域設定頁面](#adding-cdn-settings)
* [從環境頁面](#adding-cdn-environments)

新增自訂網域名稱時，會使用最明確的有效憑證提供網域。 如果多個憑證具有相同的網域，則選擇最近更新的憑證。 Adobe建議您管理憑證，以免網域重疊。

本檔案中描述的任一方法的步驟均以Fastly為基礎。 如果您使用不同的CDN，請使用您選擇要使用的CDN來設定網域。

## 從網域設定頁面新增自訂網域名稱 {#adding-cdn-settings}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 在左側導覽面板中，選取&#x200B;**網域設定**&#x200B;索引標籤

   ![域設定窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 在&#x200B;**網域設定**&#x200B;頁面的右上角附近，按一下&#x200B;**新增網域**。

1. 在&#x200B;**新增網域**&#x200B;對話方塊的&#x200B;**網域名稱**欄位中，輸入您正在使用的自訂網域名稱。
不包括`http://`,`https://`, 或輸入您的域時的空格。

1. 按一下&#x200B;**建立**。

1. 在&#x200B;**驗證網域**&#x200B;對話方塊中，在&#x200B;**您打算搭配此網域使用哪種憑證型別？**&#x200B;下拉式清單，選取下列其中一個選項：

   | 憑證型別 | 說明 |
   | --- | --- |
   | Adobe 管理的憑證 | 選取是否要使用DV （網域驗證）憑證。 此選項適用於大多數的情況，可提供基本網域驗證。 Adobe會自動管理和更新憑證。 |
   | 客戶管理的憑證 | 選取是否要使用EV/OV憑證。 此選項提供EV （延伸驗證）或OV （組織驗證）的增強式安全性。 若需要更嚴格的驗證、更高的信任層級或自訂的憑證控制，請使用。 |

1. 在&#x200B;**驗證網域**&#x200B;對話方塊中，根據您選取的憑證型別，執行下列其中一項作業：

   | 如果您選取憑證型別 | 說明 |
   | --- | ---  |
   | Adobe 管理的憑證 | 請先完成[Adobe受管理憑證步驟](#abobe-managed-cert-steps)，再繼續下一個步驟。 |
   | 客戶管理的憑證 | 請先完成[客戶管理的憑證步驟](#customer-managed-cert-steps)，再繼續下一個步驟。 |

1. 按一下&#x200B;**驗證**。

1. 您現在已準備好[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。

   >[!NOTE]
   >
   >如果您使用自我管理的SSL憑證和自我CDN提供者，則可以略過此步驟，並在準備就緒時直接移至[新增CDN設定](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。



### Adobe受管理憑證步驟 {#adobe-managed-cert-steps}

如果您選取憑證型別&#x200B;*Adobe受管理憑證*，請在&#x200B;**驗證網域**&#x200B;對話方塊中完成下列步驟。

![AdobeManaged憑證步驟](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

若要驗證使用中的網域，您必須新增及驗證CNAME。

`CNAME`或記錄一旦布建，就會將網域的所有網際網路流量路由到它指向的任何地方。 如果未佈建該位置來處理流量，則會發生中斷。如果未經測試，內容可能會存在錯誤。這就是為什麼這個步驟總是在完成測試且準備好上線之後才完成。

若要設定這些設定，請確定是否必須設定`CNAME`或Apex記錄以將您的自訂網域名稱指向Cloud Manager網域名稱。 本檔案的下列章節可協助您判斷適合您DNS設定的記錄型別。

>[!NOTE]
>
>對於Adobe管理的CDN，使用DV （網域驗證）憑證時，只允許具有ACME驗證的網站。

#### 要求 {#dv-requirements}

在設定您的DNS記錄之前，請先滿足這些要求。

* 如果您還不知道您的網域主機或註冊商，請確定它。
* 能夠編輯組織網域的DNS記錄，或聯絡可以編輯的適當人員。
* 您必須已驗證您設定的自訂網域名稱，如檔案[檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)中所述。

#### CNAME記錄 {#cname-record}

正式名稱或 CNAME 記錄是一種將別名對應到真實或正式網域名稱的 DNS 記錄。CNAME 記錄通常用於將子網域 (例如 `www.example.com`) 對應到託管該子網域內容的網域。

登入您的DNS服務提供者並建立`CNAME`記錄，將您的自訂網域名稱指向目標，如下表所示。

| CNAME | 自訂網域名稱指向目標 |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### APEX記錄 {#apex-record}

Apex 網域是不包含子網域的自訂網域，例如`example.com`。Apex網域已透過您的DNS提供者設定`A`、`ALIAS`或`ANAME`記錄。 Apex 網域必須指向特定的 IP 位址。

透過您的網域提供者將下列`A`記錄新增到您網域的DNS設定中。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`



### 客戶管理的憑證步驟 {#customer-managed-cert-steps}

如果您選取憑證型別&#x200B;*客戶管理的憑證*，請在&#x200B;**驗證網域**&#x200B;對話方塊中完成下列步驟。

![客戶管理的憑證步驟](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

若要驗證使用中的網域，您必須新增及驗證TXT記錄。

文字記錄（也稱為TXT記錄）是網域名稱系統(DNS)中的資源記錄型別。 它可讓您關聯任意文字與主機名稱。 此文字可能包括伺服器或網路資訊等人類看得懂的細節。

Cloud Manager使用特定TXT記錄來授權要在CDN服務中託管的網域。 在授權Cloud Manager使用自訂網域部署CDN服務並將其與後端服務關聯的區域中，建立DNS TXT記錄。 此關聯完全在您的控制之下，並授權 Cloud Manager 將內容從服務提供給網域。這種授權可以被授予也可以被撤銷。TXT記錄特定於網域和Cloud Manager環境。

## 要求 {#requirements-customer-cert}

在新增TXT記錄之前，請先滿足這些要求。

* 如果您還不知道您的網域主機或註冊商，請確定它。
* 能夠編輯組織網域的DNS記錄，或聯絡可以編輯的適當人員。
* 首先，新增自訂網域名稱，如本文前面所述。

## 新增TXT記錄以進行驗證 {#verification}

1. 在&#x200B;**驗證網域**&#x200B;對話方塊中，Cloud Manager會顯示用於驗證的名稱和TXT值。 複製此值。

1. 登入您的DNS服務提供者並找到DNS記錄區段。

1. 新增`aemverification.[yourdomainname]`作為值的&#x200B;**Name**，並新增TXT值，就像它在&#x200B;**網域名稱**&#x200B;欄位中顯示的一樣。

   **TXT記錄範例**

   | 網域 | 名稱 | TXT 數值 |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | 複製Cloud Manager UI中顯示的整個值。 此值專用於網域和環境。 例如：<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | 複製Cloud Manager UI中顯示的整個值。 此值專用於網域和環境。 例如：<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. 將TXT記錄儲存至您的網域主機。

## 驗證TXT記錄 {#verify}

完成後，可執行下列指令來驗證結果。

```shell
dig _aemverification.[yourdomainname] -t txt
```

預期結果應顯示Cloud Manager UI之&#x200B;**新增網域名稱**&#x200B;對話方塊的&#x200B;**驗證**&#x200B;索引標籤上提供的TXT值。

例如，如果您的網域是 `example.com`，然後執行：

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>有數個[DNS查詢工具](https://www.ultratools.com/tools/dnsLookup)可供使用。 Google DoH可用於查詢TXT記錄專案並識別TXT記錄是否遺失或錯誤。

>[!NOTE]
>
>由於 DNS 傳播延遲，DNS 驗證可能需要幾個小時才能完成。
>
>Cloud Manager會驗證所有權並更新狀態，這可在網域設定表中看到。 如需詳細資訊，請參閱[檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。

<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->

>[!TIP]
>
>TXT專案和CNAME或A記錄可以同時設定在控管的DNS伺服器上，因此可節省時間。
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


## 從環境頁面 {#adding-cdn-environments}

從&#x200B;**環境**&#x200B;頁面新增自訂網域名稱的步驟與[從「網域設定」頁面](#adding-cdn-settings)新增自訂網域名稱的步驟相同，但進入點不同。 按照以下步驟從&#x200B;**環境**&#x200B;頁面。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 瀏覽至感興趣環境的&#x200B;**環境詳細資料**&#x200B;詳細資訊頁面。

   ![在環境詳情頁面輸入網域名稱](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用&#x200B;**網站網域名稱**&#x200B;表提交自訂網域名稱。

   1. 輸入自訂網域名稱。
   1. 從下拉清單中選擇與此名稱關聯的 SSL 憑證。
   1. 按一下&#x200B;**+新增**。

   ![新增自訂網域名稱](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. **新增網域名稱**&#x200B;對話方塊會開啟至&#x200B;**網域名稱**&#x200B;索引標籤。 繼續進行，如同從[網域設定]頁面](#adding-cdn-settings)新增自訂網域名稱一樣。 —>[
