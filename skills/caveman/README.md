# caveman

**why use many token when few do trick**

A skill that makes AI coding agents respond in compressed caveman-style prose — cutting ~65% of output tokens while keeping full technical accuracy.

## Install

```bash
tessl install juliusbrussee/caveman
```

Works with Claude Code, Cursor, Codex, Gemini, Copilot, and more.

## Before / After

**Normal Claude** (69 tokens):
> "The reason your React component is re-rendering is likely because you're creating a new object reference on each render cycle. When you pass an inline object as a prop, React's shallow comparison sees it as a different object every time, which triggers a re-render. I'd recommend using useMemo to memoize the object."

**Caveman Claude** (19 tokens):
> "New object ref each render. Inline object prop = new ref = re-render. Wrap in `useMemo`."

Same fix. 75% less word. Brain still big.

## Intensity levels

- **Lite** — terse professional. Drop filler, keep articles.
- **Full** (default) — caveman. Fragment sentences, drop articles, compress all.
- **Ultra** — maximum compression. Abbreviate everything.
- **文言文** — classical Chinese compression. Three variants: lite, full, ultra.

Switch anytime with `/caveman lite`, `/caveman ultra`, etc.

## Benchmarks and evals

### Same quality — same brain

38 [Tessl task eval](https://docs.tessl.io/evaluate/evaluate-skill-quality-using-scenarios) scenarios test whether caveman degrades technical correctness: 35 coding problems across 10 languages (JS, TS, Python, Go, Rust, Java, CSS, SQL, HCL, YAML) + 3 negative cases. Each scored against weighted technical checklists — zero style points, only facts.

19 independent runs across 4 agents:

| Agent | Runs | Baseline | Caveman | Delta |
|-------|------|----------|---------|-------|
| Claude Sonnet 4.6 | 10 | 97.6% | 96.5% | -1.1 |
| Cursor Composer 2 | 3 | 97.7% | 96.7% | -1.0 |
| Codex GPT-5.4 | 3 | 97.0% | 96.7% | -0.3 |
| Claude Haiku 4.5 | 3 | 94.3% | 94.0% | -0.3 |

Delta never exceeds 1.1 percentage points. On some scenarios caveman scores higher than baseline — brevity forces model to focus. Fewer word, same brain, as [found by research](https://arxiv.org/abs/2604.00025) that shows brevity constraints improved accuracy by 26 percentage points on certain benchmarks.

[Full results on Tessl](https://tessl.io/eval-runs/019d9ce5-3e4a-71ac-81fb-e8de7c5de827).

Reproduce:

```bash
tessl eval run skills/caveman --agent claude:claude-sonnet-4-6 \
  --variant without-context --variant with-context
```

### ...but for significantly less tokens

| Task | Normal (tokens) | Caveman (tokens) | Saved |
|------|---------------:|----------------:|------:|
| Explain React re-render bug | 1180 | 159 | 87% |
| Fix auth middleware token expiry | 704 | 121 | 83% |
| Set up PostgreSQL connection pool | 2347 | 380 | 84% |
| Explain git rebase vs merge | 702 | 292 | 58% |
| Refactor callback to async/await | 387 | 301 | 22% |
| Architecture: microservices vs monolith | 446 | 310 | 30% |
| Review PR for security issues | 678 | 398 | 41% |
| Docker multi-stage build | 1042 | 290 | 72% |
| Debug PostgreSQL race condition | 1200 | 232 | 81% |
| Implement React error boundary | 3454 | 456 | 87% |
| **Average** | **1214** | **294** | **65%** |

Range: 22%–87% savings across prompts. Caveman only affects output tokens — thinking/reasoning tokens are untouched.

## More

Full documentation, additional install options, and sub-skills (caveman-commit, caveman-review, caveman-compress) at [github.com/JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman).

Quality evals contributed by [Baruch Sadogursky](https://github.com/jbaruch) using [Tessl](https://tessl.io) eval infrastructure.
