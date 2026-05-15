---
title: 使用通用編輯器建立表單
description: 使用最適化Forms運算式來新增自動驗證、計算，並開啟或關閉區段的可見度。
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 67%

---

# 使用通用編輯器建立表單

使用通用編輯器建立下列表單。 此表單有3個下拉式清單，其值將使用API整合填入
![最適化表單](assets/address-form.png)

## 居住國家/地區

初始化時，居住國家/地區下拉式清單會填入 API 呼叫的結果。
![initialize-event](assets/initialize-event.png)

## 成功處理常式

成功處理常式的定義是使用 geonames 陣列中的適當值來設定國家/地區的列舉和列舉名稱下拉式清單。 地名陣列可在「事件裝載」選項下使用
![event-payload](assets/event-payload.png)
![success-handler](assets/success-handler.png)

## 擷取子值

使用者在居住國家/地區下拉式清單中進行選擇時，會填入州或省下拉式清單。 與所選國家/地區相關的 geonameId 會作為輸入參數，傳遞至 GetChildren API 整合

![get-children](assets/invoke-service-get-children.png)

已定義序列處理常式，以設定StateOrProvidle下拉式欄位的enum/enumNames
![get-children-success-handler](assets/child-success-handler.png)

已選取州或省份後，您可以按照上述用於填入州或省份的下拉式清單模式，來填入城市下拉式清單。