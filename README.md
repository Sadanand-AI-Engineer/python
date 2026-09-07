 
Hi Team, I went through the Arize AX documentation and documented my understanding of how we can fit it into our current UW AI Assist POC. I also used Copilot to generate a small integration/template codebase against our current flow so we can see what the implementation could look like, rather than keeping it only at the architecture level. Arize would sit around the existing AKS application as the observability/evaluation layer without changing the underwriting flow.

It looks like we may have a solution for some of the questions that could come up during AIRB/production review — production hallucination/grounding monitoring, detecting silent RuleEngine drift, comparing prompt/model changes against the same golden dataset before promotion, identifying recurring failure patterns through Signal, and PHI-safe tracing. We still need to validate the enterprise side, particularly Private Link/connectivity, SSO/RBAC, data-region requirements and whether Arize is the approved observability path for this workload.

I also created these POC templates using Copilot:

tracing_init.py — initializes OpenTelemetry/OpenInference tracing for LangGraph and model calls at AKS startup.
guardrail_spans.py — exposes our existing grounding checks as traceable Guardrail spans while redacting clinical/PHI attributes.
code_evaluator_rule_drift.py — replays the deterministic RuleEngine against traced inputs and flags MATCH/DRIFT.
build_golden_dataset.py — converts our existing synthetic underwriting cases into a reusable Arize regression dataset.
run_experiment.py — compares current vs. candidate versions against the same dataset/evaluator before promotion.

I’ve attached the notes and templates for review. These are POC-level templates for discussion/validation, not finalized production code.
