# Prompt API: Sampling Mode Presets Studio

An interactive playground, benchmarking suite, and repeatability testbed for the **Chromium Prompt API Sampling Mode Categorical Presets** (`LanguageModel.create({ samplingMode })`).

Hosted live on GitHub Pages: [https://isaacahouma.github.io/prompt-api-sampling-presets/](https://isaacahouma.github.io/prompt-api-sampling-presets/)

---

## 🌟 Overview

The **Chrome Prompt API** is transitioning from low-level sampling parameters (`temperature`, `topK`) to high-level **categorical presets** (`samplingMode`).

This studio allows developers, spec editors, and web AI researchers to:
- 🎛️ **Compare Sampling Modes in Parallel**: Inspect outputs side-by-side across all 7 categorical modes.
- 🔁 **Multi-Run Repeatability & Variance**: Run $N$ identical passes through `LanguageModel.create({ samplingMode })` to test determinism and vocabulary divergence.
- 📊 **Empirical Performance Profiling**: Measure streaming throughput (tokens/sec), output lengths, and real latency distributions.
- 🌊 **Stream & Batch Modes**: Switch between real-time token streaming (`promptStreaming()`) and atomic batch generation (`prompt()`).

---

## 🧭 The 7 Categorical Sampling Presets

| Sampling Mode | Temperature ($T$) | Top-K ($K$) | Target Use Cases |
| :--- | :---: | :---: | :--- |
| **`most-predictable`** | `0.0` | `1` | JSON extraction, classification, math, schema enforcement |
| **`predictable`** | `0.3` | `32` | Summarization, entity extraction, structured QA |
| **`slightly-predictable`** | `0.7` | `64` | Grounded dialogue, editorial rewriting |
| **`balanced`** *(Default)* | `1.0` | `64` | General chat, assistive copywriting |
| **`slightly-creative`** | `1.1` | `72` | Brainstorming, marketing copy |
| **`creative`** | `1.15` | `80` | Creative writing, storytelling |
| **`most-creative`** | `1.2` | `100` | Divergent thinking, exploratory ideation |

---

## 💻 JavaScript API Usage

```javascript
// Check availability with samplingMode
const availability = await LanguageModel.availability({
  samplingMode: "most-predictable"
});

// Create a session configured with a categorical preset
const session = await LanguageModel.create({
  samplingMode: "most-predictable",
  systemPrompt: "You are a precise technical classifier."
});

// Stream response tokens
const stream = session.promptStreaming("Classify the sentiment: 'Great battery life!'");
for await (const chunk of stream) {
  process.stdout.write(chunk);
}
```

---

## 🔗 References & Standards

- **Chromium Issue**: [crbug.com/502214118](https://crbug.com/502214118) &mdash; Prompt API Sampling Mode Categorical Presets
- **W3C WebML Prompt API Spec Discussion**: [Issue #203](https://github.com/webmachinelearning/prompt-api/issues/203)
- **Prompt API Explainer**: [W3C WebML Prompt API Explainer](https://github.com/webmachinelearning/prompt-api)

---

## 📄 License

Apache-2.0 or BSD-3-Clause (Chromium Open Source compatible).
