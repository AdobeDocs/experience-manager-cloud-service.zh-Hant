---
title: AEM as a Cloud Service 團隊和產品設定檔
description: 了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授予和限制您的授權 Adobe 解決方案的存取權。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: b9cc5450effb70afcb67725fe38826646d947da9
workflow-type: ht
source-wordcount: '2124'
ht-degree: 100%

---


# AEM as a Cloud Service 團隊和產品設定檔 {#product-profiles}

了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授予和限制您的授權 Adobe 解決方案的存取權。

## 產品設定檔 {#profiles}

在授予使用者特定 Adobe 解決方案的存取權時，您不一定想要授予他們完整的存取權。產品設定檔使每個解決方案都可以擁有自己的一組使用者權限。這些可透過 [Admin Console](/help/journey-onboarding/admin-console.md) 取得和存取。

Adobe Admin Console 具有產品、產品執行個體和產品設定檔的結構化階層，可為組織的內部使用者指派會籍，使其能夠存取授權的解決方案和功能。

<!-- Alexandru: Drafting for now 

Your AEM as a Cloud Service team members are added and assigned to one or more of the following product profiles via the Admin Console during onboarding.

* **AEM Administrators**: An AEM administrator is typically assigned to developers, in particular developers who need access to, for example, the development environments. The AEM administrator's product profile is used to grant administrator privileges in the associated AEM instance.

* **AEM Users**: AEM users are the users in your organization who use AEM as a Cloud Service generally to create content. These users need to access AEM to do their tasks. The AEM users product profile is typically assigned to an AEM content author who creates and reviews the content. This content can be of many types such as pages, assets, publications, and so on. The AEM users product profile shown below is assigned to these members.

![Product profiles](/help/onboarding/assets/admin-console-profiles.png) -->

## AEM as a Cloud Service 產品設定檔 {#aem-product-profiles}

AEM as a Cloud Service 是完全的雲端原生產品，可提供 AEM 即服務。它以雲端原生方式提供 AEM，具有永遠可用、永遠最新、永遠安全和永遠可擴展等新屬性。同時，它讓客戶仍能享有 AEM 作為可自訂平台的重要價值主張，並允許企業級團隊整合到他們的開發和交付程序中。若要深入了解 AEM as a Cloud Service，請參閱 [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)。

### 組織層級產品執行個體 {#org-level-product-instances}

>[!NOTE]
>
> 本文所述的某些產品執行個體和產品設定檔可能僅會出現在新建立的環境中。請參閱[為現有環境新增產品設定檔區段](#adding-product-profiles-for-existing-environments)，了解如何將您的環境現代化。

Adobe 首次處理 AEM 解決方案的授權時，Adobe Admin Console 中的 Adobe Experience Manager as a Cloud Service 產品下方會出現兩個產品執行個體：

* **AEM 組織層級** - 包含一或多個產品設定檔，代表對所有 AEM 環境 (而不僅僅是單一環境) 範圍內功能的存取權
* **Cloud Manager** - 包含與 Cloud Manager 功能之不同存取層級對應的產品設定檔。

<!--
>[!NOTE]
>
>For existing programs, the AEM Org-Level Product Instance is created upon selecting the **Update product** profiles action for a given environment.
-->

![組織層級產品執行個體](/help/onboarding/assets/orglevel.png)

AEM 組織層級產品執行個體內有一個名為 AEM 組織層級報告者的產品設定檔，目前未使用該設定檔，但未來可能會用來表示擷取有關 AEM 產品授權資訊的存取權。

Forms Communication 解決方案獲得授權時，對應的產品設定檔也會出現在 AEM 組織層級產品執行個體下方。

![報告者產品設定檔](/help/onboarding/assets/org-level-reporters.png)

### 環境和層級產品執行個體 {#environment-and-tier-level-product-instances}

在使用一或多個 AEM 環境佈建新方案時，每個環境都會出現兩個產品執行個體，分別包含用於編寫和發佈的產品設定檔。

![環境產品執行個體](/help/onboarding/assets/env-productinstances.png)

以下為編寫產品執行個體中的產品設定檔，適用於已在包含 AEM Sites 的方案中佈建環境的組織：

![Sites 產品執行個體](/help/onboarding/assets/sites-product-instances.png)

以下表格說明在環境階層特定產品執行個體下方可能列出的產品設定檔清單。

<table style="table-layout:auto">
    <tr>
        <th>產品執行個體</th>
        <th>命名慣例</th>
        <th>預設服務</th>
        <th>說明</th>
    </tr>
    <tr>
        <td>AEM 作者</td>
        <td>AEM Sites 內容經理 - 作者 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Sites 內容經理</td>
        <td>
            <ul>
                <li>適用於控制此環境中 AEM Sites 編寫功能的存取權。此產品設定檔中的使用者將是 AEM Sites 內容作者 AEM 群組的成員，而該群組是在 AEM 中自動建立。應在 AEM 中使用所需的存取層級設定 AEM 群組權限。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM Sites 內容經理 - 服務」AEM 群組的成員。</li>
                      <!--  <li>users in this product profile will have access to AEM Sites Content Management API.</li>
                        <li>an Adobe Developer Console API OAuth S2S project containing AEM Sites Content Management API can optionally be scoped to this environment.</li>-->
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM 管理員 - 作者 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM 管理員</td>
        <td>
            <ul>
                <li>適用於不受限制地存取 AEM 編寫和發佈環境功能。此產品設定檔中的使用者會是 AEM 管理員作者 AEM 群組的成員，而該群組是在 AEM 中自動建立。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM 管理員 - 服務」AEM 群組的成員</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM 使用者 - 作者 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM 使用者</td>
        <td>
            <ul>
                <li>適用於極有限制地存取 AEM 編寫環境功能。此產品設定檔中的使用者會是「投稿人」AEM 群組的成員，且該群組是在 AEM 中自動建立</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM 使用者 - 服務」AEM 群組的成員</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM 報告者 - 作者 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM 報告者</td>
        <td>
            <ul>
                <li>目前未使用，但未來可能會提供對此環境之編寫階層相關報告資訊的存取權。</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets 協作者 - 作者 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Assets 協作者使用者</td>
        <td>
        <ul>
                <li>透過整合其他 Adobe 產品和非 Adobe 應用程式中可供貴組織使用的資產來運用 Experience Manager 中的資產。
                </li>
                <li>使用內建的 Adobe Express 和 Firefly，善用專業設計的範本、品牌套件、Adobe Stock 資產等等，以建立和編輯資產。</li>
                <li>透過 AEM Assets Content Hub 入口網站來存取貴組織中已核准的資產並加以運用。</li>
          <ul>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets 進階使用者 - 作者 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Assets 進階使用者</td>
<td>
        <ul>
                <li>存取所有 AEM Assets 功能，包含管理資產、中繼資料，以及有關數位資產的整體治理和自動化。</li>
                <li>透過整合其他 Adobe 產品和非 Adobe 應用程式中可供貴組織使用的資產來運用 Experience Manager 中的資產。
                </li>
                <li>使用內建的 Adobe Express 和 Firefly，善用專業設計的範本、品牌套件、Adobe Stock 資產等等，以建立和編輯資產。</li>
                <li>透過 AEM Assets Content Hub 入口網站來存取貴組織中已核准的資產並加以運用。</li>
          <ul>
</td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms 內容經理 - 作者 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Forms 內容經理</td>
        <td>
            <ul>
                <li>適用於控制此環境中 AEM Forms 編寫功能的存取權。此產品設定檔中的使用者會是 AEM Forms 表單使用者 AEM 群組的成員，且該群組是在 AEM 中自動建立。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM Forms 內容經理 - 服務」AEM 群組的成員。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms 開發人員 - 作者 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Forms 開發人員</td>
        <td>
            <ul>
                <li>適用於控制此環境中 AEM Forms 編寫功能的存取權。此產品設定檔中的使用者會是 AEM Forms 表單進階使用者 AEM 群組的成員，且該群組是在 AEM 中自動建立。除了正常的表單編寫任務之外，這些使用者還有權上傳 XDP 和編寫表單資料模型。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM Forms 開發人員 - 服務」AEM 群組的成員。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms Communications Service 使用者 - 作者 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Forms Communications Service 使用者</td>
        <td>
            <ul>
                <li>適用於控制此環境中 AEM Forms Communications Services 功能的存取權。此產品設定檔中的使用者會是 AEM Forms 表單使用者 AEM 群組的成員，且該群組是在 AEM 中自動建立。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM Forms Communications Service 使用者 - 服務」AEM 群組的成員。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>AEM 發佈</td>
        <td>AEM 使用者 - 發佈 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM 使用者</td>
        <td>
            <ul>
                <li>適用於極有限制地存取 AEM 編寫環境功能。此產品設定檔中的使用者會是「投稿人」AEM 群組的成員，且該群組是在 AEM 中自動建立</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM 使用者 - 服務」AEM 群組的成員。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM 報告者 - 發佈 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM 報告者</td>
        <td>
            <ul>
                <li>目前未使用，但未來可能會提供對此環境之發佈階層相關報告資訊的存取權。</li>
            </ul>
        </td>
    </tr>
   <tr>
        <td></td>
        <td>AEM Forms Communications Service 使用者 - 發佈 - 程式 <code>id</code> - 環境 <code>id</code></td>
        <td>AEM Forms Communications Service 使用者</td>
        <td>
            <ul>
                <li>適用於控制此環境中 AEM Forms Communications Services 功能的存取權。此產品設定檔中的使用者會是 AEM Forms 表單使用者 AEM 群組的成員，且該群組是在 AEM 中自動建立。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM Forms Communications Service 使用者 - 服務」AEM 群組的成員。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
</table>

請注意，預設情況下，每個產品設定檔都啟用了相關的產品設定檔服務。除非您有複雜的存取要求，否則建議僅選取「預設服務」。AEM 中會建立對應的 AEM 群組，且命名慣例為 `<Product Profile Prefix> - Service` (例如，**AEM Sites 內容經理 - 服務**)，且位於上層產品設定檔的使用者會自動成為對應 AEM 群組的成員。

AEM 中與該服務相關聯的 AEM 群組會有一組彙總的使用者，且這些使用者存在於該環境階層組合之該服務相關聯產品設定檔中。

![服務](/help/onboarding/assets/services.png)

下圖內容代表反映出 AEM Sites 內容經理編寫階層產品設定檔和服務的 AEM 群組。

![AEM 群組與服務的對應](/help/onboarding/assets/profile-to-service-mapping.png)

>[!NOTE]
>
>指派給 AEM as a Cloud Service 產品設定檔的每個使用者透過&#x200B;**雲端管理員使用者**&#x200B;角色具有對 Cloud Manager 的唯讀存取權。
>
>唯具有&#x200B;**雲端管理員使用者**&#x200B;角色的使用者可以使用「**方案**」選單選項，登入 Cloud Manager 並瀏覽至 AEM 編寫環境 (如果存在)。**雲端管理員使用者**&#x200B;角色不足以存取方案詳細資料。如果需要此類存取權，系統管理員必須授予使用者其他角色。

>[!WARNING]
>
>**AEM 管理員**&#x200B;產品設定檔名稱不得變更。如果變更 **AEM 管理員**&#x200B;產品設定檔名稱，會將所有指派到該設定檔之使用者的管理員權限移除。

>[!TIP]
>
>* 若要深入了解 AEM 產品設定檔，請參閱「[指派 AEM 產品設定檔](/help/journey-onboarding/assign-profiles-aem.md)」。
>* 如需上線流程的詳細資訊，請參閱[上線歷程](/help/journey-onboarding/overview.md)

### 為現有環境新增產品設定檔 {#adding-product-profiles-for-existing-environments}

2024 年 4 月初以前建立的環境，可能缺少上面各區段中描述的組織級產品執行個體以及特定的產品設定檔。現有的產品設定檔也會缺少服務切換功能。建議更新這些產品設定檔，因為這是存取某些未來 API 的先決條件。

如果方案中的一個或多個環境需要更新其產品設定檔，Cloud Manager 會顯示以下通知。請注意，環境必須處於最新的 AEM 版本才能更新其產品設定檔。

![現代化產品設定檔](/help/onboarding/assets/modernize-product-profiles.png)

按一下「**新增產品設定檔**」按鈕會開啟一個選單，其中顯示用於將新產品設定檔新增至程式中的所有可用環境或個別環境的選項。

![更換環境](/help/onboarding/assets/choose-env-r.png)

按一下「**所有環境**」，將新產品設定檔新增至方案中的所有環境。或者，按一下「**個別環境**」，將新產品設定檔新增至選定的環境；這會讓使用者導覽至環境清單頁面，於此頁面中可使用「**更多選項**」圖示選取「**新增產品設定檔**」動作。

![個別環境](/help/onboarding/assets/individual-environments.png)

您也可以將產品設定檔新增至選定的環境，方法是導覽至方案概觀頁面的「環境」區段，按一下與環境對應的「更多選項」圖示，然後選取「新增產品設定檔」。

新增產品設定檔時，環境狀態會顯示「正在新增產品設定檔」，隨後於流程完成時，會顯示「正在執行」。


## Cloud Manager 產品設定檔 {#cloud-manager-product-profiles}

Cloud Manager 具有預先設定的產品設定檔，可以將其視為角色型權限。您的系統管理員負責將您的 Cloud Manager 團隊指派給這些產品設定檔來設定團隊。

>[!TIP]
>
>如需更多詳細資訊，請參閱[Cloud Manager 中的角色型權限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)。

每個產品設定檔都有與之關聯的特定權限。

* **業務負責人**
   * 在此角色中，您擁有權限可以新增方案或編輯方案、新增或更新環境、將程式碼部署到 AEM 環境或執行程式碼品質檢查。
   * 這類使用者會負責定義 KPI、核准生產部署並在必要時覆寫重要的 3 層級失敗。
* **部署管理員**
   * 在此角色中，您擁有權限可新增或更新環境、執行管道，和將程式碼部署到 AEM 環境或執行程式碼品質檢查。
   * 這類使用者會管理部署操作，並使用 Cloud Manager 來執行中繼/生產部署、編輯 CI/CD 管道、核准重要的 3 層級失敗 (如有必要)，並可存取 Git 存放庫。
* **開發人員**
   * 在此角色中，您擁有權限可產生個人存取權杖以存取 Git。
   * 這類使用者會開發和測試自訂應用程式，並主要使用 Cloud Manager 來檢視部署狀態，且可存取 Git 存放庫程式來認可程式碼。
* **方案管理員**
   * 在此角色中，您擁有權限可安排管道、覆寫 3 層品質門檻並提供生產核准。
   * 這類使用者會使用 Cloud Manager 來執行團隊設定、審查狀態、檢視 KPI，並可在必要時核准重要的 3 層級失敗。

可以將一個使用者指派給多個產品設定檔。例如，同時指派&#x200B;**業務負責人**&#x200B;和&#x200B;**部署管理員**&#x200B;角色以賦予使用者兩者的所有權限。

您的 Cloud Manager 團隊將至少包括：

* 一位&#x200B;**業務負責人**，他通常也是系統管理員，並且必須是第一個登入和存取 Cloud Manager 的人
* 一位&#x200B;**部署管理員**
* 一位&#x200B;**開發人員**

>[!NOTE]
>
>要取得AEM as a Cloud Service 的存取權，使用者必須屬於以下兩個產品設定檔之一：`AEM Users` 或 `AEM Administrators`。管理 Cloud Manager 的權限是不夠的。

>[!TIP]
>
>* 若要深入了解 Cloud Manager 產品設定檔，請參閱「[將團隊成員指派到 Cloud Manager 產品設定檔](/help/journey-onboarding/assign-profiles-cloud-manager.md)」。
>* 如需上線流程的詳細資訊，請參閱「[上線歷程](/help/journey-onboarding/overview.md)」。
