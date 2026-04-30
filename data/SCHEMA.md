# W11–W15 教材 JSON Schema

**給陪讀看的**：請照這份格式，從 PDF 提取 W11–W15 的教材內容，輸出成 JSON 檔案。  
輸出檔案路徑：`PKA/Projects/他加祿語學習/data/w11-15.json`

---

## 頂層結構

```json
{
  "vocab": [...],
  "dialogues": [...],
  "grammar": [...],
  "exercises": [...]
}
```

---

## 1. vocab（單字列表）

每個單字一個物件，放進 `vocab` 陣列。

```json
{
  "id": 500,
  "wk": 11,
  "tl": "Kailangan",
  "zh": "需要／必須",
  "en": "Need / Must",
  "reading": "凱拉安",
  "cat": "w11_15",
  "hint": "凱拉安需要幫忙",
  "ex": {
    "tl": "Kailangan ko ng kape.",
    "cn": "我需要咖啡。"
  }
}
```

| 欄位 | 型別 | 說明 |
|------|------|------|
| `id` | 數字 | W11 從 500 開始、W12 從 560 開始、W13 從 620 開始、W14 從 680 開始、W15 從 740 開始（每週留 60 個空位）|
| `wk` | 數字 | 週次，11 到 15 |
| `tl` | 字串 | 他加祿語單字或片語 |
| `zh` | 字串 | 中文意思 |
| `en` | 字串 | 英文意思（可省略，留空字串 `""`） |
| `reading` | 字串 | 中文諧音（用台灣國語近似音） |
| `cat` | 字串 | 分類，一律填 `"w11_15"`（工程師會處理） |
| `hint` | 字串 | 記憶口訣，越好記越好（例：「凱拉安≈你需要我的安慰」） |
| `ex.tl` | 字串 | 他加祿語例句 |
| `ex.cn` | 字串 | 例句中文翻譯 |

**注意**：現有 W1-10 已有 ID 1–428，W11-15 的 ID 從 500 開始，不要重複。

---

## 2. dialogues（對話練習）

每個完整對話一個物件，放進 `dialogues` 陣列。

```json
{
  "wk": 11,
  "week_key": "w11",
  "title": "W11 傳道對話 — 需要聖靈幫助",
  "context": "傳道時遇到菲律賓朋友，練習用 Kailangan 表達需要",
  "lines": [
    {
      "speaker": "A",
      "tl": "Hello. Kamusta ka?",
      "cn": "你好。你好嗎？"
    },
    {
      "speaker": "B",
      "tl": "Mabuti naman.",
      "cn": "我很好。"
    }
  ]
}
```

| 欄位 | 說明 |
|------|------|
| `wk` | 週次數字 |
| `week_key` | 篩選用 key，格式 `"w11"` 到 `"w15"` |
| `title` | 對話標題（含週次） |
| `context` | 情境說明（一句話，讓學習者知道這個對話的背景） |
| `lines` | 對話行陣列 |
| `lines[].speaker` | `"A"`（傳道者）或 `"B"`（屋主或朋友）|
| `lines[].tl` | 他加祿語台詞 |
| `lines[].cn` | 中文翻譯 |

**注意**：
- 每週至少 1 個主要傳道對話
- 如果 PDF 有多個對話，每個單獨放一個物件
- 說話者請用 A/B（A = 傳道者，B = 對方）

---

## 3. grammar（文法重點）

每週的文法重點卡，放進 `grammar` 陣列。

```json
{
  "wk": 11,
  "keyword": "Kailangan",
  "reading": "凱拉安",
  "meaning": "需要 / 必須",
  "mnemonic": "凱拉安你需要安慰",
  "formulas": [
    "需要東西：Kailangan + 所有格 + ng + 東西",
    "需要做事：Kailangan + 所有格+ng + 動詞"
  ],
  "examples": [
    { "tl": "Kailangan ko ng kape.", "cn": "我需要咖啡。" },
    { "tl": "Kailangan kong kumain.", "cn": "我需要吃。" }
  ],
  "tip": "Kailangan=實際需要；Dapat=道義應該；Gusto=想要偏好",
  "table": {
    "headers": ["用法", "Tagalog", "中文"],
    "rows": [
      ["需要東西", "Kailangan ko ng kape.", "我需要咖啡"],
      ["需要做事", "Kailangan kong kumain.", "我需要吃"],
      ["被需要", "Kailangan ako.", "需要我"]
    ]
  }
}
```

| 欄位 | 必填 | 說明 |
|------|------|------|
| `wk` | ✅ | 週次 |
| `keyword` | ✅ | 核心文法詞（例：`"Kailangan"`） |
| `reading` | ✅ | 中文諧音 |
| `meaning` | ✅ | 一句話解釋 |
| `mnemonic` | ✅ | 記憶口訣 |
| `formulas` | ✅ | 句型公式（字串陣列，可以有多個） |
| `examples` | ✅ | 例句陣列（至少 2 個） |
| `tip` | ✅ | 學習小提示（通常是跟近似詞比較） |
| `table` | ❌ | 比較表（有的話加，沒有可省略）|

---

## 4. exercises（填空練習）

每週的填空題組，放進 `exercises` 陣列。

```json
{
  "wk": 11,
  "key": "w11_kailangan",
  "label": "W11 Kailangan",
  "items": [
    {
      "s": "「我需要咖啡」Tagalog？",
      "b": "Kailangan ko ng kape.",
      "h": "Kailangan+所有格+ng+東西",
      "zh": "W11：需要東西",
      "c": [
        "Kailangan ako ng kape.",
        "Kailangan ko ng kape.",
        "Kailangan kong kape.",
        "Gusto ko ng kape."
      ]
    }
  ]
}
```

| 欄位 | 說明 |
|------|------|
| `wk` | 週次 |
| `key` | 唯一識別碼，格式：`w11_keyword`（全小寫，底線分隔）|
| `label` | 顯示名稱，例 `"W11 Kailangan"` |
| `items` | 題目陣列（建議每週至少 4 題，最多 8 題）|
| `items[].s` | 題目（中文問句或有 `___` 的填空句）|
| `items[].b` | 正確答案 |
| `items[].h` | 提示（簡短，幫助理解為什麼是這個答案）|
| `items[].zh` | 中文解釋（標示週次和重點）|
| `items[].c` | 4 個選項的陣列（正確答案必須在其中，順序可以亂）|

---

## 完整輸出範例

```json
{
  "vocab": [
    {
      "id": 500,
      "wk": 11,
      "tl": "Kailangan",
      "zh": "需要／必須",
      "en": "Need / Must",
      "reading": "凱拉安",
      "cat": "w11_15",
      "hint": "凱拉安你需要幫忙",
      "ex": { "tl": "Kailangan ko ng kape.", "cn": "我需要咖啡。" }
    }
  ],
  "dialogues": [
    {
      "wk": 11,
      "week_key": "w11",
      "title": "W11 傳道對話",
      "context": "練習用 Kailangan 表達需要",
      "lines": [
        { "speaker": "A", "tl": "Hello.", "cn": "你好。" }
      ]
    }
  ],
  "grammar": [
    {
      "wk": 11,
      "keyword": "Kailangan",
      "reading": "凱拉安",
      "meaning": "需要 / 必須",
      "mnemonic": "凱拉安你需要安慰",
      "formulas": ["Kailangan + 所有格 + ng + 東西"],
      "examples": [
        { "tl": "Kailangan ko ng kape.", "cn": "我需要咖啡。" }
      ],
      "tip": "Kailangan=需要；Dapat=應該；Gusto=想要"
    }
  ],
  "exercises": [
    {
      "wk": 11,
      "key": "w11_kailangan",
      "label": "W11 Kailangan",
      "items": [
        {
          "s": "「我需要咖啡」Tagalog？",
          "b": "Kailangan ko ng kape.",
          "h": "Kailangan+所有格+ng+東西",
          "zh": "W11：需要東西",
          "c": [
            "Kailangan ako ng kape.",
            "Kailangan ko ng kape.",
            "Kailangan kong kape.",
            "Gusto ko ng kape."
          ]
        }
      ]
    }
  ]
}
```

---

## 每週要做的事（陪讀待辦）

| 週次 | 核心文法 | 預計 vocab 數 |
|------|----------|--------------|
| W11 | Kailangan（需要） | 10–15 個 |
| W12 | Kanino / Kailan（誰的 / 何時） | 10–15 個 |
| W13 | I-verb 受詞焦點 | 10–15 個 |
| W14 | Ma-verb 感受狀態 | 10–15 個 |
| W15 | -an verb 地點/受者焦點 | 10–15 個 |

全部輸出成一個檔案：`PKA/Projects/他加祿語學習/data/w11-15.json`

完成後通知工程師接進 PWA。

---

## 參考：現有 W11-15 單字（已在網頁）

工程師已把這些放進去了，陪讀可以補充、修正或新增。現有：

- W11：Kailangan kita、Upang、Sumulong、Matatag、Banal na espiritu、Tulong、Pagkain
- W12：Kanino、Kaninong、Kailanman、Asambleya
- W13：Ituro、Ibigay、Itinuturo、Kaligayahan、Hamon、Nagmamadali、Libreng pag-aaral
- W14：Makinig、Matulog、Maupo
- W15：Bigyan、Tulungan、Hugasan、Tract、Dormitory、Dalawin、Pampatibay-loob

**陪讀的任務**：從 PDF 提取**完整**詞彙（目前的清單可能不完整），特別是對話和文法公式部分。
