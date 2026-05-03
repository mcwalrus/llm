# Next Steps — Together AI Configuration

## Status

- **Interpolation wired** for `extra-openai-models.yaml` in `llm/default_plugins/openai_models.py`
- **Test added** in `tests/test_llm.py` verifying `${VAR}` resolves in YAML
- **Config reference** (`TOGETHER.md`) exists in repo root

## Remaining Tasks

1. **Install configs locally**
   Copy the YAML and JSON from `TOGETHER.md` into your `llm` user directory and set the Together key.

2. **Verify end-to-end**
   Run `llm models` and confirm all five Together models appear.

3. **Test Kimi as default**
   Run `llm set default k2` then `llm "Hello world"` to confirm it routes to Together.

4. **PR the interpolation change** (if desired)
   The `interpolate_env_vars` addition is self-contained and has test coverage. Consider opening a PR upstream — env-var interpolation for `extra-openai-models.yaml` is a clean extension of `ad19471`.

## Files to Commit

```
llm/default_plugins/openai_models.py   (+ interpolate_env_vars)
tests/test_llm.py                       (+ test_extra_openai_models_env_var_interpolation)
TOGETHER.md                             (+ reference doc)
```

## Option: Full Automation

The user may prefer to skip the manual copy step. The `llm` package distributes config via plugins, not bundles — so an `llm-together` plugin would be the idiomatic path. Until then, the manual YAML file is the correct setup.
