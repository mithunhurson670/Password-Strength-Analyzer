# Password-Strength-Analyzer

### Real-Time Password Strength & Entropy Analyzer

To access the tool click the below link: https://mithunhurson670.github.io/Password-Strength-Analyzer/


A single-file, client-side tool that scores password strength using Shannon
entropy rather than arbitrary rule-of-thumb checks, wrapped in a minimal,
distraction-free interface with no framework, build step, or backend.

## 🌟 Key Features

- **Real-Time Analysis** — results update on every keystroke; no submit button, no page reload, no network request.
- **Shannon Entropy Calculation** — dynamically determines the active character pool (lowercase, uppercase, digits, symbols) and computes `length × log2(poolSize)` to measure true randomness in bits, rather than guessing from surface-level rules.
- **Normalized 0–100 Score** — entropy is capped at 100 and mapped directly to a score, giving a quick, comparable read at a glance.
- **Five-Tier Verdict System** — `Very Weak → Weak → Fair → Strong → Very Strong`, banded from the score.
- **Zero Data Retention** — the password is never transmitted, logged, or written to storage in any form; everything happens in-memory in the browser tab.
- **Minimal, Distraction-Free UI** — one input, one results panel, no colour-coded chrome or decorative elements competing with the numbers.

## 📁 Repository Structure

```
├── password-strength-analyzer.html   # Single-file tool (markup, styling, and logic)
└── README.md                         # Documentation
```

## 🧱 Logic & Structure

```
<body>
  ├── <input id="pw">              (live keystroke listener)
  └── <div id="results">
        ├── Length     — pw.length
        ├── Entropy    — length × log2(poolSize)
        ├── Score      — min(100, round(entropy))
        └── Verdict    — banded from score
```

## 🧪 Scoring Model

| Metric   | Formula                                   | Notes                                                        |
|----------|--------------------------------------------|---------------------------------------------------------------|
| Pool size | Sum of active character classes (26/26/10/32) | Grows only for character types actually present in the password |
| Entropy  | `length × log2(poolSize)`                  | Bits of randomness represented by the password's search space |
| Score    | `min(100, round(entropy))`                 | Entropy capped at 100 bits for a simple 0–100 read            |
| Verdict  | Banded thresholds on score                 | `<20` Very Weak · `<40` Weak · `<60` Fair · `<80` Strong · `≥80` Very Strong |

## Running it

Open `password-strength-analyzer.html` directly in any modern browser — no build step, no dependencies, no server required.
