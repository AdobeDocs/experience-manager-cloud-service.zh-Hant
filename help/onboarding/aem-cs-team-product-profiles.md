---
title: AEM as a Cloud Service 團隊和產品設定檔
description: 了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授與和限制您的授權 Adobe 解決方案的存取權。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: c8534ddf84998377ee63575403417165ccec2dbd
workflow-type: tm+mt
source-wordcount: '2059'
ht-degree: 34%

---


# AEM as a Cloud Service 團隊和產品設定檔 {#product-profiles}

了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授與和限制您的授權 Adobe 解決方案的存取權。

## 產品設定檔 {#profiles}

在授與使用者特定 Adobe 解決方案的存取權時，您不一定要授與他們完整的存取權。產品設定檔使每個解決方案都可以擁有自己的一組使用者權限。這些可透過 [Admin Console](/help/journey-onboarding/admin-console.md) 取得和存取。

Adobe Admin Console具有產品、產品執行個體和產品設定檔的結構化階層，可為組織的內部使用者指派成員資格，讓他們存取已授權的解決方案和功能。

<!-- Alexandru: Drafting for now 

Your AEM as a Cloud Service team members are added and assigned to one or more of the following product profiles via the Admin Console during onboarding.

* **AEM Administrators**: An AEM administrator is typically assigned to developers, in particular developers who need access to, for example, the development environments. The AEM administrator's product profile is used to grant administrator privileges in the associated AEM instance.

* **AEM Users**: AEM users are the users in your organization who use AEM as a Cloud Service generally to create content. These users need to access AEM to do their tasks. The AEM users product profile is typically assigned to an AEM content author who creates and reviews the content. This content can be of many types such as pages, assets, publications, and so on. The AEM users product profile shown below is assigned to these members.

![Product profiles](/help/onboarding/assets/admin-console-profiles.png) -->

## AEM as a Cloud Service 產品設定檔 {#aem-product-profiles}

AEM as a Cloud Service 是完全的雲端原生產品，可提供 AEM 即服務。它以雲端原生方式提供 AEM，具有永遠可用、永遠最新、永遠安全和永遠可擴展等新屬性。同時，它保留了 AEM 作為可自訂平台提供給客戶的主要價值主張，並允許企業級團隊整合到他們的開發和交付方案中。若要深入了解 AEM as a Cloud Service，請參閱 [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)。

### 組織層級產品例項 {#org-level-product-instances}

>[!NOTE]
>
> 本文中說明的某些產品執行個體和產品設定檔可能只會出現在新建立的環境中。 未來的機制將允許更新現有的環境。

當Adobe首次處理AEM解決方案的授權時，兩個產品執行個體會出現在Adobe Admin Console的Adobe Experience Manager as a Cloud Service產品下方：

* **AEM組織層級** — 包含一或多個產品設定檔，這些設定檔代表存取涵蓋所有AEM環境的功能，而不只是存取單一功能
* **Cloud Manager** — 包含與不同層級的Cloud Manager功能存取權相對應的產品設定檔。

<!--
>[!NOTE]
>
>For existing programs, the AEM Org-Level Product Instance is created upon selecting the **Update product** profiles action for a given environment.
-->

![組織層級產品執行個體](/help/onboarding/assets/orglevel.png)

在AEM組織層級產品執行個體內是名為AEM組織層級報告者的產品設定檔，目前不使用，但未來可能會用於表示擷取AEM產品授權相關資訊的存取權。

當Forms通訊解決方案獲得授權時，對應的產品設定檔也會出現在AEM組織層級的產品執行個體下。

![記者產品設定檔](/help/onboarding/assets/org-level-reporters.png)

### 環境和層級產品執行個體 {#environment-and-tier-level-product-instances}

使用一或多個AEM環境布建新程式後，每個環境將顯示兩個產品執行個體，分別包含用於製作和發佈的產品設定檔。

![環境產品執行個體](/help/onboarding/assets/env-productinstances.png)

以下是作者產品例項中的產品設定檔，適用於已在包含AEM Sites的方案中提供環境的組織：

![網站產品執行個體](/help/onboarding/assets/sites-product-instances.png)

下表說明環境層特定產品執行個體底下的可能產品設定檔清單。

<table style="table-layout:auto">
    <tr>
        <th>產品例項</th>
        <th>命名慣例</th>
        <th>預設服務</th>
        <th>說明</th>
    </tr>
    <tr>
        <td>AEM 作者</td>
        <td>AEM Sites內容管理員 — 作者 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM Sites內容管理員</td>
        <td>
            <ul>
                <li>用於在此環境中控制存取AEM Sites作者功能。 此產品設定檔中的使用者會成為AEM Sites內容作者AEM群組的成員，此群組會自動在AEM中建立。 AEM群組許可權應在AEM中以所需的存取層級設定。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM Sites內容管理員 — 服務」AEM群組的成員。</li>
                      <!--  <li>users in this product profile will have access to AEM Sites Content Management API.</li>
                        <li>an Adobe Developer Console API OAuth S2S project containing AEM Sites Content Management API can optionally be scoped to this environment.</li>-->
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM管理員 — 作者 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM管理員</td>
        <td>
            <ul>
                <li>旨在不受限制地存取AEM作者和發佈環境功能。 此產品設定檔中的使用者將成為AEM管理員的成員，可撰寫在AEM中自動建立的AEM群組。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也將是「AEM管理員 — 服務」AEM群組的成員</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM使用者 — 作者 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM 使用者</td>
        <td>
            <ul>
                <li>旨在提供非常有限的AEM作者環境功能存取權。 此產品設定檔中的使用者將會是在AEM中自動建立的「貢獻者」AEM群組的成員</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM使用者 — 服務」AEM群組的成員</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Reporters — 作者 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM記者</td>
        <td>
            <ul>
                <li>目前未使用，但未來可能會提供此環境作者階層的相關報表資訊存取權。</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets Collaborator — 作者 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM Assets Collaborator使用者</td>
        <td>
        <ul>
                <li>旨在以唯讀方式存取DAM。 此產品設定檔中的使用者將會是在AEM中自動建立的「貢獻者」AEM群組的成員。
                </li>
                <li>
                此外，它提供Adobe Express許可權以建立資產變數。
                </li>
          <ul>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets超級使用者 — 作者 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM Assets超級使用者</td>
<td>
        <ul>
                <li>旨在以唯讀方式存取DAM。 此產品設定檔中的使用者將會是在AEM中自動建立的「貢獻者」AEM群組的成員。
                </li>
                <li>
                此外，它提供Adobe Express許可權以建立資產變數。
                </li>
          <ul>
</td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms內容管理員 — 作者 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM Forms內容管理員</td>
        <td>
            <ul>
                <li>用於在此環境中控制存取AEM Forms作者功能。 此產品設定檔中的使用者將會是在AEM中自動建立的AEM Forms forms-users AEM群組的成員。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM Forms內容管理員 — 服務」AEM群組的成員。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms開發人員 — 作者 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM Forms開發人員</td>
        <td>
            <ul>
                <li>用於在此環境中控制存取AEM Forms作者功能。 此產品設定檔中的使用者將會是在AEM中自動建立的AEM Forms forms-power-users AEM群組的成員。 除了正常表單編寫工作之外，這些使用者還有權上傳XDP和編寫表單資料模型。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM Forms開發人員 — 服務」AEM群組的成員。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms Communications Service使用者 — 作者 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM Forms Communications Service使用者</td>
        <td>
            <ul>
                <li>旨在控制此環境中對AEM Forms Communications Services功能的存取。 此產品設定檔中的使用者將會是在AEM中自動建立的AEM Forms forms-users AEM群組的成員。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM Forms Communications Service使用者 — 服務」AEM群組的成員。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>AEM 發佈</td>
        <td>AEM使用者 — 發佈 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM 使用者</td>
        <td>
            <ul>
                <li>旨在提供非常有限的AEM作者環境功能存取權。 此產品設定檔中的使用者將會是在AEM中自動建立的「參與者」AEM群組的成員</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM使用者 — 服務」AEM群組的成員。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Reporters — 發佈 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM記者</td>
        <td>
            <ul>
                <li>目前未使用，但未來可能會提供此環境發佈層級相關報表資訊的存取權。</li>
            </ul>
        </td>
    </tr>
   <tr>
        <td></td>
        <td>AEM Forms Communications Service使用者 — 發佈 — 方案<code>id</code> — 環境 <code>id</code></td>
        <td>AEM Forms Communications Service使用者</td>
        <td>
            <ul>
                <li>旨在控制此環境中對AEM Forms Communications Services功能的存取。 此產品設定檔中的使用者將會是在AEM中自動建立的AEM Forms forms-users AEM群組的成員。</li><br>
                <li>如果預設服務保持選取狀態
                    <ul>
                        <li>此產品設定檔中的使用者也會是「AEM Forms Communications Service使用者 — 服務」AEM群組的成員。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
</table>

請注意，每個產品設定檔都會預設啟用相關聯的產品設定檔服務。 除非您有複雜的存取需求，否則建議您只選取預設服務。 將在AEM中以命名慣例`<Product Profile Prefix> - Service` (例如&#x200B;**AEM Sites Content Managers - Service**)建立對應的AEM群組，父產品設定檔中的使用者會自動成為該對應AEM群組的成員。

與該服務相關聯的AEM中的AEM群組將具有彙總使用者集，這些使用者集存在於該環境層組合之該服務的所有相關聯產品設定檔中。

![服務](/help/onboarding/assets/services.png)

下圖代表反映AEM Sites內容管理員作者層產品設定檔和服務的AEM群組。

![AEM群組對服務對應](/help/onboarding/assets/profile-to-service-mapping.png)

>[!NOTE]
>
>指派給 AEM as a Cloud Service 產品設定檔的每個使用者透過&#x200B;**雲端管理員使用者**&#x200B;角色具有對 Cloud Manager 的唯讀存取權。
>
>唯具有&#x200B;**雲端管理員使用者**&#x200B;角色的使用者可以使用「**方案**」選單選項，登入 Cloud Manager 並瀏覽至 AEM 製作環境 (如果存在)。**雲端管理員使用者**&#x200B;角色不足以存取方案詳細資料。如果需要此類存取權，系統管理員必須授予使用者其他角色。

>[!WARNING]
>
>**AEM 管理員**&#x200B;產品設定檔名稱不得變更。如果變更 **AEM 管理員**&#x200B;產品設定檔名稱，會將所有指派到該設定檔之使用者的管理員權限移除。

>[!TIP]
>
>* 若要深入了解 AEM 產品設定檔，請參閱「[指派 AEM 產品設定檔](/help/journey-onboarding/assign-profiles-aem.md)」。
>* 如需上線流程的詳細資訊，請參閱[上線歷程](/help/journey-onboarding/overview.md)

### 新增現有環境的產品設定檔 {#adding-product-profiles-for-existing-environments}

在2024年11月初之前建立的環境可能遺失上述章節所述的組織層級產品執行個體，以及某些產品設定檔。 現有的產品設定檔也將遺失服務切換。 建議更新這些產品設定檔，這是存取某些未來API的先決條件。

如果計畫中的一個或多個環境需要其產品設定檔更新，Cloud Manager將顯示以下通知。 請注意，環境必須是最新的AEM版本，才能更新其產品設定檔。

![更新產品設定檔](/help/onboarding/assets/modernize-product-profiles.png)

按一下&#x200B;**新增產品設定檔**&#x200B;按鈕將會開啟一個功能表，其中顯示將新產品設定檔新增到計畫或個別環境中所有可用環境的選項。

![取代環境](/help/onboarding/assets/choose-env-r.png)

按一下&#x200B;**所有環境**，將新的產品設定檔新增至方案中的所有環境。 或者，按一下「**個別環境**」以將產品設定檔新增至選取的環境；這會將使用者導覽至「環境」清單頁面，其中可從&#x200B;**更多選項**&#x200B;圖示選取&#x200B;**新增產品設定檔**&#x200B;動作。

![個別環境](/help/onboarding/assets/individual-environments.png)

您還可以將產品設定檔新增到選定的環境，方法是瀏覽到計畫總覽頁面的環境區段，按一下與環境對應的更多選項圖示，然後選擇新增產品設定檔。

在新產品設定檔被新增時，環境的狀態會顯示新增產品設定檔，並在流程完成時隨後顯示執行中。


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
