# Triple Synth

**Role Separation × Model-Specific Formatting × Multi-AI Synthesis**

A single HTML file that generates structured prompts for running multi-AI debates across ChatGPT, Claude, and Gemini — no API keys, no subscriptions, no installs.

[**→ Try it now**](https://Simmon-Gomi.github.io/triple-synth/) ·  [日本語版](https://Simmon-Gomi.github.io/triple-synth/ja/)

---

## The Problem

Many people now use multiple AIs on the same topic to compare outputs. This makes sense — every model has blind spots, and comparing reveals what any single model would miss.

But in practice, most comparisons stay at the surface: ask the same question three times, read the three answers, pick the one that "looks best." The problem is that all three models are optimizing for the same objective — give a helpful, balanced answer. So you get three polite, partially overlapping responses, each with its own hidden gaps, and no systematic way to find those gaps.

## The Approach

Triple Synth structures the comparison by separating it into distinct operations:

### Role Separation

Instead of asking the same question three times, assign each AI a different role:

- **Proposer** — Build the single strongest hypothesis with supporting evidence and a falsifiable prediction
- **Critic** — Actively find weaknesses, counterexamples, and blind spots. Propose alternatives. Do not agree easily
- **Judge** — Organize points of agreement and contention. Identify the most defensible conclusion and remaining open questions

This matters because the roles force each model to optimize for a different objective. A critic that is instructed not to agree easily will surface problems that a model trying to "give a good answer" would gloss over. A judge that is told not to decide by majority vote has to evaluate evidence quality instead of counting heads.

Roles are optional — you can set any or all models to "None" and use the tool as a simple multi-model prompt generator.

### Model-Specific Formatting

Each AI processes prompts differently. Claude responds well to XML-tagged structure (`<instructions>`, `<topic>`, `<output_format>`). ChatGPT works better with Markdown headers and numbered lists. Gemini performs best when context and background come before instructions.

Triple Synth generates the same logical content in three different formats, matched to each model. This isn't cosmetic — prompt format measurably affects output quality, especially for complex instructions.

### Dialectic vs. Synthesis

After collecting three responses, you have two distinct operations:

**Dialectic** ("find holes") — Identifies logical contradictions, missed risks, scope problems, and practicality issues across all three outputs. Prioritizes deletion over addition. Use this when the responses haven't converged yet or when you suspect unresolved problems.

**Synthesis** ("produce a final answer") — Integrates the three outputs into a single finished product, judging by evidence quality rather than majority vote. Use this when the debate has sufficiently converged.

These are deliberately separate because they are opposite cognitive operations. Dialectic is destructive analysis; synthesis is constructive integration. Mixing them produces muddy results.

### The Iteration Loop

The generated dialectic or synthesis prompt should be pasted into a **new chat session** of any AI — not the same session that produced one of the three responses. This prevents the previous role assignment from biasing the integration.

If the dialectic finds significant holes, revise and run another round. If it returns "no change needed," switch to synthesis. This loop converges toward a result that has survived structured cross-examination from multiple models.

## Why Copy-Paste Instead of API?

This is a deliberate design choice, not a limitation:

- **Zero setup** — No API keys, no Python, no tokens to manage. Open the HTML, start using it
- **Use each AI's full power** — ChatGPT's web browsing, Claude's extended thinking, Gemini's grounding — none of these work through third-party API wrappers
- **No additional cost** — Works with the subscriptions you already have
- **Your data stays in each provider's standard interface** — No third-party middleman

The target user is someone who already has ChatGPT, Claude, and Gemini open in separate tabs and is already comparing outputs manually. Triple Synth makes that existing workflow more structured — it does not replace it with a different system.

## Workflow

```
┌─────────────┐
│  Enter topic │
│  Assign roles│
└──────┬──────┘
       │  Generate prompt (×3)
       ▼
┌──────────────────────────────────┐
│  ChatGPT    Claude      Gemini   │
│  (Proposer) (Critic)    (Judge)  │
└──────┬─────────┬─────────┬──────┘
       │  Paste responses back
       ▼
┌─────────────────┐     ┌──────────────────┐
│   Synthesize    │ or  │    Dialectic      │
│  (final answer) │     │  (find holes →    │
│                 │     │   another round)  │
└─────────────────┘     └──────────────────┘
       │
       ▼  Paste into any AI's NEW chat
       │
       ▼  Repeat until converged
```

## Quick Start

**Option A: Use online** — Visit the [demo link](https://Simmon-Gomi.github.io/triple-synth/)

**Option B: Use locally** — Download `index.html`, open in any browser. That's it.

**On iPhone** — Open the URL in Safari → Share button → "Add to Home Screen"

## File Structure

```
triple-synth/
├── index.html      ← English version (default)
├── ja/
│   └── index.html  ← Japanese version
└── README.md
```

## License

MIT

---

# Triple Synth（日本語）

**役割分離 × モデル別形式 × マルチAI生成統合**

ChatGPT・Claude・Geminiの出力を比較・議論させるプロセスを構造化するツール。HTML1枚、API不要、サブスク不要。

[**→ 日本語版を使う**](https://simmon-gomi.github.io/triple-synth/ja/) · [English](https://simmon-gomi.github.io/triple-synth/)

## 何を解決するか

複数のAIに同じテーマを投げて比較する人は多い。どのモデルにも穴があるから比較するわけだが、実際には「同じ質問を3つに投げて、良さそうな方を選ぶ」にとどまっていることが多い。

この方法の問題は、3つのモデルが全て同じ目標——「良い回答を出す」——に対して最適化していること。結果として、それぞれが自分の穴を自覚しないまま、表面的に整った回答を出す。穴を見つけるには、穴を探す役割を明示的に与える必要がある。

## 3つの仕組み

### 役割分離

各AIに異なる役割を割り当てる：

- **提案者** — 最善の仮説を1つ提示し、根拠と反証可能な予測を述べる
- **反証者** — 弱点・反例・見落としを最大5点挙げる。安易に同意しない
- **裁定者** — 合意点と争点を整理し、現時点で最も妥当な結論と未確定点をまとめる

役割を分けることで、各モデルの最適化目標が変わる。反証者に「安易に同意するな」と指示すれば、通常なら「ただし～にも注意が必要です」程度で済ませる問題点を明示的に掘り出す。裁定者に「多数決で決めるな」と指示すれば、根拠の質で判断せざるを得なくなる。

役割はオプション。全て「なし」にすれば、単純なマルチモデルプロンプト生成器として使える。

### モデル別形式

同じ論理的内容を、AIごとに異なる形式で生成する。ClaudeにはXMLタグ構造（`<instructions>`、`<topic>`、`<output_format>`）、ChatGPTにはMarkdown見出しと番号リスト、Geminiにはコンテキスト先行の構成。

これは見た目の問題ではない。プロンプトの形式は、特に複雑な指示において、出力の質に実測可能な影響がある。

### 弁証と統合

3つの回答を集めた後、2つの異なる操作がある：

**弁証**（穴を探す）— 3つの出力にまたがる論理矛盾・リスク見落とし・範囲の過不足・実用性の問題を特定する。追加より削除を優先する。回答がまだ収束していない時に使う。

**統合**（完成品を作る）— 3つの出力を、多数決ではなく根拠の質で判断して1つの完成品に統合する。議論が十分に収束した時に使う。

この2つを意図的に分離しているのは、破壊的分析（穴を探す）と構成的統合（まとめる）が逆方向の操作だから。混ぜると中途半端な結果になる。

### 反復ループ

生成された弁証・統合プロンプトは、3つの回答を出したチャットではなく、任意のAIの**新規チャット**に貼る。前の役割（提案者/反証者/裁定者）のバイアスが残ったまま統合すると、判断が歪む。

弁証で「要改訂」が出たら修正してもう1ラウンド。「変更不要」が出たら統合に切り替える。複数モデルによる構造化された交差検証を経て収束した結果が得られる。

## なぜAPIではなくコピペか

制約ではなく設計上の選択：

- **セットアップ不要** — APIキーもPythonもトークン管理も不要。HTMLを開くだけ
- **各AIの全機能を使える** — ChatGPTのWeb検索、Claudeの拡張思考、Geminiのグラウンディング。API経由では動かない機能がそのまま使える
- **追加コスト0** — 既に持っているサブスクだけで動く
- **データが外部に出ない** — 各社の正規チャットUIで完結。第三者を経由しない

想定ユーザーは、既にChatGPT・Claude・Geminiを別タブで開いて手動で比較している人。Triple Synthはその既存のワークフローを構造化する——別のシステムに置き換えるのではない。

## 使い方

1. ブラウザでページを開く
2. テーマを入力、役割を選ぶ
3. 各ボタンでプロンプト生成 → 自動コピーされる
4. 各AIのチャットに貼り付けて回答を得る
5. 回答を貼り戻す
6. 「弁証」で穴を探す or「統合」で完成品を作る → 生成されたプロンプトを任意のAIの**新規チャット**に貼る
7. 納得いくまで繰り返す

## iPhoneで使う

SafariでURLを開く → 共有ボタン（□↑）→「ホーム画面に追加」
