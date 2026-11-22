# llm-glioma-molecular-subtyping

Prompts used for LLM-based molecular subtype classification of adult-type diffuse gliomas from MRI reports.

- [prompt_classification.md](prompt_classification.md) — classification only (model returns the class name).
- [prompt_classification_with_quotes.md](prompt_classification_with_quotes.md) — classification with verbatim supporting quotes (model returns a JSON object).

Both prompts share the same system-prompt preamble and label set; they differ only in the requested output format.
The same prompts were used unchanged for the reasoning-mode (thinking-enabled) runs.
