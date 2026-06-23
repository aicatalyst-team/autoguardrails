# Blog Abstract: autoguardrails

## Thesis
Deploying Santander AI Lab's autoguardrails on OpenShift proves that AI safety evaluation harnesses work seamlessly as containerized workloads, enabling platform teams to run guardrail policy testing as part of their AI operations pipeline.

## Target Audience
Platform engineers, ML engineers, and AI safety teams deploying LLM-based applications on Red Hat OpenShift AI.

## Blog Type
Red Hat Developer Blog

## Key Points
1. autoguardrails is a zero-dependency Python CLI that evaluates guardrail policies against adversarial attack suites, measuring attack success rate (ASR) with a benign-pass floor
2. The tool was containerized with a UBI-minimal image and deployed as Kubernetes Jobs, completing baseline evaluation in under 5 seconds
3. The deployment validates that AI safety evaluation can be operationalized on OpenShift AI, connecting to TrustyAI and model serving workflows

## Products/Projects
Red Hat OpenShift AI, TrustyAI, Open Data Hub

## CTA
Try deploying autoguardrails on your OpenShift cluster to evaluate your own guardrail policies.

## Proposed Section Outline
1. What is autoguardrails?
2. Why AI safety evaluation belongs on your platform
3. Containerizing for OpenShift
4. Deploying and running the evaluation
5. Results and what we learned
6. Next steps: connecting to live models
