tracing_init.py — Gives us end-to-end visibility of each underwriting request, so we can see which agent, retrieval step, or model call caused an issue.
guardrail_spans.py — Makes our grounding checks visible in Arize, so we can quickly identify unsupported responses while keeping PHI out of the telemetry.
code_evaluator_rule_drift.py — Rechecks our underwriting rules against production traces, helping us catch if a rule/code change unexpectedly changes an underwriting result.
build_golden_dataset.py — Reuses our known underwriting test scenarios as a standard regression set, so every future change is tested against the same expected outcomes.
run_experiment.py — Lets us compare the current and proposed versions using the same test cases and scoring, so we have measurable evidence before promoting a prompt, model, retrieval, or code change.
