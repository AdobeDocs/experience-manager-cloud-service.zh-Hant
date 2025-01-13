---
title: 適用於AEM as a Cloud Service的客戶自控金鑰
description: 瞭解如何管理AEM as a Cloud Service的加密金鑰
feature: Security
role: Admin
hide: true
hidefromtoc: true
source-git-commit: d00a3099d5468c711ed80a69d74f0a3d51f24672
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---


# 為AEM as a Cloud Service設定客戶自控金鑰 {#cusomer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Service目前將客戶資料儲存在Azure Blob Storage和MongoDB，預設會使用提供者管理的加密金鑰來保護資料。 雖然此設定符合許多組織的安全需求，但受規管產業的企業或需要加強資料主權的企業，可能會尋求對其加密實務的更大控制。 對於優先考慮資料安全性、法規遵循以及管理加密金鑰的組織，客戶自控金鑰(CMK)解決方案提供了重要的增強功能。

## 正在解決的問題 {#the-problem-being-solved}

提供者管理的金鑰可能會為金融、醫療及政府等行業的企業帶來疑慮，因為在這些行業中，嚴格的法規要求全面控制資料安全性。 如果無法控制關鍵管理，組織將面臨各種挑戰，包括符合法規要求、實作自訂安全性原則，以及確保完整的資料主權。

客戶自控金鑰(CMK)的推出讓AEM客戶能夠完全控制其加密金鑰，藉此解決上述問題。 透過Microsoft Entra ID （先前稱為Azure Active Directory）進行驗證，AEM CS可安全地連線至客戶的Azure Key Vault，讓他們管理其加密金鑰的生命週期，涵蓋金鑰建立、輪換和撤銷。

CMK具備數個優點：

* **增強式安全性：**&#x200B;客戶可確保他們的加密實務符合特定的安全性需求，讓他們完全不必擔心資料保護問題。
* **法規遵循彈性：**&#x200B;企業可以完全控制關鍵生命週期，輕鬆適應不斷演變的法規標準，例如GDPR、HIPAA或CCPA，以確保其法規遵循狀況持續穩固。
* **緊密整合：** CMK解決方案直接與AEM CS中的Azure Blob Storage和MongoDB整合，確保不會中斷儲存作業或可用性，同時為客戶提供強大的加密功能。

透過採用CMK，客戶可以加強對其資料安全性和加密實務的控制，增強合規性並降低風險，同時繼續享有AEM CS的擴充性和彈性。

AEM as a Cloud Service可讓您自備加密金鑰，用於加密閒置的資料。 本指南提供在AEM as a Cloud Service的Azure Key Vault中設定客戶自控金鑰(CMK)的步驟。

>[!WARNING]
>
>設定CMK後，您無法還原為系統管理的金鑰。 您有責任安全地管理您的金鑰，並提供對Azure中金鑰儲存庫、金鑰和CMK應用程式的存取權，以防止無法存取您的資料。

我們也會引導您完成下列步驟，以建立和設定所需的基礎架構：

1. 設定您的環境
1. 從Adobe取得應用程式ID
1. 建立新的資源群組
1. 建立金鑰
1. 授予Adobe對金鑰Kault的存取權
1. 建立加密金鑰

您需要與Adobe共用金鑰儲存庫URL、加密金鑰名稱以及金鑰儲存庫的相關資訊。

## 設定環境 {#setup-your-environment}

Azure命令列介面(CLI)是本指南的唯一需求。 如果您尚未安裝Azure CLI，請依照官方的安裝指示[這裡](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)。

在繼續本指南的其餘部分之前，請使用`az login`登入您的CLI。

>[!NOTE]
>
>雖然本指南使用Azure CLI，但可以透過Azure主控台執行相同的作業。 如果您偏好使用Azure主控台，請使用下列指令作為參考。

## 從Adobe取得應用程式ID {#obtain-an-application-id-from-adobe}

Adobe會提供您在本指南其他章節中所需的Entra應用程式ID。 如果您還沒有應用程式ID，請聯絡Adobe以取得此ID。

## 建立新的資源群組 {#create-a-new-resource-group}

在您選擇的位置中建立新的資源群組。

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

如果您已經有資源群組，請隨時改用它。 在本指南的其餘部分中，資源群組的位置及其名稱分別以`$location`和`$resourceGroup`識別。

## 建立金鑰儲存庫 {#create-a-key-vault}

您必須建立金鑰儲存庫以包含您的加密金鑰。 金鑰儲存庫必須啟用清除保護。 若要從其他Azure服務加密閒置資料，必須執行清除保護。 此外，必須啟用公用網路存取，以確保Adobe租使用者可存取金鑰儲存庫。

>[!IMPORTANT]
>建立已停用「公用網路存取」的「金鑰儲存庫」會強制所有與「金鑰儲存庫」相關的作業（例如「金鑰建立」或「輪換」）都必須從具有KeyVault網路存取權的環境執行，例如，可以存取KeyVault的VM。

```powershell
# Reuse this information from the previous step.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Choose a name for the key vault.
$keyVaultName="<KEY VAULT NAME>"

# Create the key vault.
az keyvault create `
  --location $location `
  --resource-group $resourceGroup `
  --name $keyVaultName `
  --default-action=Deny `
  --enable-purge-protection `
  --enable-rbac-authorization `
  --public-network-access Disabled
```

## 授予Adobe對金鑰儲存庫的存取權 {#grant-adone-access-to-the-key-vault}

在此步驟中，您將允許Adobe透過Entra應用程式存取您的金鑰儲存庫。 Entra應用程式的ID應該已經由Adobe提供。

首先，您必須建立附加至Entra應用程式的服務主體，並為其指派&#x200B;**金鑰儲存庫Reader**&#x200B;和&#x200B;**金鑰儲存庫加密使用者**&#x200B;角色。 這些角色僅限於本指南中建立的金鑰儲存庫。

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# The application ID is provided by Adobe.
$appId="<APPLICATION ID>"

# Retrieve the ID of the key vault.
$keyVaultId=(az keyvault show --resource-group $resourceGroup --name $keyVaultName --query id --output tsv)

# Create a new service principal.
$servicePrincipalId=(az ad sp create --id $appId --query id --out tsv)

# Assign the roles to the service principal.
az role assignment create --assignee $servicePrincipalId --role "Key Vault Reader" --scope $keyVaultId
az role assignment create --assignee $servicePrincipalId --role "Key Vault Crypto User" --scope $keyVaultId
```

## 建立加密金鑰 {#create-an-ecryption-key}

最後，您可以在金鑰儲存庫中建立加密金鑰。 請注意，您需要&#x200B;**金鑰儲存庫加密管理員**&#x200B;角色才能完成此步驟。 如果登入的使用者沒有此角色，請聯絡您的系統管理員以將此角色授予您，或要求已具有該角色的人為您完成此步驟。

需要透過網路存取金鑰儲存庫才能建立加密金鑰。 首先確認您可以存取金鑰儲存庫並繼續建立金鑰：

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Chose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## 共用金鑰儲存庫資訊 {#share-the-key-vault-information}

此時，您已準備就緒。 您只需要與Adobe共用一些必要資訊，他們會負責為您設定環境。

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# Retrieve the URL of your key vault.
$keyVaultUri=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.vaultUri `
    --output tsv)

# In addition we would need the tenantId and the subscriptionId in order to setup the connection.
$tenantId=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.tenantId `
    --output tsv)
$subscriptionId="<Subscription ID>"
```


## 撤銷金鑰存取許可權的影響 {#implications-of-revoking-key-access}

撤銷或停用金鑰儲存庫、金鑰或CMK應用程式的存取權可能會造成重大中斷，包括平台運作上的重大變更。 停用這些索引鍵後，可能無法存取Platform中的資料，且任何依賴此資料的下游作業都將停止運作。 在對您的關鍵設定進行任何變更之前，完全瞭解下游影響至關重要。

如果您決定撤銷Platform對您資料的存取權，可以從Azure的金鑰儲存庫中移除與應用程式相關聯的使用者角色，藉此進行撤銷。

## 後續步驟 {#next-steps}

聯絡Adobe與分享：

* 您的金鑰儲存庫的URL。 您在此步驟中擷取了該檔案，並將其儲存在`$keyVaultUri`變數中。
* 您的加密金鑰的名稱。 您已在先前的步驟中建立金鑰，並將其儲存在`$keyName`變數中。
* 設定金鑰儲存庫連線所需的`$resourceGroup`、`$subscriptionId`和`$tenantId`。

<!-- Alexandru: hiding this for now

### Private Link Approvals {#private-link-approvals}

>[!TIP]
>You can also consult the [Azure Documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/private-link-service?tabs=portal#how-to-manage-a-private-endpoint-connection-to-key-vault-using-the-azure-portal) on how to approve a Private Endpoint Connection.

Afterwards, an Adobe Engineer assigned to you will contact you to confirm the creation of the private endpoints, and will request you to approve a set of required Connection Requests. The requests can be approved either using the Azure Portal UI, where you can go to **KeyVault > Settings > Networking > Private Endpoint Connections** and approve the requests with names similar to these: 

`mongodb-atlas-<REGION>-<NUMBER>`, `storage-account-private-endpoint` and `backup-storage-account-private-endpoint`. 

Notify the Adobe Engineer once this process is complete and the Private Endpoints show up as **Approved**. -->

## Private Beta中的客戶自控金鑰 {#customer-managed-keys-in-private-beta}

Adobe的工程團隊目前正在利用Azure的私人連結，致力於CMK的增強實作。 新的實作將允許透過Azure骨幹分享您的金鑰，這要歸功於Adobe的租使用者與您的金鑰儲存庫之間的直接私人連結連線。

此增強型實作目前在Private Beta中，且可為同意訂閱Private Beta方案並與Adobe工程密切合作的選定客戶啟用。 如果您對使用私人連結的CMK適用的Private Beta感興趣，請聯絡Adobe瞭解詳情。
