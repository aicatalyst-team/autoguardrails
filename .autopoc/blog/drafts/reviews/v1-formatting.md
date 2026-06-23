# Formatting Review: v1 Draft -- autoguardrails on OpenShift AI

## Scores

| Dimension | Weight | Score (1-10) | Weighted |
|---|---|---|---|
| Heading hierarchy | 1x | 8 | 8 |
| Code formatting | 1x | 5 | 5 |
| CTA placement | 2x | 2 | 4 |
| SEO readiness | 1x | 3 | 3 |
| Link strategy | 1x | 4 | 4 |
| Editorial compliance | 2x | 5 | 10 |
| Brand standards | 1x | 6 | 6 |
| Word count | 1x | 8 | 8 |
| **Total** | **10x** | | **48** |

**Normalized score: (48 / 100) * 10 = 4.8 / 10**

---

## Line-level feedback

### Heading hierarchy (8/10)

Headings are all H2 with no H1 in body -- correct. Sentence case is used consistently. One minor issue: "Next steps: connecting to live models" (line 107) should capitalize after the colon per the rubric rule ("capitalize after colons"), making it "Next steps: Connecting to live models."

No H3 sub-headings are used, which is acceptable for a post this length but limits scannability in the longer sections (lines 50-105 cover deployment, results, and architecture in a dense run).

### Code formatting (5/10)

Code blocks use proper fenced syntax with language tags (`dockerfile`, `yaml`, `bash`, `mermaid`) -- good. The code itself appears real and runnable.

However, the draft uses inline backticks extensively in running text, which the rubric explicitly prohibits:

- Line 5: `policy.md`
- Line 48: `USER 1001`, `chgrp -R 0`
- Line 52: not backticked but references CLI tool
- Line 88: `results.tsv`, `candidate`
- Line 90: no backticks here, good

Replace all inline backticks with alternative phrasing. For example:
- "a policy.md file" -> "a policy.md file" (rendered as plain text, no monospace)
- "USER 1001" -> describe as "a non-root user directive"
- "results.tsv" -> "the results file"

Or use italics where a filename must be called out specifically.

### CTA placement (2/10)

This is the biggest gap. The abstract defines a clear CTA ("Try deploying autoguardrails on your OpenShift cluster to evaluate your own guardrail policies") but it never appears in the draft. The rubric requires CTAs near the top, mid-post, and at closing, linked to redhat.com.

Currently:
- **Top:** No CTA. The intro (lines 1-7) could end with a link to the OpenShift AI product page.
- **Mid:** No CTA. After the containerization section (line 48) would be a natural spot for "Get started with Red Hat OpenShift AI" or similar.
- **Closing:** Lines 122-127 have next steps and GitHub links, but no actionable CTA linking to redhat.com. The abstract's CTA should appear here with a link to the OpenShift AI trial or documentation page.

Suggested additions:
1. After line 7, add: "Learn more about [Red Hat OpenShift AI](https://www.redhat.com/en/technologies/cloud-computing/openshift/openshift-ai)."
2. After line 20, add a CTA linking to OpenShift AI's TrustyAI documentation.
3. At the end (after line 127), add the abstract's CTA with a link: "Try deploying autoguardrails on your own [Red Hat OpenShift AI](https://www.redhat.com/en/technologies/cloud-computing/openshift/openshift-ai) cluster to evaluate your guardrail policies."

### SEO readiness (3/10)

The post has no title. There's no H1 or meta title defined. The first heading is "## What is autoguardrails?" which works as a section header but not as the post title. A proper title is needed, ideally 50-60 characters with the primary keyword.

Suggested title: "Deploy AI guardrail evaluation on OpenShift AI with autoguardrails" (63 chars -- trim slightly).

The first paragraph (line 3) does contain relevant keywords ("guardrails," "evaluation," "adversarial prompts") which is good. But without a title, search engines have nothing to index as the primary heading.

### Link strategy (4/10)

Two external GitHub links exist (lines 3 and 127), which are appropriate and not competitor links. However:

- **No internal links to redhat.com** at all. The rubric requires internal links to redhat.com properties. The post mentions Red Hat OpenShift AI, TrustyAI, and UBI images without ever linking to their product pages or documentation.
- Suggested internal links:
  - Red Hat OpenShift AI -> https://www.redhat.com/en/technologies/cloud-computing/openshift/openshift-ai
  - TrustyAI -> link to the TrustyAI documentation or blog
  - UBI images -> https://www.redhat.com/en/blog/introducing-red-hat-universal-base-image
  - Red Hat OpenShift -> https://www.redhat.com/en/technologies/cloud-computing/openshift

### Editorial compliance (5/10)

**Oxford commas:** Mostly correct. Line 15 "logged, versioned, and traceable" -- good. Line 48 uses the serial comma correctly. No violations found.

**Product names:** Mixed compliance.
- "Red Hat OpenShift AI" is used correctly on lines 7, 13, and 119 -- good.
- "OpenShift" appears alone on lines 22, 48, and 68 without "Red Hat" prefix. First standalone mention should be "Red Hat OpenShift."
- "TrustyAI" on lines 17 and 125 -- should verify this is the official product name (it is, as a component name under OpenShift AI).
- "UBI-minimal" and "UBI" on lines 26-29 -- "UBI" isn't expanded on first use. Should be "Universal Base Image (UBI)" on first mention.

**Acronyms not expanded on first use:**
- "ASR" (line 72): first appears as "ASR metrics" with no expansion. Should be "attack success rate (ASR)."
- "CLI" (line 52): should be "command-line interface (CLI)" on first use.
- "PVC" (line 103): should be "PersistentVolumeClaim (PVC)" on first use. (Line 90 mentions "PersistentVolumeClaim" in full, but PVC appears later in the mermaid diagram without prior abbreviation in running text.)
- "CronJob" / "CronJobs" (lines 18, 122): these are Kubernetes resource types so capitalization is correct, but the term could benefit from brief explanation for the target audience.

**Contractions:** Some used ("doesn't" on line 11, "didn't" implicitly) but the draft could be more aggressive with contractions as the rubric requests. Examples:
- Line 11: "This does not scale" -- should be "This doesn't scale" (wait, line 11 already says "doesn't" -- good).
- Line 20: "this is not optional" -- should be "this isn't optional."
- Line 90: "This is solvable" -- consider "Here's how to fix it" or similar.

**Numerals:** Line 24 "zero runtime dependencies" -- should be "0 runtime dependencies" per the numerals rule. Line 48 "under 30 seconds" -- correct. Line 79 "Three of four" -- should be "3 of 4."

**Em dashes:** None present -- good.

### Brand standards (6/10)

The mermaid diagram (line 93) uses Red Hat brand color `#EE0000` -- good attention to detail. Product names are mostly correct (see editorial compliance above). No competitor brand references.

Deductions: No reference to or compliance with Red Hat developer blog formatting templates. The draft doesn't specify author, date, or taxonomy metadata that the publishing platform would require.

### Word count (8/10)

815 words, within the 800-1300 range for a tutorial/PoC post. On the lean side, which means adding CTAs, expanding acronyms, and adding a title won't push it over the upper bound. Ideal target would be closer to 900-1000 after revisions.

---

## Editorial compliance checklist

| Rule | Status | Notes |
|---|---|---|
| Sentence case headings | PASS | All H2s use sentence case |
| Capitalize after colons | FAIL | Line 107: "connecting" should be "Connecting" |
| Oxford commas | PASS | Consistently applied |
| No backticks | FAIL | Multiple inline backticks throughout (lines 5, 48, 88) |
| Full product name first mention | PARTIAL | "Red Hat OpenShift AI" correct; "OpenShift" alone and "UBI" not expanded |
| Lowercase component descriptors | PASS | No violations found |
| No H1 in body | PASS | All headings are H2 |
| Expand acronyms on first use | FAIL | ASR, CLI, UBI, PVC not expanded |
| Use contractions aggressively | PARTIAL | Some used, but "is not" on line 20 and other opportunities missed |
| Numerals in running text | FAIL | "zero" (line 24), "Three of four" (line 79) should be numerals |
| No em dashes | PASS | None present |

---

## Summary

The draft is technically strong and well-structured, with clean heading hierarchy and real, runnable code examples. The content itself is compelling and appropriately scoped.

The most critical gaps are the complete absence of CTAs (the single highest-weighted dimension) and missing SEO infrastructure (no title). These two issues alone pull the score below 5.0.

The second tier of issues involves editorial compliance: unexpanded acronyms (ASR, CLI, UBI), inline backticks that need removal, inconsistent product name usage ("OpenShift" without "Red Hat"), and missed opportunities for contractions and numeral formatting.

**Top 5 fixes for v2:**

1. Add a post title (50-60 chars) with primary keywords
2. Add 3 CTAs (top, mid, closing) linked to redhat.com/OpenShift AI product page
3. Remove all inline backticks and rephrase affected text
4. Expand all acronyms on first use (ASR, CLI, UBI, PVC)
5. Add internal links to redhat.com properties (OpenShift AI, TrustyAI, UBI)
