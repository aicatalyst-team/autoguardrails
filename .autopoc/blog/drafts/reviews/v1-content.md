# Content Review -- v1

## Scores
| Dimension | Raw (1-10) | Weight | Weighted |
|---|---|---|---|
| Technical accuracy | 8 | 2x | 16 |
| Red Hat voice | 8 | 2x | 16 |
| Audience alignment | 7 | 1x | 7 |
| Originality | 8 | 1x | 8 |
| Evidence & examples | 8 | 2x | 16 |
| Product positioning | 9 | 1x | 9 |
| Human authenticity | 7 | 2x | 14 |
| **Total** | | | **86 / 110 -> 7.8** |

## Line-Level Feedback

### Technical accuracy
- **Location**: Section "What is autoguardrails?", line 5
- **Issue**: The phrase "fix everything else" slightly mischaracterizes the tool. The eval suite (`eval_suite.jsonl`) and judge prompt (`judge_prompt.md`) are also user-editable files that ship as defaults. Calling them "fixed" overstates it.
- **Current**: "keep one mutable surface (a `policy.md` file defining your guardrail rules), fix everything else (the attack suite, the judge prompt, the evaluation harness)"
- **Suggested**: "keep one primary variable (a `policy.md` file defining your guardrail rules), hold the attack suite, judge prompt, and evaluation harness constant, then measure whether your policy changes actually reduce attack success rate"

- **Location**: Section "Containerizing for OpenShift", line 29
- **Issue**: The Dockerfile uses `ubi9/ubi-minimal` but the text on line 27 says "UBI-minimal-based Dockerfile." This is accurate. However, the AGENTS.md reference lists `ubi9/python-312` as the standard Python base image for the project. Consider noting why you chose `ubi-minimal` plus manual Python install over the prebuilt Python image. This is a minor gap but a reader running OpenShift AI will wonder why you didn't use the standard Python runtime image.
- **Current**: "We built a UBI-minimal-based Dockerfile:"
- **Suggested**: "We chose a UBI-minimal base rather than the prebuilt `ubi9/python-312` runtime image to keep the footprint small, since autoguardrails has zero runtime dependencies beyond the standard library:"

- **Location**: Results table, line 84
- **Issue**: The Status row shows `ASR=0.4000` but the Baseline row shows `ASR=1.0000`. The text doesn't explain what ASR=1.0 means in context (all attacks succeed, meaning the stub "model" has no guardrails). A reader unfamiliar with autoguardrails will be confused about whether ASR=1.0 is good or bad.
- **Current**: "ASR=1.0000, benign_pass=1.0000, 140 total cases"
- **Suggested**: Add a sentence before the table: "ASR (Attack Success Rate) measures how many adversarial prompts bypass the guardrail. A lower ASR means a stronger policy. The deterministic stubs return fixed responses, so the baseline ASR of 1.0 is expected and serves as a reference point."

### Red Hat voice
- **Location**: Section "Why AI safety evaluation belongs on your platform", line 11
- **Issue**: "Someone runs a few prompts locally, eyeballs the results, and declares the policy 'good enough.'" is strong, conversational, and direct. Good use of the Red Hat voice. The opening section is also confident without being salesy.
- **Current**: (no change needed)
- **Suggested**: (keep as-is)

- **Location**: Section "Results and what we learned", line 88
- **Issue**: The honest treatment of the candidate scenario failure is excellent and very on-brand for the Red Hat voice. Admitting "this failed and here's why" is exactly the kind of brave, authentic content that resonates.
- **Current**: (no change needed)
- **Suggested**: (keep as-is)

- **Location**: Section "Why AI safety evaluation belongs on your platform", line 20
- **Issue**: "For regulated industries like financial services (Santander's domain), this isn't optional. It's a governance requirement." reads slightly assertive without evidence. What specific regulation requires this? If you can't cite one, soften it.
- **Current**: "For regulated industries like financial services (Santander's domain), this isn't optional. It's a governance requirement."
- **Suggested**: "For regulated industries like financial services, where Santander operates, demonstrating that your guardrail policies are systematically tested is increasingly a compliance expectation."

### Audience alignment
- **Location**: Section "Containerizing for OpenShift", lines 28-46
- **Issue**: The Dockerfile is great for the platform engineer audience, but the line `RUN python3 -m pip install --no-cache-dir -e .` uses editable mode (`-e .`) inside a container. This is a development pattern, not a production best practice. A platform engineer would notice and question it.
- **Current**: `RUN python3 -m pip install --no-cache-dir -e .`
- **Suggested**: `RUN python3 -m pip install --no-cache-dir .` (drop the `-e` for production images, or explain why editable mode is used)

- **Location**: Overall
- **Issue**: The target audience includes "AI safety teams" per the abstract, but the post is primarily written for platform engineers. AI safety practitioners would want more detail about the attack categories in the eval suite, how the judge prompt works, and what the ASR numbers mean for their threat model. Consider one or two sentences addressing that audience.
- **Current**: (gap)
- **Suggested**: Add a brief parenthetical or sentence in the "What is autoguardrails?" section explaining the types of attacks tested (prompt injection, jailbreaks, etc.) and how the judge determines pass/fail.

### Originality
- **Location**: Section "Results and what we learned", lines 87-91
- **Issue**: The insight about ephemeral storage breaking the baseline-candidate workflow is genuinely original. This is not something you'd find in docs. The proposed solutions (PVC or combined Job) are practical. This is the strongest section of the post.
- **Current**: (no change needed)
- **Suggested**: (keep as-is)

- **Location**: Section "Why AI safety evaluation belongs on your platform", lines 13-19
- **Issue**: The four bullet points (Reproducibility, Auditability, Integration, Scalability) are solid but somewhat predictable. Every "why Kubernetes" blog hits these notes. Can you ground at least one of them in something specific you observed during the PoC?
- **Current**: "**Reproducibility:** Every evaluation run is a Kubernetes Job with fixed inputs and captured outputs"
- **Suggested**: "**Reproducibility:** Every evaluation run is a Kubernetes Job with fixed inputs and captured outputs. In our PoC, running the same baseline Job twice produced identical ASR=1.0 and benign_pass=1.0 scores, confirming deterministic behavior."

### Evidence & examples
- **Location**: Section "Results and what we learned", lines 80-86
- **Issue**: The results table is concrete and well-formatted. Showing actual durations (5s, 4s, 120s) and metrics (ASR, benign_pass) gives the post real substance. The failure case is particularly valuable evidence.
- **Current**: (no change needed)
- **Suggested**: (keep as-is)

- **Location**: Section "Next steps: connecting to live models", lines 113-117
- **Issue**: The environment variable examples are good, but this section makes a claim ("The real value unlocks when you connect autoguardrails to live model endpoints") without any evidence that this actually works. Since you didn't test it, be transparent.
- **Current**: "The real value unlocks when you connect autoguardrails to live model endpoints on OpenShift AI."
- **Suggested**: "We didn't test against a live model in this PoC, but autoguardrails is designed to connect to any OpenAI-compatible endpoint. Pointing it at a vLLM-served model on OpenShift AI would look like this:"

### Product positioning
- **Location**: Overall
- **Issue**: Product mentions feel natural and earned. OpenShift AI, TrustyAI, and UBI are mentioned where they're genuinely relevant. The post doesn't feel like a product pitch. Well done.
- **Current**: (no change needed)
- **Suggested**: (keep as-is)

### Human authenticity
- **Location**: Section "What is autoguardrails?", line 5
- **Issue**: "simple but powerful approach" is a mildly formulaic AI writing pattern. "Powerful" is one of the flagged vague enthusiasm words.
- **Current**: "The tool takes a simple but powerful approach"
- **Suggested**: "The tool takes a focused approach" or "The approach is straightforward"

- **Location**: Overall structure
- **Issue**: The post has a somewhat uniform rhythm: short intro paragraph, then a list or code block, in every section. Varying the structure would feel more natural. For instance, the "Why AI safety evaluation belongs on your platform" section could lead with a short anecdote or a specific scenario rather than jumping to a bullet list.
- **Current**: (structural pattern)
- **Suggested**: Consider opening the "Why" section with a one-sentence scenario: "Picture a team updating their content policy the week before a compliance audit. How do they prove the new policy actually blocks more attacks than the old one?" Then transition to the bullet list.

- **Location**: Lines 48, 119
- **Issue**: Two instances of colons introducing lists or elaborations in quick succession. This is a subtle AI pattern when pervasive, but here it's limited and doesn't significantly detract.
- **Current**: (minor)
- **Suggested**: (no action required, just noting)

## AI Writing Flags

### Em Dashes: 0 found
No em dash characters or stylistic double-hyphens detected. The `--` occurrences are all CLI flags (`--reset`, `--repeat`, `--notes`, `--help`, `--model`), which are correct.

### Formulaic Phrases: 1 found
- "simple but powerful" (line 5): vague enthusiasm pattern. Replace with a more specific descriptor.

## Summary
The single most important content change: explain what ASR means and why ASR=1.0 is expected in the stub-based baseline, before the results table. Without this context, the key metrics in the post are opaque to readers who haven't used the tool, and the results section loses much of its impact.
