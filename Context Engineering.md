The practice of architecting the systems that manage a [[Large Language Model]]'s [[Context]].

An LLM's context window is one of the biggest determining factors for the quality of it's output. At it's most basic level, an LLM predicts the next word in a piece of text. In most production systems, however, an LLM has to face the same walls a human would (authorization, networking, API management, etc.) before content generation even comes into the picture.

Let's say we were interacting with an [[AI Agent]] through a chat interface in a typical ecommerce website. If the agent's context window were to be filled with the system's entire architecture, from database schema to authentication to available API endpoints all the way up to the current user's login session, the model would hallucinate from the first [[Prompt]].

A context window can look anything like the following:

![[Context Window]]

Notice how before even the first prompt is made, easily half of the context window can already be in use.

---

This is where context engineering comes into play. A good agentic system takes care of limiting context window sizes to reasonable levels through a variety of strategies.

## Orchestrator pattern

Quoting from Anthropic, "most agent workloads have two very different jobs inside them: a small amount of planning and judgement, and a large amount of mechanical reading and doing".

The idea behind the orchestrator pattern is to split the two workloads. A stronger, frontier model plans the research and synthesizes a given prompt while cheaper "[[Subagents]]" take care of the real work, based on whatever plan was crafted.

Let's say you wanted to analyze long, complex clinical protocol files. Any one of these files could have flowcharts, tables, diagrams, images, you name it. 

One approach could be to give a strong LLM the entire file at once, and ask it to provide you a JSON file mapping each protocol to its pages, a summary, and other metadata. This approach could work with small files, but what if the files grew to thousands of pages? Between image processing and text generation you would run out of context quick.

Using the orchestrator pattern, we could tell the stronger model to do a quick pass through the entire file with a simpler task: "**Walk through the file and every time you encounter 10 protocols send the respective page ranges to a sub-agent for analysis**". If we had a file that was 100 pages long with 80 protocols, the orchestrator would offload work to 8 different subagents.
	Not only do we establish basic separation of concerns, but by the time each subagent is done with it's work we could then reutilize the orchestrator agent as a judge, validating whether the subagent's job is truly finished or not (see [[Loop Engineering]]). 