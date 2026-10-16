# Odysseys2 evaluation recipe

This documents the saved artifact-aware findings judge. It releases the exact system prompt and scoring policy, not the original execution runner or a complete reproduction of the evidence-building pipeline.

## Judge inputs and model

Six inspected saved requests all use the accompanying `judge-prompt.txt` byte for byte (SHA-256 `fc10c11068d0189a45b565a456260981ca7d6d757369b997bf20a5b543eec0d3`). They identify `gpt-5.6-luna` with `xhigh` reasoning effort. The older archive extraction records this same prompt hash for 2,460 readable requests; 15 request hashes were unavailable. This does not establish identical prompts for every earlier-panel run.

The harness prepares the task, website, rubric, numbered agent trajectory, final response, extracted output-file contents, and selected screenshots. The judge receives this prepared evidence and returns one structured judgment containing:

- `agent_task_reading`: its description of how the agent interpreted the request;
- `findings`: one evidence explanation and status per rubric item;
- `observations`: additional unscored observations;
- `infra_error`, `pii_present`, `reward_hacking_suspected`, and `flag_notes`.

The saved requests contain system text, input text parts, and image hashes. They show no judge tool calls. The judge does not interactively open folders, browse websites, execute code, or retrieve additional evidence. File extraction is performed by the harness before judging. “Artifact-aware” describes the evidence it receives.

## Evidence selection and limits

The prompt explicitly says long trajectory tool results are clipped in the middle, preserving the beginning and end, with omissions marked inline. Delivered-file previews can also be clipped. Missing source images or screenshots may leave a claim unassessable. A plausible value in an output file is insufficient when the requirement calls for corroborating trace evidence.

The six inspected packets contain 2–15 screenshots; their recorded `images_sent` equals `images_available`. These are observations, not universal screenshot limits. The exact global character limits, output parsers, screenshot-selection rules, request retries, and provider generation settings are not fully specified by this release. Do not infer those settings from the sample sizes. Exact replay requires the original evidence builder, complete requests, and matching model availability.

## Execution settings

The six inspected high-effort BrowserCode manifests record BrowserCode `0.1.20`, agent reasoning effort `high`, `task_timeout: 3600` seconds, and declared `max_steps: 35`. The recorded trajectory can contain more action entries than this declared step setting, so the declaration should not be interpreted as a cap of 35 logged browser actions. These settings describe the inspected main-study runs and must not be generalized to every earlier-panel or other-harness configuration.

The blog reports 20 main-study setups on 100 tasks, plus five 100-task Luna reruns: 2,500 attempts in that scope. Earlier-panel attempts are separate. The public chart data gives model/harness/effort labels and aggregate scores; it does not supply every setup's full configuration or every original trajectory. Browser Use Cloud browser provisioning and live websites also affect reproducibility.

## Deterministic score policy

For the released tasks, every rubric item has weight 1. The judge emits findings; the scoring step computes the score.

1. `met` earns the item's weight. `violated` and `not_assessable` earn zero.
2. The denominator includes every rubric item's weight, including unassessable or missing findings.
3. Item credit is `100 * earned_weight / total_weight`.
4. If the saved `rh_zeroed` flag is true, final score is zero. Otherwise final score is item credit.
5. A perfect attempt has final score 100 and is not zeroed.

The zeroing policy uses suspected reward hacking, including suspected fabrication. A flag is the judge's assessment, not independent proof of agent intent or misconduct. Other diagnostic flags should not be silently treated as equivalent to `rh_zeroed`.

Archive score records use a 0–1 scale; published CSVs use 0–100. Published task scores and times are rounded. Astra's pre-check credit and flag status are unavailable in the public score export, so those cells are blank. Reruns supply only final scores. Missing data is not zero.

## Verification coverage and remaining gaps

Release checks establish consistency between the page, its data files, and the downloadable bundle. The older archive cross-check matched all 99 available task instructions and rubrics and 884 available high-effort/rerun final scores. It excluded task `cmub-061`; that task appears in the current catalog, but its original task/run evidence was not verified against that archive.

The full 2,500-attempt count is consistent with the published aggregate counts, but not independently reconstructed from the older archive. The September Odysseys run/audit, three-grader pooled ablation, 49-of-210 ranking comparison, and published confidence intervals have not been independently recomputed in this release check. The downloads do not contain all underlying records or analysis code needed to reproduce those claims. They remain reported study results.

The paid human-review pilot did not establish a reliable human reference. Neither this consistency check nor the model re-reviews validate the judge's accuracy against ground truth. Scores compare recorded runs under their stated grading policy.
