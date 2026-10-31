# Bearings

A do-it-yourself premarital inventory for two people. Each partner answers about 270 questions alone. Bearings then compares the answers question by question and shows what to talk about.

It follows the structure of counselor-run inventories like PREPARE/ENRICH: core topics scored by couple agreement, an idealization check, relationship dynamics, closeness and flexibility maps, personality, and stress. All statements, decision questions and exercises are original. Bearings isn't affiliated with or derived from any commercial instrument.

## Files

| File | What it is |
|---|---|
| `bearings.html` | The app, without a document wrapper. This is what gets published as a Claude artifact. |
| `index.html` | The same app wrapped in a full HTML document. Open it in a browser, or host it anywhere static (GitHub Pages, Vercel, Netlify). |

After editing `bearings.html`, rebuild `index.html` (PowerShell):

```powershell
$body = Get-Content bearings.html -Raw
"<!doctype html>`n<html lang=`"en`">`n<head>`n<meta charset=`"utf-8`">`n<meta name=`"viewport`" content=`"width=device-width, initial-scale=1, viewport-fit=cover`">`n</head>`n<body>`n$body</body>`n</html>" | Set-Content index.html -NoNewline
```

## How it works

- **Taking it.** Each person answers on their own phone and then sends the other an *answer code*: the answers as JSON, deflate-compressed and base64url-encoded, about 1,700 characters. Couples can also take turns on one device. Progress saves to `localStorage`.
- **Statements** use a 5-point agree scale. Each is marked healthy-if-agree, healthy-if-disagree, or a values question with no right answer. Two partners' answers are classed as:
  - *agree*: same side of "not sure", in the healthy direction (either side counts for values questions)
  - *differ*: two or more points apart
  - *unsure*: one or both answered "not sure" and are otherwise close
  - *shared concern*: both answered on the unhealthy side
- **Topic agreement** is the share of a topic's statements in *agree*. 80% or more counts as a strength, 50–79% a likely strength, 30–49% worth discussing, and under 30% a place to start.
- **Decision questions** compare concrete choices: same, close (one step apart on an ordered scale), or far apart. Partners can guess each other's answers. "Who should handle…" questions are mirrored, so "Me" from one partner matches "Partner" from the other.
- **The talk list** ranks every item worth discussing. Big decisions where you're far apart come first, then shared concerns, then clear differences, then unsure answers and wrong guesses.
- **About each of you:**
  - commitment
  - a 7-item rose-colored-glasses check
  - four relationship dynamics (speaking up, self-assurance, avoiding issues, feeling controlled)
  - closeness and flexibility maps for the couple and for each family of origin, on 5 levels where the middle 3 count as balanced
  - personality from the public-domain Mini-IPIP (Donnellan et al., 2006), rated for yourself and for your partner
  - recent stressors
- **A private check** asks about fear, violence, control and sexual pressure. It is never stored or included in answer codes, and it shows hotline information when anything is ticked.

## Limits

- This hasn't been validated as a psychological instrument. The cut-offs and dimension scores are reasonable defaults, not norms.
- It doesn't predict outcomes, and it can't detect abuse or coercion.
- Answer codes aren't encrypted. Anyone with a code can read the answers in it.
