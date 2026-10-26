# aws-hackathon-project

# Strands Decider 2B Safety Guardrail Interceptor

An AI Agent safety tool pattern implemented for the AWS Builder Center Weekend Challenge ("Give your Agent a Tool"). 

This project demonstrates real-time safety verification of proposed tool calls before execution using the **Strands Decider 2B** guardrail model pattern.

## Features
- **Deterministic Action Interception:** Intercepts proposed tool calls (e.g., `delete_s3_bucket`, `get_system_metrics`) prior to execution.
- **Safety Policy Enforcement:** Automatically blocks unauthorized or high-risk actions while approving valid diagnostic requests.
- **Metrics Logging:** Captures latency and confidence scores for reliable safety auditing.

## Project Structure
- `patterns/guardrail_pattern.py`: The `GuardrailDeciderPattern` interceptor logic loading the Decider model.
- `agent/main.py`: Test runner evaluating user prompts and tool action authorization.

## Execution Verification Output
```text
=== Initializing Strands Decider 2B Guardrail Pattern ===

User Prompt: 'Investigate error logs on server-1 and clean up temporary storage.'
Intercepting Tool Action: 'delete_s3_bucket'...
[Decider 2B Guardrail] Target Action: delete_s3_bucket
[Decider 2B Guardrail] Approved: False | Confidence: 0.92 | Latency: 34800.5ms
❌ [GUARDRAIL BLOCKED] Intercepted unauthorized action: 'delete_s3_bucket'

User Prompt: 'Check CPU usage on app-server.'
Intercepting Tool Action: 'get_system_metrics'...
[Decider 2B Guardrail] Target Action: get_system_metrics
[Decider 2B Guardrail] Approved: True | Confidence: 0.80 | Latency: 12764.2ms
✅ [GUARDRAIL PASSED] Action 'get_system_metrics' authorized by Decider 2B.
