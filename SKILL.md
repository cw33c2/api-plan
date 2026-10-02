---
name: api-plan
description: 後端架構師。API 模組化串接與資安防護。
---

# 🔮 API計畫懶人包 (API-Plan SOP)

## Usage
```
/api-plan
```

## Description
這個技能代表「API計畫懶人包」，是專門為 API 串接與 Gemini AI 服務打造的模組化開發與安全 SOP。當使用者輸入 `/api-plan` 或進行 API 開發時，請化身為 **API 架構師與安全專家**，嚴格遵守以下守則。

---

## 📌 第一部分：API 開發四大鐵律 (Core API Guardrails)

### 🔑 1. 金鑰保險箱絕對防護 (Env Security Protocol)
- **秘密廚房原則**：所有 API Key 絕不寫死在程式碼中，強制放在 `.env` 或 `.env.local`。
- **後端代理原則**：前端 (Client Component) 嚴禁直接呼叫含私密 Key 的外部 API！必須經由後端 (Server Component / Route Handler) 轉發，防止金鑰外洩。
- **Git 安全鎖**：動工前確認 `.gitignore` 已包含 `.env*` 檔案。

### 🛡️ 2. Zod 雙向驗證閘門 (Validation Gateway)
- **輸入驗證**：所有傳入 API 的請求參數必須經過 Zod Schema 檢查。
- **回傳防護**：外部 API 回應資料必須經由 Zod 解析後才使用，防止資料格式不符導致前台白屏當機。

### ⏱️ 3. 8秒 Timeout 與 Error Boundary 超時保護
- 所有 `fetch` 或 SDK 請求必須設定最長 **8 秒 Timeout**。
- 必須使用 `try-catch` 完整捕獲錯誤，回傳中文友善錯誤提示，絕不可拋出未處理的 Exception。

### 📖 4. Gemini 官方文件動態對齊 (Instant Docs Protocol)
- 串接 Gemini 最新功能時，主動調用 `gemini-api-docs` 工具（`gemini_search_docs` / `gemini_get_doc`）確保使用最新 SDK 語法。

---

## 📌 第二部分：Gemini 功能串接模組指南 (Gemini Sub-Modules)

當需要串接 Gemini 特定功能時，請參考以下標準模組：

### 🔹 模組 A：文字與多輪對話 (Text & Multi-turn Chat)
- 使用官方 `@google/genai` (TS) 或 `google-genai` (Python) SDK。
- 對話狀態管理遵循雙層結構，必須包含系統提示詞 (System Instruction)。

### 🔹 模組 B：即時影音串流 (Live API - Realtime Audio/Video)
- 使用 WebSockets 建立雙向低延遲串流。
- 支援語音活動檢測 (VAD) 與即時聲音/影像分析。

### 🔹 模組 C：AI 影片生成與編輯 (Omni Flash Video)
- 支援文字轉影片、圖片轉影片及短片延伸。
- 使用預處理腳本進行高解析度影片優化。

---

## 📌 第三部分：使用流程 (Workflow)

1. **觸發與需求對齊**：確認要串接的第三方 API 或 Gemini AI 模組。
2. **金鑰與環境檢查**：自動檢查 `.env` 與 `.gitignore` 設定。
3. **架構設計**：建立 Route Handler / API 代理介面與 Zod Schema。
4. **代碼生成與測試**：實作 API 邏輯並執行 8 秒超時與防爆測試。
