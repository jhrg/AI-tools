# What is Context

In LLMs, **context** means the information available to the model at the moment it generates a response.

More precisely, it is the text and other inputs the model can “see” in its current request. The model does not think in an open-ended vacuum; it predicts the next tokens conditioned on the context it has been given.

## What counts as context

For a chat model, context usually includes:

1. **The system/developer instructions**
   Rules about how the model should behave, what tools it may use, safety constraints, formatting preferences, and so on.

2. **The conversation history**
   Prior user messages and assistant replies that are still inside the active context window.

3. **The current user message**
   The immediate question or task.

4. **Uploaded or retrieved material**
   File excerpts, search results, database records, code snippets, documentation, or tool outputs that are inserted into the prompt.

5. **Structured metadata**
   Things like current date, user locale, app state, selected text, or previous tool results, when provided to the model.

## Context window

The **context window** is the maximum amount of input the model can consider at once.

It is usually measured in **tokens**, not words. A token is a chunk of text: sometimes a word, sometimes part of a word, sometimes punctuation. For example, a model with a 128k-token context window can process far more text than a model with an 8k-token window, but it still has a hard upper limit.

When a conversation or document exceeds the context window, some information must be omitted, summarized, compressed, or retrieved selectively.

## Context is not the same as memory

This distinction matters:

**Context** is what the model has access to in the current interaction.

**Memory** is information retained across interactions, if the product has such a feature and it is enabled.

A model can only use “memory” if that memory is actually provided back into the current context. Internally, the model itself is not reliably recalling your past chats unless the system supplies relevant information as part of the prompt.

## Context is not the same as training data

Training data affects the model’s learned behavior and general knowledge.

Context affects the model’s immediate response.

For example, if the training data says “the API endpoint is `/v1/foo`” but the current context includes new documentation saying “the endpoint is now `/v2/foo`,” the model should follow the current context. In practice, clear and relevant context usually overrides broad learned priors.

## Why context matters

Context determines:

* what facts the model can use;
* which instructions it should follow;
* what style or format it should produce;
* what entities pronouns refer to;
* whether it can answer from a document, codebase, or conversation;
* how much detail it can preserve across a long task.

Poor context often causes poor answers. Missing context leads to guessing. Conflicting context can lead to ambiguity or errors.

## Example

User asks:

> “Can you summarize the risks in this proposal?”

The model needs the proposal in context. Without it, it can only give a generic answer.

If the proposal text is included, the model can summarize the actual risks. If only part of the proposal fits in the context window, the answer may miss risks from omitted sections.

## Retrieval-augmented generation

In many LLM systems, relevant documents are not all placed into context upfront. Instead, the system performs **retrieval**: it searches a document store, selects relevant passages, and inserts those passages into the context.

That inserted material becomes part of the model’s working context for that response.

So, in LLM usage, **“adding context”** usually means giving the model more relevant information to condition on: documents, examples, constraints, goals, definitions, or prior decisions.
