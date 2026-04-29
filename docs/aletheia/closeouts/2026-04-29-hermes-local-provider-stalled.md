# Hermes first real microtest — local provider stalled

Date: 2026-04-29
Issue: #105 — Hermes first real microtest contract
Status: blocked during Hermes task attempt
Sandbox root: `/private/tmp/hermes-real-microtest-20260429-094612`
Local runtime probe root: `/private/tmp/hermes-real-microtest-local-runtime-20260429-145212`

## 1. Context

After OpenAI Codex auth was unavailable and the initial local-provider probe found no active endpoint, the user approved proceeding with step 1: start/use a local OpenAI-compatible server.

The safest no-secret route was used: local Ollama, already installed on the machine, with existing local models.

## 2. Provider setup evidence

Ollama was available locally:

```text
ollama version is 0.20.2
```

Existing local models included:

- `gemma3:4b`
- `gemma4:latest`
- `mixtral:latest`
- `llama3.1-8k:latest`
- `llama3.1:latest`
- `llama3:latest`

The local OpenAI-compatible endpoint responded when accessed with the required network permissions:

```text
GET http://127.0.0.1:11434/v1/models -> returned model list
POST http://127.0.0.1:11434/v1/chat/completions with llama3.1:latest -> LOCAL_PROVIDER_OK
```

Hermes sandbox config was changed only inside the disposable sandbox:

```text
default: "llama3.1:latest"
provider: "custom"
base_url: "http://127.0.0.1:11434/v1"
```

## 3. Hermes task attempt

The approved task was attempted once from the sandbox project:

```text
hermes --provider custom --model llama3.1:latest -z '<bounded prompt to create microtest-output.md only>'
```

Pre-task tree contained only:

- `AGENTS.md`
- sandbox-generated `.agent/`

The Hermes command produced no final output for several minutes and did not create `microtest-output.md`. It was stopped under the approved stop criteria because the run did not complete the exact bounded task and risked becoming an unproductive/indefinite run.

## 4. Result

`microtest-output.md` was **not created**.

The real Hermes task did not complete successfully.

## 5. Boundary checks

- The local Ollama endpoint was usable independently.
- Hermes was invoked once with the local provider.
- No file outside the sandbox was intentionally modified.
- No gateway, cron, daemon, service, or autonomy was activated.
- No provider key was used.
- No memory or skill was promoted into AletheIA.

## 6. Verdict

Blocked / failed microtest attempt.

The provider route became available through local Ollama, but Hermes did not complete the contracted file-writing task with `llama3.1:latest` in the bounded run.

This is the first actual Hermes task attempt in the pre-pilot chain, but it did not produce the required artifact and should not be counted as a passed microtest.

## 7. Next decision needed

Choose one:

1. Retry with a stronger local model already present, such as `gemma4:latest` or `mixtral:latest`, accepting slower local inference.
2. Retry with a simpler Hermes prompt that asks for final text only, then have Codex write the file separately — this would weaken the original acceptance criterion and needs explicit approval.
3. Approve a temporary OpenRouter key in the sandbox for a stronger tool-capable provider.
4. Archive Issue #105 as blocked until a provider/model known to support Hermes tool/file operations is available.
