<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

[English](./README.md) | **繁體中文** | [简体中文](./README.zh-CN.md)

# 給真正工程師的 Skills

> **Fork 變更說明（lp1688/skills）**——本 fork 在 [mattpocock/skills](https://github.com/mattpocock/skills) 之上的修改：
>
> - `kimi.plugin.json`：本 repo 現在可作為 **Kimi Code plugin** 安裝（`/plugins install https://github.com/lp1688/skills`），收錄 `skills/engineering/` 與 `skills/productivity/` 共 25 個正式 skills。已驗證 skill frontmatter（`name`、`description`、`disable-model-invocation`）與 Kimi Code 的 skill 載入器相容。
> - `README.zh-TW.md` / `README.zh-CN.md`：本 README 的繁體中文與簡體中文譯本。
> - `skills-report.html`：涵蓋全部 35 個 skill（engineering / productivity / misc / in-progress 四個 bucket）的中文視覺化分析報告。

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

這是我每天用来做真正工程開發的 agent skills——不是 vibe coding。

開發真正的應用程式很難。GSD、BMAD、Spec-Kit 這類方法試圖透過「接管整個流程」來幫忙，但這麼做的同時，它們也奪走了你的掌控權，而且流程中一旦出錯就很難排除。

這些 skills 的設計目標是小巧、容易調整、可組合。它們適用於任何模型，背後是數十年的工程經驗。盡情改造它們，變成你自己的東西。Enjoy。

如果你想追蹤這些 skills 的更新、以及我未來新增的技能，可以加入我的電子報，與約 60,000 位開發者一起：

[訂閱電子報](https://www.aihero.dev/s/skills-newsletter)

## 安裝（30 秒完成）

兩種安裝方式，兩種哲學。**[Claude Code plugin](https://code.claude.com/docs/en/plugins)** 把整套 skills 安裝為受管理的唯讀套件，我發布更新時你就會收到——你是訂閱，而不是 fork。**[skills.sh](https://skills.sh/mattpocock/skills)** 則把可編輯的 skill 檔案複製進你的專案，讓你可以動手改造、據為己有。二選一——兩個都裝會讓每個 skill 出現兩次。

### 1. 取得 skills

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugins install mattpocock-skills
```

或者，在 session 內：

```
/plugin install mattpocock-skills
```

它已在 Claude Code 官方 marketplace 中，不需要先加入任何東西，更新會自動送達。

</details>

<details>
<summary><strong>Kimi Code</strong></summary>

本 repo 同時也是一個 Kimi Code plugin（見 `kimi.plugin.json`）。在 Kimi Code session 中輸入：

```
/plugins install https://github.com/lp1688/skills
```

然後執行 `/reload`（或開新 session）即可啟用。Plugin 收錄 `skills/engineering/` 與 `skills/productivity/` 的正式 skills；可用 `/skill:<名稱>` 手動觸發，或讓模型依情境自動取用。之後可用 `/plugins list`、`/plugins info mattpocock-skills` 或 `/plugins remove mattpocock-skills` 管理。

</details>

<details>
<summary><strong>Codex 與其他 agents</strong></summary>

```bash
npx skills@latest add mattpocock/skills
```

挑選你想要的 skills，以及要安裝到哪些 coding agents。**安裝器讓你自由選擇要哪些 skills——請務必勾選 `setup-matt-pocock-skills`。**

原生 Codex plugin 已在 roadmap 上——詳見 [`.agents/adr/0002-ship-as-a-claude-code-plugin.md`](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)。

</details>

<details>
<summary><strong>給愛動手改造的人</strong></summary>

在任何 agent 上使用同一個安裝器——包括 Claude Code：

```bash
npx skills@latest add mattpocock/skills
```

它會把 skills 以普通檔案的形式寫進你的 repo，歸你所有、可以編輯。沒有任何東西會在你背後偷偷更新；想要我的最新變更時，用 `npx skills update` 拉取即可。

</details>

### 2. 執行 `/setup-matt-pocock-skills`

在你的 agent 中，每個 repo 執行一次。它會：

- 問你想用哪個 issue tracker（GitHub、Linear，或本地檔案）
- 問你在分診（triage）tickets 時使用哪些標籤（`/triage` 依賴標籤運作）
- 問你想把我們產生的文件存放在哪裡

### 3. 搞定——可以開始用了。

## 這些 Skills 為什麼存在

我打造這些 skills，是為了修掉我在 Claude Code、Codex 和其他 coding agents 身上常見的失敗模式。

### #1：Agent 做的不是我想要的

> 「沒有人確切知道自己要什麼。」
>
> David Thomas & Andrew Hunt，《[The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》

**問題**：軟體開發中最常見的失敗模式是認知落差（misalignment）。你以為開發者懂你要什麼，直到你看到他做出來的東西——才發現他完全誤解了你。

AI 時代也一樣。你和 agent 之間存在溝通落差。解法是 **grilling session（連番追問）**——讓 agent 針對你要做的東西，向你提出詳細的問題。

**解法**是使用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md)——非程式碼用途
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)——與 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 相同，但多了更多好東西（見下文）

這是我最熱門的 skills。它們幫你在動手之前先與 agent 對齊，並深入思考你要做的變更。**每次**要做變更時都該用它們。

### #2：Agent 太囉嗦了

> 有了統一語言（ubiquitous language），開發者之間的對話與程式碼的表達，都衍生自同一個領域模型。
>
> Eric Evans，《[Domain-Driven-Design](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)》

**問題**：在專案初期，開發者與軟體的服務對象（領域專家）通常說的是不同的語言。

我和我的 agents 之間也感受到同樣的張力。Agent 通常被丟進一個專案，被要求邊做邊摸索術語，於是它用 20 個字表達 1 個字就夠的東西。

**解法**是建立共享語言：一份幫助 agent 解讀專案術語的文件。

<details>
<summary>範例</summary>

這是來自我的 `course-video-manager` repo 的 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 範例。哪一種比較好讀？

- **之前**：「當課程某個 section 裡的一堂課被『實體化』（也就是在檔案系統中取得一個位置）時會出問題」
- **之後**：「materialization cascade（實體化連鎖）有問題」

這種簡潔，在每一個 session 都持續帶來回報。

</details>

這已內建於 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)。它是一場 grilling session，但同時幫你與 AI 建立共享語言，並把難以解釋的決策記錄在 ADR 中。

很難用言語形容這有多強大——它可能是這個 repo 裡最酷的技巧。試試看就知道了。

> [!TIP]
> 共享語言的好處不只是減少囉嗦：
>
> - **變數、函式與檔案的命名更一致**，都使用共享語言
> - 因此 **codebase 對 agent 來說更容易導航**
> - Agent 也**花更少 tokens 在思考上**，因為它能使用更精簡的語言

### #3：程式碼不能動

> 「永遠採取小而審慎的步驟。回饋的速度就是你的速限。永遠不要接下太大的任務。」
>
> David Thomas & Andrew Hunt，《[The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》

**問題**：假設你和 agent 已經對齊了要做什麼，但 agent *還是*產出垃圾，怎麼辦？

該檢視你的回饋迴圈（feedback loops）了。如果得不到「程式碼實際跑起來如何」的回饋，agent 就是在盲飛。

**解法**：你需要那一整套常見的回饋迴圈：靜態型別、瀏覽器存取、自動化測試。

在自動化測試方面，red-green-refactor 迴圈至關重要：agent 先寫一個會失敗的測試，然後修好它。這能給 agent 穩定的回饋水準，產出好得多的程式碼。

我做了一個可以插進任何專案的 **[`/tdd`](./skills/engineering/tdd/SKILL.md) skill**。它鼓勵 red-green-refactor，並給 agent 大量關於好測試與壞測試的指引。

在除錯方面，我也做了 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** skill，把除錯最佳實踐包裝成一個按階段把關的紀律化迴圈。

### #4：我們造出了一團泥球（Ball Of Mud）

> 「*每天*都要投資在系統的設計上。」
>
> Kent Beck，《[Extreme Programming Explained](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)》

> 「最好的模組是深的（deep）。它們讓大量功能透過一個簡單的介面被取用。」
>
> John Ousterhout，《[A Philosophy Of Software Design](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)》

**問題**：大多數用 agent 做出來的 app 都很複雜、難以修改。因為 agent 能大幅加速寫程式，它們也同時加速了軟體熵（entropy）。Codebase 正以前所未有的速度變得更複雜。

**解法**是一種激进的 AI 開發新路線：在乎程式碼的設計。

這個理念內建於這些 skills 的每一層：

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 在產生 spec 之前，會先拷問你這次會動到哪些模組

而最關鍵的是 [`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md)：它掃描 codebase 找出 deepening（加深模組）的機會，並把候選清單交給你。我建議每隔幾天就在你的 codebase 上跑一次。它是一場體檢，不是急救：在真正老舊的 codebase 上它會找到真實的候選，但它不會幫你把泥球解開。

### 總結

軟體工程基本功比以往任何時候都更重要。這些 skills 是我把這些基本功濃縮成可重複實踐方式的最大努力，希望能幫你交付職業生涯中最好的 app。Enjoy。

## 技能一覽

這些 skills 沿著一個軸線區分——誰可以觸發它們。**User-invoked** skills 只有你親自輸入時才能觸發（例如 `/grill-me`）；它們的職責是編排（orchestrate）。**Model-invoked** skills 可以由你觸發，也可以在任務相符時由 agent 自動取用；它們承載的是可重複使用的紀律。User-invoked skill 可以調用 model-invoked skills，但絕不會調用另一個 user-invoked skill。

### Engineering

我每天寫程式使用的 skills。

**User-invoked**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)** — 詢問哪個 skill 或 flow 適合你的情況。這是整個 repo 中 user-invoked skills 的路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)** — Grilling session，同時建立專案的領域模型：磨利術語，並就地更新 `CONTEXT.md` 與 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)** — 讓 issues 在一個由分診角色組成的狀態機中流轉。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)** — 掃描 codebase 找出 deepening 機會，以視覺化 HTML 報告呈現，然後針對你挑選的候選進行 grilling。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)** — 為 engineering skills 設定此 repo（issue tracker、triage 標籤、domain 文件布局）。使用其他 engineering skills 前，每個 repo 先執行一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)** — 把目前的對話轉化成 spec 並發佈到 issue tracker。不做訪談——只綜合你們已經討論過的內容。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)** — 把任何計畫、spec 或對話拆解成一組 tracer-bullet tickets，每張都宣告自己的 blocking 依賴——本地檔案以文字書寫，真正的 tracker 則用原生 blocking 連結。
- **[implement](./skills/engineering/implement/SKILL.md)** — 依據 spec 或一組 tickets 建置工作，在預先約定的 seams 驅動 `/tdd`，commit 前以 `/code-review` 收尾。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)** — 把一大塊超出單一 agent session 容量的工作，規劃成 issue tracker 上由 decision tickets 組成的共享地圖——一次解決一張，直到通往目的地的路清晰為止。

**Model-invoked**

- **[prototype](./skills/engineering/prototype/SKILL.md)** — 打造一次性 prototype 來回答設計問題——狀態/邏輯問題產出單一可分享的 HTML 檔，UI 問題產出數個從同一路由切換的、截然不同的 UI 變體。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)** — 針對難 bug 與效能退化的紀律化診斷迴圈：建立一條會對此 bug 變紅的回饋迴圈 → 最小化 → 提出假設 → 插樁 → 修復 → 回歸測試。
- **[research](./skills/engineering/research/SKILL.md)** — 以背景 agent 的形式，針對問題查證高信任度的一手來源，並把發現整理成附引用的 Markdown 檔存進 repo。
- **[tdd](./skills/engineering/tdd/SKILL.md)** — 採用 red-green-refactor 迴圈的測試驅動開發。一次一個垂直切片地建功能或修 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)** — 主動建立並磨利專案的領域模型——對照 glossary 挑戰術語、用邊界情境壓力測試，並就地更新 `CONTEXT.md` 與 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)** — 設計 deep modules 的共享紀律與詞彙：大量行為藏在小介面後面、位於乾淨的 seam 上、可透過介面測試。
- **[code-review](./skills/engineering/code-review/SKILL.md)** — 對某固定點以來的 diff 做雙軸審查：**Standards**（是否符合 repo 的編碼標準，外加 Fowler 壞味道基線？）與 **Spec**（是否忠實實作原始 issue/spec？），以併行 sub-agents 執行，互不污染。
- **[resolving-merge-conflicts](./skills/engineering/resolving-merge-conflicts/SKILL.md)** — 逐 hunk 處理進行中的 git merge 或 rebase 衝突，透過追溯雙方一手來源中的意圖來解決，然後完成整個操作——絕不 `--abort`。
- **[wizard](./skills/engineering/wizard/SKILL.md)** — 產生互動式 bash wizard，帶著人類完成只有人類能做的步驟：開通基礎設施、設定憑證或 CI secrets、操作陌生的第三方 dashboard，或執行一次性 migration / cutover。

### Productivity

一般工作流程工具，非程式碼專屬。

**User-invoked**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)** — 針對計畫或設計接受無情的訪談，直到設計樹的每個分支都被解決。
- **[handoff](./skills/productivity/handoff/SKILL.md)** — 把目前的對話壓縮成交接文件，讓另一個 agent 能接續工作。
- **[teach](./skills/productivity/teach/SKILL.md)** — 跨多個 session 教使用者學會新技能或概念，以目前目錄作為有狀態的教學 workspace。
- **[to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md)** — 把你獨自無法回答的決策，轉化成給「唯一能回答的人」的 Markdown 問卷——非同步填寫，或在會議中一起填。它拷問的是「寄送」（寄給誰、需要拿回什麼），而非主題本身。
- **[wait-what](./skills/productivity/wait-what/SKILL.md)** — 在訊息看不懂的當下立刻觸發。Agent 會用白話英文、補上你缺的上下文，並使用你 `CONTEXT.md` 中的詞彙重新說明。

**Model-invoked**

- **[grilling](./skills/productivity/grilling/SKILL.md)** — 針對計畫、決策或想法無情地訪談使用者，直到設計樹的每個分支都被解決。這是 `grill-me`、`grill-with-docs`、`triage`、`wayfinder` 與 `improve-codebase-architecture` 背後可重複使用的訪談 primitive。
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)** — 撰寫給 agent 看的文件：skills、AGENTS.md/CLAUDE.md，以及任何 agent 經由 pointer 觸達的文件。
