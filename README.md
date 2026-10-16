# Odysseys2 public release

100 new web tasks built from real user requests, with 982 rubric requirements.

- [Interactive release and methodology](https://odysseysbench.com/v2/)
- [BrowserCode agent harness](https://github.com/browser-use/browsercode)

## Files

- `odysseys2-tasks.json`: all 100 instructions, start URLs and full rubrics.
- `odysseys2-rubrics.csv`: one row per requirement (982 rows). All weights are 1.
- `odysseys2-scores.csv`: 1,000 task/setup rows: four BrowserCode models at high effort, GPT-6 Astra from the earlier panel at default effort, and five GPT-5.6 Luna reruns.
- `odysseys2-chart-data.json`: the page's per-task results, time curves, harness/effort summaries, and judge/model comparison summaries.
- `SHA256SUMS`: checksums of the files above.

The scores export is the per-task data available in the blog, not all 2,500 main-study attempts or all earlier-panel runs. The chart data includes aggregate results for setups whose per-task scores are not in this export. Scores are rounded for display; aggregate means may differ slightly from averages of the rounded task scores.

## Task schema

Each task has `id`, `title`, `category`, `start_url`, `instruction`, and `rubric`. Rubric items have `id`, `name`, `requirement`, and `weight`. Titles and categories are browsing labels; the instructions and rubric requirements are copied unchanged from the release page. Task IDs retain the `cmub-` prefix.

## Score schema and grading

`final_score` is on a 0–100 scale. `item_credit` is the percentage of rubric items marked met before the whole-attempt check. `zeroed=1` means the judge applied that check, setting the final score to zero. `minutes` is recorded attempt duration. Empty cells mean unavailable, not zero. Astra's pre-check credit and flag status are unavailable in this export; reruns contain only final scores.

In chart data, `results[task_id][model]` is `[final_score, item_credit, zeroed, minutes]`, and `reps` contains five rerun final scores. Null values mean unavailable. The other chart structures mirror the published page. Astra is an earlier-panel comparison at default effort, not a fifth high-effort main-study run.

The judge reads action history, screenshots, and delivered files. Not-assessable items receive no credit. The judge has not been validated against a reliable human reference; the paid pilot was insufficient for that purpose. A judge flag is a model judgment, not an independently confirmed finding of fabrication.

## Running tasks

Use the instruction and start URL with a browser-equipped agent such as BrowserCode. Follow each task's explicit action restrictions. This release supplies task definitions and reported scores; it does not include the original benchmark runner, judge implementation, or private trajectory archives. Running a task in a current harness does not by itself reproduce the published evaluation protocol. Live sites and results change over time.

## Citation

Jang, Lawrence, Alexander Yue, Magnus Müller, Gregor Zunic, Jing Yu Koh and Ruslan Salakhutdinov. (2026). *Odysseys2: Evaluating Web Agents on Real User Requests*. https://odysseysbench.com/v2/
