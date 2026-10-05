# CRSU x Romeo & Juliet Hackathon

**Participant release 1.0.0 | 5 October 2026 | Vouchsafe-focused synthetic challenge**

Design a consent-first decision-support policy for sequential introductions. The policy must respect each person's stated constraints, work with incomplete preferences and delayed feedback, and leave final decisions to people. Every person, profile, conversation and outcome in this kit is synthetic.

## Start here

1. Read [the problem statement](PROBLEM_STATEMENT.md) or [download its PDF](docs/PROBLEM_STATEMENT.pdf), [data contract](docs/DATA_CONTRACT.md), [policy interface](docs/POLICY_INTERFACE.md) and [submission instructions](docs/SUBMISSION.md).
2. Download this repository with **Code → Download ZIP**, or clone it. The complete synthetic dataset is in `data/`; no Supabase account, API key or separate download is needed.
3. Install Python 3.10 or later. Run:

```bash
python -m unittest -v
python verify_data.py
python evaluate.py --seeds 101 --output results/first_run.json
```

On Windows, use `py` instead of `python` if needed. On macOS/Linux, use `python3` if that is your Python executable. The starter has no external Python dependencies. Results measure this invented simulator only.

## CRSU participation

- **Teams:** 1–3 participants.
- **Round 1 (research and ideation):** 5–9 October 2026; results by 11 October, 22:00 IST.
- **Final build:** 12–18 October 2026.
- **Registration:** complete registration on both [Unstop](https://unstop.com/) and [events.romeojuliet.love](https://events.romeojuliet.love/crsu-hackathon-2026). Complete the event site's voice chat; it issues a participant code. The team leader must enter each team member's issued code while completing registration on Unstop.
- **Mentorship and workshops:** these are not part of the CRSU track.

Use the forthcoming Google Form for Round 1 research submissions. Use the Final submission and Question issue forms linked below for build submissions and technical questions. Event registration or the participant code is handled through Unstop and the event website, not through GitHub.

## What is included

| File / folder | Purpose |
|---|---|
| [PROBLEM_STATEMENT.md](PROBLEM_STATEMENT.md) | Challenge, rules, scoring, schedule and participation terms |
| [data/](data/) | 2,000 synthetic adults across ten disjoint pools |
| [data_manifest.json](data_manifest.json) | Pool counts, generation seeds and train/validation/development-test split |
| [docs/DATA_CONTRACT.md](docs/DATA_CONTRACT.md) | Fields, constraints and feedback rules |
| [docs/POLICY_INTERFACE.md](docs/POLICY_INTERFACE.md) | Executable JSON request/response protocol |
| [policy.py](policy.py) | Greedy, no-clarification and random-feasible baselines |
| [evaluate.py](evaluate.py) | Episode runner, metrics and scenario-level score |
| [build_public_data.py](build_public_data.py) | Rebuild public synthetic tables in a new folder |
| [kit.py](kit.py) | Reproducible simulator and reciprocal eligibility checks |
| [organise.py](organise.py) and [docs/ORGANISER_RUNBOOK.md](docs/ORGANISER_RUNBOOK.md) | Organiser assessment commands and ranking procedure |
| [Dockerfile](Dockerfile) | Offline container packaging for assessed inference |
| [docs/SUBMISSION.md](docs/SUBMISSION.md) | Research and final submission requirements |
| [docs/INTEGRATION.md](docs/INTEGRATION.md) | Safe adapter boundary for later Vouchsafe evaluation |
| [docs/FAQ.md](docs/FAQ.md) | Common questions and communication guidance |
| [examples/](examples/) | Reference baseline results and report guide |

## Develop and compare

Edit `policy.py`, keeping the JSON interface. Use only the observable input state. The evaluator handles refreshed observations after clarification. Policy memory is passed explicitly between calls and reset between episodes.

```bash
python evaluate.py --baseline greedy --seeds 101,102,103 --variants all --output results/greedy.json
python evaluate.py --baseline no_asks --seeds 101,102,103 --variants all --output results/no_asks.json
python evaluate.py --baseline random --seeds 101,102,103 --variants all --output results/random.json
```

The full commands take longer than the quick start. Public variants are `development`, `sparse`, `cold_start`, `delayed`, `shift` and `drift`. Keep the six training pools, two validation pools and two development-test pools disjoint. Day-30 snapshots are not observations from earlier decisions.

To check container execution after installing Docker:

```bash
docker build -t crsu-policy:1.0 .
python evaluate.py --image crsu-policy:1.0 --seeds 101 --output results/container.json
```

Local subprocess mode is only for trusted development code. Assessed submissions use offline containers with no host evaluation files mounted. Private organiser worlds are not included in this repository.

## Submit and ask questions

| Milestone | Date and time (IST) |
|---|---|
| Round 1 research submission closes | 9 October 2026, 23:59 |
| Round 1 results announced by | 11 October 2026, 22:00 |
| Round 2 build starts | 12 October 2026 |
| Final build submission closes | 18 October 2026, 23:59 |

**Round 1:** submit the research note through a Google Form. The organisers will release the link soon through [Discord](https://discord.gg/ka3uRZza6) and [the submission guide](docs/SUBMISSION.md#research-submission). GitHub Issues are not the research submission route.

**Round 2:** use the [Final submission](https://github.com/RomeoJulietLove/CRSU-x-Romeo-Juliet-Hackathon/issues/new?template=final_submission.yml) issue form by the final deadline. Provide the immutable submitted version and required report/results. Use [Question](https://github.com/RomeoJulietLove/CRSU-x-Romeo-Juliet-Hackathon/issues/new?template=question.yml) for technical questions. Never post personal data, access codes or credentials in public issues.

The repository is the technical source of truth. Questions answered through public Issues are visible to all teams. Event announcements and registration reminders are shared through [the CRSU Discord server](https://discord.gg/ka3uRZza6).

## Data and ownership

The dataset contains invented records only. It contains no real Romeo & Juliet member profiles, conversations, contact details, audio or outcomes. Its structure is designed for a hackathon simulator and does not establish that a model predicts real relationship outcomes.

The [starter-code licence](LICENSE) and [synthetic-data licence](DATA_LICENSE.md) cover the supplied materials. Participants retain ownership of their submissions; participation does not give Vouchsafe a commercial licence to student code. Any later product use requires a separate written agreement.
