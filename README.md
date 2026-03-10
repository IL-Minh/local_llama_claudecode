# llama.ccp with Homebrew on MacOS
## Installing llama.cpp via Homebrew

```bash
brew install llama.cpp
```

That's it! Homebrew handles the build with Metal support automatically.

## Python env & model download (with `uv`)

```bash
uv add huggingface_hub hf_transfer

uv run hf download unsloth/Qwen3.5-9B-GGUF \
    --local-dir unsloth/Qwen3.5-9B-GGUF \
    --include "*UD-Q4_K_XL*"
```

## Start llama-server

When installed via Homebrew, the binary is just `llama-server` (available globally), not `./llama.cpp/llama-server`:

```bash
llama-server \
    --model unsloth/Qwen3.5-9B-GGUF/Qwen3.5-9B-UD-Q4_K_XL.gguf \
    --alias "unsloth/Qwen3.5-9B" \
    --temp 0.6 \
    --top-p 0.95 \
    --top-k 20 \
    --min-p 0.00 \
    --port 8001 \
    --kv-unified \
    --cache-type-k q8_0 --cache-type-v q8_0 \
    --flash-attn on --fit on \
    --ctx-size 131072
```

---

## How this differs from the Unsloth Claude Code guide

Based on the official guide at [`https://unsloth.ai/docs/basics/claude-code`](https://unsloth.ai/docs/basics/claude-code), this setup makes a few MacBook Pro M3‑friendly changes:

- **Install method**: use Homebrew (`brew install llama.cpp`) instead of cloning/building `llama.cpp` with `cmake`.
- **Environment management**: use `uv` (`uv add`, `uv run …`) instead of global `pip` / `pip3` installs.
- **Model choice**: use **Qwen3.5‑9B** with **UD‑Q4\_K\_XL** quant, which comfortably fits a **16GB M3 MacBook Pro**, instead of the heavier 27B/35B variants from the original guide.
- **Local paths**: models are downloaded into a project‑local `unsloth/` folder in this repo, and `llama-server` points directly at that relative path.

All other llama.cpp flags (temperature, top‑p, KV cache settings, port, etc.) follow the Unsloth recommendations.

--- 
# Removing

```bash
brew uninstall llama.cpp
```

If you also want to clean up the downloaded model files, you'd remove those manually since Homebrew doesn't manage them:

```bash
rm -rf unsloth/
```

And if you want to remove the Python packages too:

```bash
uv remove huggingface_hub hf_transfer
```


# Models
- unsloth/Qwen3.5-9B-GGUF/Qwen3.5-9B-UD-Q4_K_XL.gguf
***
- 