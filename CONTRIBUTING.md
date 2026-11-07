# Contributing to K.A.V.A.C.H Blue Team Challenges

Thank you for helping build practical, approachable SOC and Blue Team challenges for the K.A.V.A.C.H community. Consistent organization helps participants find what they need, keeps solution material protected, and makes each challenge easier to review and integrate into the community platform.

## Challenge structure

Add each new challenge under the appropriate difficulty directory:

```text
Easy-Challenges/ | Medium-Challenges/ | Hard-Challenges/
└── Challenge-XX-Descriptive-Name/
    ├── README.md
    ├── questions.md
    ├── soc-lab-challenge.md
    ├── evidence/
    └── organizer/
```

Use the existing `Challenge-01-The-Failed-Login` directory as the reference implementation. Not every challenge needs both participant formats, but every challenge should remain self-contained and include its own `README.md`.

## Where files belong

### Challenge folder

Keep participant-facing content directly in the challenge folder. This includes the challenge question or question sheet, scenario briefs, lab instructions, and other general materials needed to complete the challenge. The challenge's `README.md` should introduce the scenario and provide clear navigation to its participant materials and evidence.

### `evidence/`

Store all files participants must examine in `evidence/`. This includes logs, packet captures, screenshots, disk or memory artifacts, and any other supporting evidence. Use clear, descriptive filenames and ensure all material is safe and sanitized for training use.

### `organizer/`

Keep all organizer-only content in `organizer/`. This includes answer keys, expected findings, solutions, scoring or evaluation guidance, AI evaluation prompts, and any steps used to reproduce or validate the scenario. Do not place answers or reproduction details in participant-facing files.

## Before submitting

- Confirm the challenge is placed under the correct difficulty directory.
- Confirm its `README.md` links participants to the relevant questions, lab brief, and evidence.
- Confirm all artifacts are located in `evidence/` and all answers, evaluation material, and reproduction steps are located in `organizer/`.
- Review the content to ensure it is accurate, safe to distribute, and free of sensitive real-world data.

Following this structure keeps every challenge clear for learners and dependable for organizers, reviewers, and platform integrations. Thank you for contributing.
