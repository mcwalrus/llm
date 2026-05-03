# Together AI Configuration for LLM

## Checkpoint

- Variable interpolation is now wired into `extra-openai-models.yaml`
  - `llm/default_plugins/openai_models.py` imported `interpolate_env_vars` and applies it after YAML load
  - `tests/test_llm.py` gained `test_extra_openai_models_env_var_interpolation`

## Setup

### 1. API key in `keys.json`

```json
{
    "together": "${TOGETHER_API_KEY}"
}
```

Set the variable in your shell or `.bashrc`/`.zshrc`:

```bash
export TOGETHER_API_KEY="<your-together-api-key>"
```

Or store directly (no interpolation):

```bash
llm keys set together
```

### 2. `extra-openai-models.yaml`

Place in `$(dirname "$(llm logs path)")/extra-openai-models.yaml`:

```yaml
- model_id: together-kimi
  model_name: moonshotai/Kimi-K2.6
  api_base: "https://api.together.xyz/v1"
  api_key_name: together
  aliases: [kimi, k2]

- model_id: together-deepseek-v4
  model_name: "deepseek-ai/DeepSeek-V4-Pro"
  api_base: "https://api.together.xyz/v1"
  api_key_name: together
  aliases: [deepseek-v4]

- model_id: together-glm
  model_name: "zai-org/GLM-5.1"
  api_base: "https://api.together.xyz/v1"
  api_key_name: together
  aliases: [glm]

- model_id: together-minimax
  model_name: "MiniMaxAI/MiniMax-M2.7"
  api_base: "https://api.together.xyz/v1"
  api_key_name: together
  aliases: [minimax]

- model_id: together-qwen
  model_name: "Qwen/Qwen3.5-397B-A17B"
  api_base: "https://api.together.xyz/v1"
  api_key_name: together
  aliases: [qwen]
```

### 3. Set default model

```bash
llm set default k2
```

## Verification

```bash
# List models
llm models

# Verify Together models appear
llm models | grep -i together

# Quick chat with Kimi K2.6
llm "Explain the difference between Kimi and DeepSeek"
```
