# Claude Code 專案基本架構模板（通用版）

適用於任何有明確產出物的專案：教材、文件、簡報、行銷企劃、資料報表，當然也包括程式。目標：讓 agent（一）持續記住規格、（二）有反思能力、（三）留下可供人學習的決策記錄。

## 心智模型

規格是**地圖**，實際的工作素材與限制是**疆域**，兩者的落差就是「未知」。模型本身無狀態，所有該被記住的東西都必須落在檔案裡、在對的時機被讀取。因此整個架構在回答三個問題——什麼該恆在（每次對話都載入）、什麼該按需（用到才載入）、什麼該定期蒸餾（從流水帳晉升為規則）。

```
專案根目錄/
├── CLAUDE.md                  ← 載入殼：只有一行 `@WORKFLOW.md`（既有專案只需追加這行）
├── WORKFLOW.md                ← 恆在層：行為規則（怎麼工作、怎麼記錄）
├── SPEC.md                    ← 恆在層：規格（唯一真相來源）
├── DECISIONS.md               ← 學習層：決策記錄（教學導向格式）
├── notes/
│   ├── workflow-guide.md      ← 本檔：模板使用指南
│   ├── implementation-notes.md ← 工作層：本輪工作筆記與偏離記錄
│   └── html-comment-layer.html ← 留言層片段：所有 HTML 產出直接內嵌
└── .claude/skills/
    ├── kickoff/SKILL.md       ← 開案：從粗略想法起草 SPEC.md 初稿
    ├── interview/SKILL.md     ← 動工前：問出「未知的已知」與模糊處
    ├── blindspot/SKILL.md     ← 動工前：掃描「未知的未知」＋領域速成教學
    ├── quiz/SKILL.md          ← 交付前：變更報告＋測驗（自己懂了沒）
    ├── pitch/SKILL.md         ← 交付時：懶人包／explainer（讓別人懂、要 buy-in）
    └── reflect/SKILL.md       ← 完工後：反思與記憶晉升
```

另有兩個使用者層 skill 配合這套流程：`kickoff`（同名的使用者層版本，會在空資料夾先建骨架再起草規格）與 `scout`（競品調查——kickoff 選方向時「業界怎麼解」還不知道，就插跑它）。

## 三個需求怎麼被滿足

**規格持續被記住**：SPEC.md 是唯一真相來源，WORKFLOW.md（經 CLAUDE.md 的 `@WORKFLOW.md` import 每次對話自動載入）強制 agent 每次開工先讀它、發現規格與現實衝突時先更新規格再改產出物。對話壓縮前先把未沉澱的決定寫進檔案（借 OpenClaw 的 memory flush 概念），規格就不會隨摘要蒸發。

**反思能力**：反思不在工作對話裡順手做，而是開新對話跑 `/reflect`——帶全新上下文的獨立輪次，避免產出者自評的確認偏誤。晉升有門檻：同類教訓出現兩次以上才寫進 WORKFLOW.md，一次性的留在筆記層（借 OpenClaw Dreaming 的晉升制，避免規則檔膨脹）。

**可學習的決策記錄**：DECISIONS.md 的格式是教學導向的——每筆不只記「決定了什麼」，還記「有哪些選項、為什麼選這個、下次你自己怎麼判斷」。這來自 Thariq 文章的 implementation-notes 模式（遇到計畫外狀況就選保守方案、記入偏離記錄、繼續前進），加上他的 quiz 模式：交付前先通過測驗，確認你真的理解這次的產出。

## HTML 作為輸出與互動介面

給人讀的長內容、給人操作的介面，一律用單一自包含 HTML 檔（存 `notes/`，隨反思一起歸檔）：kickoff 的方向比較頁、interview 的訪談問卷、blindspot 的領域講義、實作前的實作計畫頁、quiz 的互動測驗、pitch 的懶人包、reflect 的晉升檢核頁。三條紀律：（一）**互動迴路必須閉合**——agent 看不到瀏覽器裡的操作，每個互動頁都以「複製結果」按鈕收尾，把選擇變回文字貼回對話才算數；（二）**頁面照 ADHD 格式寫**——第一屏就是結論與下一步、多步驟編號、清單分組分層（不丟重要訊息）、細節收合；（三）**格式分工**——markdown 留給恆在層與需要版本比對的檔案（SPEC、WORKFLOW、DECISIONS），HTML 給人看與操作。（來源：Thariq〈The Unreasonable Effectiveness of HTML〉，claude.com/blog）

## 使用者視角：你實際要做的事

整個流程你只做五種動作：講想法、提問、做選擇、核可／否決、作答。

1. 開案（二選一）：裝了使用者層的 `kickoff` skill，就在空資料夾開 `claude` 直接說「我想做○○○」——骨架缺件會先自動建好，接著起草規格；或手動複製本模板資料夾再說「我想做○○○」。之後就是：回答起點問題、挑方向、逐節確認規格、核可。
2. 先說「訪談我」（一次答一題，答不出就說不知道），新領域再說「掃盲點」（讀速成教學＋學怎麼下指令）。熟領域可跳過掃盲點。
3. 說「開始做」→ 看本輪計畫前幾項、說 OK、放手。工作中它只為「待確認的未知」來找你。
4. 說「考我」→ 讀變更報告、作答、全對才交付；成果要給別人看就再說「pitch」，拿一份可分享的懶人包。
5. **開新對話**說「反思」→ 看晉升／刪除清單、同意或否決。這是唯一要記得換對話的一步。
6. 平時想學習就翻 DECISIONS.md；quiz 答錯的題目對應的決策條目要重點看。

## 建議工作循環

1. **開案**：帶著粗略想法跑 `/kickoff`——agent 探索素材、腦力激盪範圍選項、起草 SPEC.md 初稿（含未知清單），你只負責反應與修改。做法未定、想看業界怎麼解時插跑 `/scout`。
2. **動工前**：先跑 `/interview` 逐題釐清模糊處，再跑 `/blindspot` 掃出沒想到的面向，答案都回填 SPEC.md；agent 從規格推導本輪計畫（大輪次做成 HTML 實作計畫頁），你核可才動工。
3. **工作中**：agent 自動維護 notes/implementation-notes.md 與 DECISIONS.md。
4. **交付前**：跑 `/quiz`，產出變更報告＋測驗，全對才交付；要給別人看、要 buy-in 就接著跑 `/pitch`。
5. **交付後**：開新對話跑 `/reflect`——復盤、晉升規則、歸檔工作筆記。（順序不能顛倒：reflect 會歸檔筆記，quiz 需要讀它。）

進階選項：WORKFLOW.md 裡「壓縮前先沉澱」靠 agent 自覺，若要硬性保證，可在 Claude Code 設定 PreCompact hook 強制觸發。

## 來源

架構整合自：Thariq《A Field Guide to Claude Fable 5: Finding Your Unknowns》（claude.com/blog，本模板的 blindspot／interview／實作計畫／implementation-notes／pitch／quiz 全部對應該文的 unknowns 模式）、OpenClaw 的 memory flush 與 Dreaming 晉升制、Hermes 的技能固化與容量紀律。
