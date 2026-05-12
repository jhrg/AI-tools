# Using Agentic AI in Software Development and Maintenance

In this document we describe five tasks that can be performed using agentic AI (AI or agents, hereafter). Those tasks
are a 'deep dive,' problem analysis, refactoring, planning development and plan implementation. Each of those five tasks
are described below. 

In this document we assume that the AI tools are primarily Large Language Models (LLM) and that they are not being used
in a web browser but are either integrated into an IDE ot use a standalone application or terminal/CLI tool.
Furthermore, we assume that these AI tools can read code in one or more git repositories (repos). The AI tool's ability
to process a large 'prompt' (the number of tokens of context) is assumed to be substantial. We also a


## What's Common to all the Tasks

There are some aspects of AI use that are common to all of the tasks. For any use of AI, it is important to document the
intent - why you are doing this - and the agents reasoning. Documenting the reason for using AI is no different than
documenting the reasons for any objective in an engineering project. However, it is easy to get swept up by the relative
ease with which previously time consuming tasks can be accomplished now using AI. Additionally, for all of the tasks,
the agents should produce documentation and that describes the reasoning it used to produce the output for the task.
This is different from no-AI development; people don't have to be told to explicitly document why they thought about
reading a particular source file (although sometimes that does show up in a bug ticket), but it's important to have an
AI tool document its reasoning when evaluating the correctness of the output. Thus, when using AI, process documentation
is more complex and more important.

### Context

AI tools used for software development need substantial context to produce results that fit into a professional
engineering workflow. See [LLMs and Context](LLMs-and-Context.md) for general information about Large Language Models
and context. The context for Codex Spark has about 128K tokens (about 95,000 English words) and Claude Code has about
200K (about 150,000 English words). Thus, the overall context of a given prompt - all the information that the LLM uses
to build a response, can be substantially larger than the a three or four sentence input. 

There are several ways that a developer can provide additional information to any/every use of an AI tool. For example,
Codex working within an IDE will read files named 'AGENTS.md' and include them in the context of every prompt made
withing the repo in which that file resides. For more information about the AGENTS.md files see the [AGENTS GitHub
repo](https://github.com/agentsmd/agents.md)

(This I copied from Google, but it seems like a good summary)
#### Key Aspects of AGENTS.md
* Purpose: Acts as a "system prompt" for AI, containing instructions that the AI cannot infer simply by reading the
  code.
* Contents: Typically includes project-specific guidelines like setup commands, testing instructions, coding styles, and
  dependency management.
* Precedence: Agents generally look for AGENTS.md at the root directory, but it can also be used in subdirectories for
  more specific context.
* Structure: It should be concise and organized, generally targeting 150 lines or fewer to maintain high AI performance.

#### Best Practices
* Be Specific: Include actionable, unique instructions that AI cannot easily discover on its own.
* Use Markdown: Use clear headings and code blocks (```) to make it easy for agents to parse and copy commands.
* Maintain it: Update the file as your project's technology stack or coding guidelines change.

You can use the AGENTS.md file to establish guardrails for AI tools For example, you can instruct the agents to always
document their reasoning unless told otherwise, to always save plans to a specific directory, et cetera.

See the [AGENTS.md](AGENTS.md) file for an example.

### Skills

Skills are markdown documents, scripts and other information that are added to a prompt - they become part of the
request context - when a prompt includes a trigger phrase for the skill or if the skill is explicitly referenced.

For an example skill, see [the OPeNDAP skill written by Ed Hartnett](skills/opendap).

More info TBD

### Prompts

The prompt given to the AI tool should be concise. But, if you want a particular kind of output and some aspect ot the
context does not include that, be sure the prompt does. One way is to include one or more examples of the kind of output
you want. Suppose you want CppUnit-based unit tests - say so and include an example that uses the templated main()
function we use with most of our C++ code.

The context of the prompt is described in [LLMs and Context](LLMs-and-Context.md) but one thing that is not covered in
that document is that every new 'chat' (i.e., session) has no knowledge of previous sessions. Tha context that is common
to a series of sessions is the AGENTS.md documents, the contents of repo, we documents that are referenced by AGENTS.md,
skills, and any thing in 'Memory.' Memory, see [LLMs and Context](LLMs-and-Context.md), is information that is
explicitly carried over from session to session. 

## The Deep Dive

A _Deep Dive_ instructs a LLM like Codex or Claude code to read over the files in a repo and provide a description of
how the code works. How various classes or functions are used, what th software it intended to do or be used for, etc. A
deep dive can also point out inconsistencies between the documentation and the actual code. Here's an example from our
software from a deep dive of the NcML handler:


> #### NcML Module Deep Dive
> 
> ##### Scope
> 
>This document is a code-oriented deep dive on `modules/ncml_module`. It focuses on the implementation in that directory
>and ignores the test layout and test differences from other modules, per request.  
> ...  
> One important documentation drift is that the old `modules/ncml_module/README` still says only `union` and `joinNew`
> are implemented, while the current code has full `joinExisting` classes in the build and dispatch path.

You can instruct an AI like Codex to update the documentation, but that can be tricky to check - you need to make sure
that it was correct in its reading of the source code and of the README. Still, this is only one example fo the whole
NcML deep dive and over all the result is very useful. 

Later section will describe how to use these tools to edit code and update existing documentation to match the edits.

Don't skip over this. The output of a correctly done deep dive is a markdown document and that, in turn can be used by
the AI tools to direct other behaviors. The next topic, _Problem Analysis_ can directly benefit from the Deep Dive
document.


## Problem Analysis

### Investigating Specific issues

### When You Just Have a Hunch

## Refactoring

## Developing a Plan

## Implementing a Plan

## Terms

Agentic AI refers to autonomous systems that can set goals, plan complex tasks, and take actions to achieve them with
limited human supervision. Unlike passive generative AI, which waits for prompts, agentic AI acts proactively in
real-time to solve problems, often utilizing multiple agents working together.

AGENTS.md is an open, markdown-based format used by AI coding agents like Codex to receive project-specific context and
instructions. Placed in the repository root, it enables consistent behavioral rules, testing instructions, and dev
environment guidance, which reduces orientation time and improves output quality.

Context is the sum total of the tokens the LLM processes to produce a given response.

Tokens a token is similar to a lexeme in the scanners and parsers discussed in a class on compilers. For an LLM, a token
is a word or a portion of a word. For example, _run_ is a token, _running_ might be a token but the LLM input parser
might break that down into several tokens: _run_, _n_, _ing_. It's not that important to know exactly how a LLM
tokenizes its input, but it is important to realize that all LLMs have a maximum number of tokens they can process.

Codex (OpenAI) is classified as an agentic AI tool, specifically designed as a full-fledged AI agent for coding,
software engineering tasks, and autonomous workflow management. It is designed to understand context, generate code, and
execute tasks across software projects.

Claude Code (Anthropic) is another example an an agentic AI software development tool.
