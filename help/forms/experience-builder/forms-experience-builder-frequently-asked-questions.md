---
title: Forms Experience Builder — 常見問題
description: 尋找有關Forms Experience Builder常見問題的解答，包括設定、使用、疑難排解和最佳作法。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: f43c2586-9075-47dc-aa45-5ed2d2979b6d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 2%

---

# Forms Experience Builder — 常見問題

>[!NOTE]
>
> Forms Experience Builder可透過搶先使用計畫取得。 開始之前，請確定您已提出要求並獲授存取權。

此常見問題集說明有關Forms Experience Builder的最常見問題，從基本設定到進階功能及疑難排解。

## 一般問題

### 什麼是Forms Experience Builder？

Forms Experience Builder是AI支援的表單建立工具，可讓您使用對話式語言建立複雜的數位表單。 您只需說明所要的內容，而不用傳統的拖放介面或複雜的編碼，AI會為您建立表單。

### 誰可以使用Forms Experience Builder？

Forms Experience Builder的設計用途為：

- **表單建立者**&#x200B;想要快速有效率地建立表單
- **需要建立表單而沒有技術專業知識的企業使用者**
- **想利用AI建立快速表單原型的**&#x200B;開發人員
- 需要設定及管理表單建立工作流程的&#x200B;**管理員**

### Forms Experience Builder是否適用於所有AEM Forms客戶？

Forms Experience Builder目前可透過搶先存取計畫使用。 請聯絡您的Adobe代表，請求存取權並瞭解您組織的可用性。

## 設定和組態

### 使用Forms Experience Builder的先決條件為何？

在使用Forms Experience Builder之前，請確定您擁有：

- 透過搶先存取計畫存取Forms Experience Builder
- AEM Forms as a Cloud Service搭配最適化Forms核心元件
- 基本瞭解表單概念與業務需求

如需詳細的技術設定需求，請參閱[部署和設定Forms Experience Builder](deploy-forms-experience-builder.md)。

### 如何在我的環境中啟用Forms Experience Builder？

Forms Experience Builder的設定取決於您的AEM Forms實作：

Edge Delivery Services的&#x200B;**：**

- 為Edge Delivery Services Forms準備專案
- 在通用編輯器中啟用Forms體驗產生器

**對於核心元件型表單：**

- 確認最適化Forms核心元件已啟用
- 在最適化Forms編輯器中設定Forms Experience Builder

### 我可以在現有表單中使用Forms Experience Builder嗎？

是的，Forms Experience Builder可以透過數種方式搭配現有表單使用：

- 匯入及轉換現有的PDF forms
- 使用AI支援的功能增強現有的最適化表單
- 將智慧型欄位新增至目前的表單結構

## 建立表單

### 如何建立我的第一個表單？

從您想要的簡單說明開始：

    建立包含名稱、電子郵件和訊息欄位的連絡人表單

AI將產生基本表單結構，然後您可以使用其他功能、驗證和樣式來增強此基本表單結構。

### 我可以建立哪些型別的表格？

Forms Experience Builder支援各種表單型別：

- 聯絡與意見回饋表單
- 註冊和入門表單
- 調查和評估表單
- 具有條件邏輯的多步驟表單
- Forms具有檔案上傳和複雜驗證

### 我可以建立多步驟表單嗎？

可以，您可以使用自然語言建立多步驟表單：

    建立包含3個步驟的漸進式表單：個人資訊、偏好設定、確認

AI會自動設定包含步驟間導覽的表單結構。

### 如何新增驗證至表單欄位？

使用自然語言命令新增驗證：

    使@email為具有電子郵件格式驗證的必要欄位
    將美國電話號碼格式驗證新增至@phoneNumber
    設定年齡驗證：@dateOfBirth
必須是18歲或以上

## 進階功能

### 什麼是LLM增強型智慧型欄位？

LLM增強型智慧型欄位是智慧型表單欄位，已預先填入AI知識庫中的相關選項。 例如：

- 包含全球各個國家/地區的國家/地區下拉式清單
- 使用標準程式碼的產業分類
- 包含州、市和郵遞區號的地理位置資料

### 如何將現有檔案匯入表單？

您可以匯入各種檔案型別：

- **PDF forms**：上傳靜態或互動式PDF
- **影像**：上傳紙本表格或熒幕擷圖的像片
- **設計檔案**：匯入Figma設計或其他設計格式

使用Forms Experience Builder中的附件圖示可上傳您的檔案並說明您的轉換需求。

### 我可以整合表單與外部系統嗎？

是的，Forms Experience Builder支援多種整合選項：

- 使用自訂範本提交電子郵件
- REST API與外部服務整合
- 雲端儲存整合(Azure、AWS、Google Cloud)
- 工作流程整合(Power Automate、AEM工作流程)

## 疑難排解

### AI不理解我的請求。 我應該怎麼做？

嘗試下列方法：

- 在說明中更加具體
- 將複雜的請求分解成小步驟
- 使用欄位參考(@fieldName)進行目標變更
- 提供您想要的明確範例

### 我的表單驗證無法運作。 該如何修正？

檢查這些常見問題：

- 驗證欄位名稱是否完全相符（區分大小寫）
- 請確認驗證語法正確
- 個別測試驗證規則
- 檢閱特定問題的錯誤訊息

### 條件邏輯未正確觸發。 有什麼問題嗎？

疑難排解條件式邏輯，方法如下：

- 確保欄位名稱正確參照
- 檢查規則語法和條件
- 使用不同的輸入組合進行測試
- 驗證欄位型別是否符合規則要求

### 介面未載入。 我應該怎麼做？

請嘗試下列解決方案：

- 重新整理瀏覽器並清除快取
- 檢查網際網路連線
- 確認您擁有適當的存取許可權
- 如果問題仍然存在，請聯絡您的系統管理員

## 最佳做法

### 如何使用Forms Experience Builder建立更好的表單？

請遵循下列最佳實務：

- **明確**：提供您想要的詳細描述
- **從簡單開始**：從基本結構開始，逐步增加複雜性
- **徹底測試**：在部署之前驗證所有表單功能
- **使用增量開發**：逐步建置表單

### 建立表單時應該避免什麼？

請避免下列常見錯誤：

- 在您的說明中過於模糊
- 嘗試一次建立所有內容
- 略過測試和驗證
- 未考量行動回應

### 如何確保我的表單可供存取？

Forms Experience Builder包含協助工具功能：

- 自動WCAG相容性檢查
- 熒幕助讀程式相容性
- 鍵盤導覽支援
- 高對比模式選項

## 整合與部署

### 如何部署使用Forms Experience Builder建立的表單？

使用Forms Experience Builder建立的Forms會遵循標準AEM Forms部署流程：

- 透過AEM作者環境發佈表單
- 設定表單提交端點
- 設定表單處理工作流程
- 在生產環境中測試表單

### 我可以自訂AI回應和行為嗎？

可以，您可以設定各種層面：

- 回應樣式（簡明、詳細、平衡）
- 語言偏好設定和術語
- 介面自訂選項
- 協助工具設定

### 如何取得Forms Experience Builder的協助？

如需其他支援：

- 檢視[快速入門手冊](forms-experience-builder-getting-started.md)
- 檢閱[部署與設定指南](deploy-forms-experience-builder.md)
- 請連絡您的系統管理員
- 如需技術問題，請聯絡Adobe支援

## 相關的文章

- [Forms Experience Builder概述](product-overview.md)
- [表單體驗建立工具快速入門](forms-experience-builder-getting-started.md)
- [部署和設定表單體驗建立工具](deploy-forms-experience-builder.md)
- [LLM增強型智慧型欄位](forms-experience-builder-llm-smart-fields.md)
- [智慧型匯入和轉換](intelligent-import-conversion.md)
- [表單提交與整合](form-submission-integration.md)
