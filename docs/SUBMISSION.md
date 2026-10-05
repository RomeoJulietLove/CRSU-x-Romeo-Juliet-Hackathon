# Submission instructions

CRSU Round 1 (research and ideation) runs 5–11 October 2026; the final build round runs 12–18 October 2026. Research submission closes 11 October 2026, 23:59 IST; final build submission closes 18 October 2026, 23:59 IST. Teams have one to three participants. Submit through the corresponding issue form in this repository. Public issue submission is the complete submission route; no separate email or chat invitation is needed.

## Research submission

Publish a PDF or Markdown approach note in your own project. Include the problem interpretation, hypothesis, reciprocal predictions, allocation method, clarification policy, handling of missing and delayed data, planned baselines, ablations and failure cases. Open a Research submission issue with the team name, team size and public note URL.

## Final submission

Your project must include:

- Policy source implementing POLICY_INTERFACE.md and a Dockerfile with all required inference assets.
- A README with exact setup and evaluation commands, Python/dependency versions, declared training seeds and inference random seed.
- Machine-readable full-episode results for greedy, no-clarification, random-feasible and your method on the same seeds and scenarios.
- A report with scenario-level outcomes, coverage, waiting times, clarification costs, missing feedback, runtime, at least one hypothesis-driven ablation and limitations.
- Model/data/tool provenance, dependency licences and any training-compute requirements.
- A concise product integration note in the report describing consent checks, human approval, user-facing explanations, data minimisation, failure monitoring and assumptions requiring validation before any Vouchsafe use. This note does not change the published technical score.

Run from your project root:

```bash
python -m unittest -v
python verify_data.py
python evaluate.py --seeds 101,102,103 --variants all --output results/final.json
docker build -t sequential-policy:submission .
python evaluate.py --image sequential-policy:submission --seeds 101 --output results/container_check.json
```

For a project copied from this starter, commit the report and experiment JSON explicitly, since `results/` is ignored by default. Do not commit private organiser data, personal records, secrets or development caches. The test suite checks the kit; add meaningful checks for your method where needed.

Open a Final submission issue with a public source URL, full 40-character commit SHA, report URL and results URL. An archive must be publicly downloadable and include its SHA-256. Declare external assets and their licences. The linked commit or archive is the assessed version. Amend the issue before the deadline to replace it. After the deadline, fixes cannot change that version.

A container build must succeed without credentials. Evaluation itself has no network or GPU. All assessed episodes must be valid. Runtime failures, malformed output, invalid asks or introductions and resource overruns make the submission ineligible for ranking. No interface or presentation replaces the executable policy.

Participants retain ownership of their submissions. A public submission does not itself license commercial product use. Put your chosen licence in your own project and discuss any later Vouchsafe agreement separately.
