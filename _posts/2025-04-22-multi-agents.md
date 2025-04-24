---
title: Is your multi agent systems really multi agentic?
date: 2025-04-22
excerpt: In this post, we will explore the concept of multi agent LLM systems, distinguishing between true multi agent systems and what are essentially modular single-agent systems.
permalink: /posts/2025/04/multi-agents/
categories:
  - research
tags:
  - LLM
  - agents
  - multi agent
---

Recent agents-sdk announcements from [OpenAI](https://openai.github.io/openai-agents-python/) and [Google](https://google.github.io/adk-docs/) has sparked a renewed interest in AI _agents_ - systems that can plan, observe, reason, and act in various environments. Beyond single agents, there's also a growing excitement around **multi agent** systems, where multiple LLM-powered entities collaborate to solve complex tasks. This post explores the current state of multi agent LLM systems, what makes them truly multi agentic, and why this matters.

## LLM Agents

To understand multi agent systems, we first need to understand what constitutes an LLM agent. At its core, an LLM agent

- Has instructions that sets the LLM behavior
- Uses an LLM as its planning and reasoning engine
- Can interact and observe an environment through tools/APIs
- Maintains some form of memory or context

The original promise of LLMs was models that could understand and generate text. The agentic breakthrough came when these models were paired with reasoning, tools that let them interact with the world, turning passive language generators into active agents that could search the web, write and execute code, and interact with other systems.

To remphasize the obvious, an agent, at the moment, is just prompt (instructions), tools, and possibly specific resources (e.g. RAG vector stores).

<figure class="half">
	<a href="/images/multi/agent_concept.png"><img src="/images/multi/agent_concept.png" alt="Basic LLM agent architecture"/></a>
	<figcaption>A simplified view of an LLM agent combining a language model with tools and memory</figcaption>
</figure>

## Multi Agent Promise

A natural next step is to create systems of multiple agents working together. This is the point at which, several folks mistake systems that are really just modular single agent systems as multi agent.

Why care about this terminology? Because lack of clear distinction affects how we think about these systems, what we expect from them, and how we design them.

Let's clarify what does NOT automatically make a system multi agentic.

### 1. Breaking down into Subtasks

Many so-called _multi agent_ systems are simply implementing good software engineering; breaking a complex process into smaller, more manageable subtasks. For example, a system might have:

- A module that retrieves information
- A module that analyzes the retrieved information
- A module that formats a response

Here, we would call an LLM for each module. But this really doesn't make it multi agent. This is just a single agent with moduarity in instructions and tools available to the LLM. Notice how in such systems the conversation context is shared across the different modules.

### 2. Specialized roles

Another common pattern is designating different LLM instances to different expertise.

- A _planning agent_ that creates task sequences
- A _research agent_ that finds information
- A _writing agent_ that writes a report

Given our definition of agent, it would be reasonable to think this constitutes a multi agent system. Are they though? What happens if I replace each _agent_ by a function call that completes the same task? Would they still be called multi agent?

The difference here is that of being _stateful_ i.e., maintaining context across multiple interactions. If your agent can be replaced by a tool call then is it really an agent?

### 3. Different LLMs

Some systems use different underlying LLMs based on the task requirements. For example, consider a system that uses

- GPT o-series model for complex reasoning
- Claude Sonnet for coding tasks
- Gemini models for search based tasks

Would it be fair to call this system multi agentic? Probably not.
The use of different LLMs merely amounts to leveraging different capabilities in these models. What if we get a new model that is single handedly the best across all tasks? So now when you use this model across the board, your multi agent system all of a sudden gets downgraded to a single agent system.

### 4. Parallel processing

Running multiple instances of similar processes and combining their outputs (like having multiple search summarizers and then merging them) is an ensemble approach. But are they multi agentic? This pattern of design is again a software design choice. If I replace the parallel calls with sequential process and perform the ensemble, the output is really not that much different (except for the latency).

## What makes a system Multi Agentic?

So if these common patterns don't constitute multi agency, what does? I have laid down the hints already. The key differentiating factor is **persistent private state that affects cross-agent interactions**.

For a system to exhibit interesting multi agent behaviors, each agent needs:

1. **Private internal state** that persists between interactions with other agents.
2. The ability to **maintain history and memory** across multiple invocations.
3. Some form of **private goals or priorities** that may or may not align perfectly with other agents.
4. The capacity for **emergent social behaviors** through repeated interactions.

Let me illustrate this with a concrete example:

### Example:

Consider a system with a coding agent and a review agent (written in pseudo-code):

**This is NOT a Multi Agent System:**

```python
function coding(requirement):
    code = coding_agent(requirement)
    review = review_agent(code, requirement)
    if review is negative:
        code = coding_agent(requirement, review)
        review = review_agent(code, requirement)
    return code, review

```

In this approach, the coding_agent (review_agent) starts fresh each time, with no memory of previous code (review). The agents here can be replaced with a function call and the system will remain the same.

**This would be a Multi Agent System:**

```python
class CodingAgent:
    def __init__(self):
        self.code_history = []
        self.observed_patterns = {}

    def code(self, requirement, review=None):
        # Code based on both requirement, current review, history of previous code
        # Update internal observations about recurring reviews
        # Return code

class ReviewAgent:
    def __init__(self):
        self.review_history = []
        self.observed_patterns = {}

    def review(self, code, requirement):
        # Review based on both current code and history of previous reviews
        # Update internal observations about recurring issues
        # Return review

function coding(requirement):
    coding_agent = CodingAgent()
    review_agent = ReviewAgent()

    code = coding_agent.code(requirement)
    review = review_agent.review(code, requirement)
    if review is negative:
        code = coding_agent.code(requirement, review)
        review = review_agent.review(code, requirement)
    return code, review

```

In the multi agent approach, the reviewer, for instance, maintains its own persistent state across multiple code reviews. It might identify patterns in the coder's behavior that inform future reviews, develop _opinions_ about certain coding practices, and have a relationship with the coder that evolves over time.

This fundamental distinction that, agents maintain their own internal states that persist across interactions is what creates multi agent scenarios. This leads to several interesting properties:

1. **Evolving relationships** - Agents can develop _trust_ or other social dynamics
2. **Private knowledge** - Agents have information not accessible to other agents
3. **Behavioral adaptation** - Agents can change strategies based on observed patterns

Persistence creates the possibility for behaviors that couldn't arise in modular systems. For example, in negotiations between our multi agents, behaviors like reciprocity, grudges, or trust can naturally develop.

<figure>
	<a href="/images/multi/state_persistence.png"><img src="/images/multi/state_persistence.png" alt="Comparison of what is and not a multi agent system"/></a>
	<figcaption>Left: Agents are just function calls. Right: A multi agent system with persistent state that affects future interactions.</figcaption>
</figure>

## Asynchronous Communication

Beyond persistent state, another level of multi agency comes from asynchronous communication patterns. In current systems, agent interactions are synchronous - one agent calls another and waits for a response. The next step in multi agent systems will include:

- Agents that operate independently without waiting for responses
- Messages from interactions can arrive at any time
- Agents decide whether and how to respond to incoming messages
- Multiple conversations can happen simultaneously

This asynchronous pattern creates much more complex and interesting dynamics, similar to how humans interact in social environments.

## Am I just being picky? Why should you care?

You might wonder why I'm concerned about this terminology distinction. There are a few reasons:

1. **Design clarity** - Understanding what makes a system multi agentic helps us design better systems
2. **Appropriate expectations** - Prematurely labeling systems as _multi agent_ creates misleading expectations
3. **Research focus** - By clarifying the boundaries of multi agent systems, we can focus research on the most promising directions
4. **Computational efficiency** - Multi agent systems will require rethinking computational complexities

## Conclusion

There's nothing wrong with modular single-agent systems - they're often the right solution for almost all problems that AI are being tasked to solve today. But by conflating agency, we risk missing out on the interesting phenomenas that can emerge from systems of multiple agents with persistent private states interacting over time.

As we continue to develop LLM-based systems, I hope we'll be more precise in our terminology and more intentional in our design choices. There's a fascinating space of possibilities in multi agent systems that we've only begun to explore, one where **the complexity of the whole exceeds the sum of its parts**.
