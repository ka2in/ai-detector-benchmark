# AI Detector Benchmark: Samples and Results

A small, transparent test of three commercial AI text detectors, GPTZero, Originality.ai, and Scribbr, against a human-written control, a raw AI-generated sample, and a lightly human-edited version of that same AI sample.

**This is a spot check, not a study.** Three samples per tool is not statistically powered. Treat the findings below as illustrative, not as a definitive measure of any tool's overall accuracy.

## What's in this repo

| File | Description |
|---|---|
| `sample1-git-primer-excerpt.md` | Human-written control. A 715-word excerpt from [Git Primer for the Impatient](https://docs.farowave.com/gitinminutes), written by the repo author. |
| `sample2-raw-ai.md` | Raw, unedited AI output. A 760-word technical primer generated fresh for this test, deliberately matched to Sample 1's register (procedural, numbered steps, command blocks). |
| `sample3-human-edited.md` | Sample 2, edited by hand by the repo author, not AI-assisted. 121 of 760 words changed (15.92%), verified with a word-level diff, not eyeballed. |

Samples 2 and 3 were written for this test specifically. They are not real product documentation.

## Methodology

- Three tools: GPTZero (gptzero.me), Originality.ai (originality.ai), Scribbr (scribbr.com/ai-detector)
- Free tiers only, no paid access, no account created beyond what each tool's free tier requires
- All three samples are close in length (715–760 words) to keep length from confounding the comparison
- Sample 3's edit rate was deliberately targeted at 15–20% word change, a threshold cited in AI-detection research as sufficient to disrupt a detector's confidence
- Three of the nine results were independently re-run in a fresh browser session as a stability check. All three reproduced exactly.

## Results

| Sample | GPTZero | Originality.ai | Scribbr |
|---|---|---|---|
| Human control (Sample 1) | 99% Human | 94% conf., "likely original" | 27% AI-generated |
| Raw AI (Sample 2) | 100% AI | 100% conf., "exceeds 15%" | 83% AI-generated |
| Edited AI (Sample 3, 15.92% changed) | 100% AI, unchanged | 51% conf., "exceeds 15%" | 72% AI-generated |

## Key findings

1. **The same 15.92% edit produced three different outcomes across tools.** GPTZero's confidence didn't move. Originality.ai's confidence nearly collapsed, from 100% to 51%, confirmed stable on a second run. Scribbr softened moderately, from 83% to 72%.

2. **Scribbr was the only tool with a false-positive-adjacent result.** It flagged 27% of a genuinely human-written technical document as AI-generated, confirmed stable on a second run. The other two tools both read the same text as confidently human.

3. **Vendor accuracy claims and independent, larger-scale benchmarks show meaningful gaps.** GPTZero advertises 99.3% accuracy; independent estimates outside controlled conditions cluster around 82-90%. Originality.ai advertises 99%+; one independent benchmark measured it at 76%. Scribbr publishes no headline accuracy figure at all.

## Reproducing this test

All three tools' free tiers are accessible without payment. Paste any of the three sample files into each tool directly and compare against the results above. Note that free-tier limits and interfaces may change over time; this test was run in August 2026.

## License

Sample text and this README are shared for reference and verification purposes.
