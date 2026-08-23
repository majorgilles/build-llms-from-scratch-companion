# Agent coding guidelines

These guidelines apply to this repository unless a more specific `AGENTS.md` exists in a subdirectory.

## Python typing

- Add type annotations to all function and method parameters and return values, including `__init__`, `__len__`, and `__getitem__`.
- Type class attributes and empty collections when their element type cannot be inferred from the assignment.
- Type reusable helpers, datasets, models, callbacks, and public module boundaries.
- Use precise built-in generics such as `list[int]`, `dict[str, int]`, and `tuple[Tensor, Tensor]`.
- Prefer concrete library types when they are stable and available, such as `tiktoken.Encoding` or `torch.Tensor`.
- Do not annotate obvious local variables when their type is directly inferable from the assigned value.
- Avoid `Any` unless a third-party boundary genuinely has no useful type information.
- Keep annotations beginner-readable; introduce `Protocol`, `TypeVar`, or complex aliases only when they provide clear value.

## Learning notebooks

- Keep examples beginner-readable and split distinct concepts into focused cells.
- Add concise comments that explain intent or non-obvious behavior rather than restating syntax.
- Add a nearby Markdown cell for each new concept, explaining its purpose, inputs, outputs, and connection to the next step.
- Let each notebook read as one continuous chapter. Do not insert repetitive checkpoint cells between sections; consolidate takeaways into one chapter summary Markdown cell at the end.
- Keep Markdown, comments, type annotations, and executable code synchronized.
- Treat `glossary.md` as the source of truth for terminology and identifiers used in generated code, comments, docstrings, and Markdown. Update the glossary before introducing a new synonym for an existing concept.
- Reuse established terminology and variable names across notebooks; do not rename the same concept from chapter to chapter without a documented semantic reason.
- Use `num_tokens` for the current sequence-length dimension in model and attention tensors. Reserve `context_length` for the configured maximum supported sequence length; do not use `seq_len` or `sql_len` for `num_tokens`.
- When a request is documentation- or typing-only, do not change executable behavior.
- Validate notebook JSON and Python code-cell syntax after editing.
