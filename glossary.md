# Project glossary

This file is the source of truth for terminology and identifiers used in generated notebook code, comments, docstrings, and Markdown. Reuse these terms across chapters instead of introducing synonyms for the same concept.

## Tensor dimensions

| Canonical term | Identifier | Meaning | Avoid for this meaning |
|---|---|---|---|
| Batch size | `batch_size` | Number of independent sequences processed together; dimension `B` | `num_samples` when referring to a model batch |
| Number of tokens | `num_tokens` | Actual token count in the current input sequence; dimension `T` or `N` | `seq_len`, `sql_len`, `sequence_size` |
| Context length | `context_length` | Configured maximum number of tokens supported by the model or causal mask | Using it for the current `num_tokens` value unless they are intentionally equal |
| Vocabulary size | `vocab_size` | Number of distinct token IDs; dimension `V` | `num_words` for subword tokenizers |
| Embedding dimension | `emb_dim` | Width of each token representation and the model dimension `d_model` | `residual_stream_width` in beginner-facing material |
| Input dimension | `d_in` | Feature width accepted by a projection or reusable layer | `emb_dim` when the layer intentionally accepts a different width |
| Output dimension | `d_out` | Total feature width produced by a projection or attention module | `head_dim`; `d_out` is the combined width across heads |
| Number of heads | `num_heads` | Number of parallel attention heads; dimension `H` | `n_heads` |
| Head dimension | `head_dim` | Width assigned to one attention head; normally `d_out // num_heads` | `d_out` when discussing one head |
| Number of layers | `num_layers` | Number of Transformer blocks in the model | `n_layers` |
| Dropout rate | `dropout_rate` | Probability of dropping an activation during training | `drop_rate` |

## Token and training data

| Canonical term | Identifier | Meaning |
|---|---|---|
| Token IDs | `token_ids` | Integer IDs produced by a tokenizer |
| Input IDs | `input_ids` | Token IDs supplied to the model or one dataset example |
| Target IDs | `target_ids` | Input IDs shifted by one position for next-token prediction |
| Inputs | `inputs` | Batched model inputs when the exact representation is clear from context |
| Targets | `targets` | Batched expected next-token IDs |
| Epoch | `epoch` | One complete traversal of the training loader |
| Global optimizer step | `global_step` | Number identifying one parameter-update step across epoch boundaries |
| Examples seen | `examples_seen` | Training examples processed by optimizer steps, including repeats across epochs |
| Evaluation frequency | `eval_freq` | Optimizer-step interval between loss evaluations |
| Evaluation batches | `eval_iter` | Maximum loader batches sampled during one quick evaluation |

## Instruction data

| Canonical term | Identifier | Meaning |
|---|---|---|
| Instruction | `instruction` | Natural-language description of the task to perform |
| Optional task input | `input` | Additional text needed to complete an instruction; may be empty |
| Desired response | `output` | Reference answer used as the supervised continuation |
| Formatted model input | `model_input` | Alpaca-style instruction and optional input presented before the response |
| Desired response text | `desired_response` | Response header plus reference output appended during supervised training |

## Attention

| Canonical term | Identifier | Meaning |
|---|---|---|
| Queries | `queries` | Projected representations describing what each token seeks |
| Keys | `keys` | Projected representations used to match against queries |
| Values | `values` | Projected information combined by attention weights |
| Attention scores | `attn_scores` | Raw query-key dot products before softmax |
| Attention weights | `attn_weights` | Normalized scores produced by softmax |
| Context vectors | `context_vecs` | Weighted combinations of value vectors; use singular `context_vec` for one query |
| Causal mask | `causal_mask` | Mask preventing a query from attending to future key positions |

## Model outputs

| Canonical term | Identifier | Meaning |
|---|---|---|
| Logits | `logits` | Unnormalized vocabulary scores with shape `(batch_size, num_tokens, vocab_size)` |
| Probabilities | `probas` | Normalized values produced by softmax; sum to one across `vocab_size` |
| Sampling temperature | `temperature` | Positive scalar that controls how sharp or flat a probability distribution is before sampling |
| Top-k cutoff | `top_k` | Number of highest-logit vocabulary candidates retained before sampling |
| End-of-sequence token ID | `eos_id` | Optional token ID that signals generation should stop |
| Next-token prediction | — | Prediction made at each input position for the token immediately following that position |

## Classification data

| Canonical term | Identifier | Meaning |
|---|---|---|
| Text message | `text` | Input string classified by the model |
| Class label | `label` | Integer target associated with one input example |
| Ham | `0` | Legitimate message in the SMS Spam Collection |
| Spam | `1` | Unwanted message in the SMS Spam Collection |
| Encoded messages | `encoded_texts` | Token-ID lists produced from the text-message column |
| Padded input length | `max_length` | Fixed number of token IDs retained or padded for each classification example; must not exceed `context_length` |
| Padding token ID | `pad_token_id` | Token ID appended until each classification input reaches `max_length` |
| Number of classes | `num_classes` | Count of mutually exclusive classification targets; `2` for ham and spam |
| Class logits | `logits` | Unnormalized class scores shaped `(batch_size, num_tokens, num_classes)` |
| Last-position class logits | `last_token_logits` | Class scores read from the final input position, shaped `(batch_size, num_classes)` |
| Predicted class labels | `predicted_labels` | Highest-logit class ID for each example, shaped `(batch_size,)` |
| Classification accuracy | `accuracy` | Fraction of evaluated examples whose predicted and target labels match |
| Classification loss | `loss` | Mean cross-entropy between final-position class logits and target labels |

## Configuration terms

- Use `GPTConfig` for the validated Pydantic architecture configuration.
- Access configuration values through typed attributes such as `cfg.emb_dim`, not dictionary keys.
- Use `num_heads`, `num_layers`, and `dropout_rate` for their corresponding configuration fields.
- Use `context_length` for model capacity and `num_tokens` for the current input length.
- When matching an external API or quoted source that uses different names, state the mapping explicitly rather than silently changing local vocabulary.
