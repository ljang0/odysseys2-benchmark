# Odysseys2 public release

100 new web tasks based on the real user request distribution provided by [Browser Use](https://browser-use.com), with 982 rubric requirements. Tasks were constructed from that distribution, not copied one-to-one from individual requests.

- [Interactive release and methodology](https://odysseysbench.com/v2/)
- [BrowserCode agent harness](https://github.com/browser-use/browsercode)

## Authors

Lawrence Jang¹, Alexander Yue², Magnus Müller², Gregor Zunic², Andrew Keunwoo Jang¹, Younghan Park¹, Mareks Woodside¹, Daniel Fried¹, Jing Yu Koh¹, Ruslan Salakhutdinov¹

¹ Carnegie Mellon University · ² Browser Use

## Files

- `odysseys2-tasks.json`: all 100 instructions, start URLs and full rubrics.
- `odysseys2-rubrics.csv`: one row per requirement (982 rows). All weights are 1.
- `odysseys2-scores.csv`: 1,000 task/setup rows: four BrowserCode models at high effort, GPT-6 Astra at default effort, and five GPT-5.6 Luna runs.
- `odysseys2-chart-data.json`: the page's per-task results, time curves, harness/effort summaries, and judge/model comparison summaries.
- `judge-prompt.txt`: exact system prompt from the six inspected findings-judge requests.
- `EVALUATION.md`: input preparation, scoring rules, recorded settings, evidence limits and verification coverage.
- `LICENSE`: MIT license, matching the original Odysseys project.
- `SHA256SUMS`: checksums of the release files.

The scores export contains the 1,000 task/setup rows listed above. The chart data includes aggregate results for setups whose per-task scores are not in this export. Scores are rounded for display; aggregate means may differ slightly from averages of the rounded task scores.

## Task schema

Each task has `id`, `title`, `category`, `start_url`, `instruction`, and `rubric`. Rubric items have `id`, `name`, `requirement`, and `weight`. Titles and categories are browsing labels; the instructions and rubric requirements are copied unchanged from the release page. Task IDs retain the `cmub-` prefix.

## Score schema and grading

`final_score` is on a 0–100 scale. `item_credit` is the percentage of rubric items marked met before the reward hacking check. `zeroed=1` means the judge applied that check, setting the final score to zero. `minutes` is recorded attempt duration. Empty cells mean unavailable, not zero. Astra's pre-check credit and flag status are unavailable in this export; runs contain only final scores.

In chart data, `results[task_id][model]` is `[final_score, item_credit, zeroed, minutes]`, and `reps` contains five run final scores. Null values mean unavailable. The other chart structures mirror the published page. Astra ran at default effort and is separate from the four high-effort models.

The artifact-aware judge evaluates action history, screenshots, and file contents extracted by the harness. It does not use tools or open files itself. Not-assessable items receive no credit. The judge has not been validated against a reliable human reference; the paid pilot was insufficient for that purpose. A judge flag is a model judgment, not an independently confirmed finding of fabrication.

## Eight-run paper figure

The [eight-run figure](https://odysseysbench.com/v2/figures/eight-runs.pdf) covers 100 tasks. At 60 minutes, the mean rubric score is 56.9 (±2.9 sample SD), best-of-eight is 83.1, and worst-of-eight is 23.1. The mean perfect-pass rate is 6.25% (±1.5 percentage points sample SD), at least one attempt is perfect on 26.0% of tasks, and no task is perfect in all eight attempts. Thin lines show individual runs, shading shows one sample standard deviation, and callouts mark 15 and 30 minutes. Best@8 and Worst@8 select an attempt for each task after grading. The per-task score CSV contains five Luna runs; the figure summarizes eight.

## Running tasks

Use the instruction and start URL with a browser-equipped agent such as BrowserCode. Follow each task's explicit action restrictions. This release supplies task definitions and reported scores; it does not include the original benchmark runner, judge implementation, or private trajectory archives. Running a task in a current harness does not by itself reproduce the published evaluation protocol. Live sites and results change over time.

## License

The original task/rubric definitions, score data, prompt, and documentation in this release are provided under the MIT license in `LICENSE`. This does not grant rights to third-party websites, their content, or external dependencies. No private trajectory archives are included.

## Citation

Jang, Lawrence, Alexander Yue, Magnus Müller, Gregor Zunic, Andrew Keunwoo Jang, Younghan Park, Mareks Woodside, Daniel Fried, Jing Yu Koh and Ruslan Salakhutdinov. (2026). *Odysseys2: A Web Agent Benchmark Based on Real User Requests*. https://odysseysbench.com/v2/

```bibtex
@misc{jang2026odysseys2,
  title        = {Odysseys2: A Web Agent Benchmark Based on Real User Requests},
  author       = {Jang, Lawrence and Yue, Alexander and M{\"u}ller, Magnus and
                  Zunic, Gregor and Jang, Andrew Keunwoo and Park, Younghan and
                  Woodside, Mareks and Fried, Daniel and Koh, Jing Yu and Salakhutdinov, Ruslan},
  year         = {2026},
  howpublished = {\url{https://odysseysbench.com/v2/}}
}
```
