# Extended thinking & extended thinking with interleaved-thinking for tool calling: why & how?

Many API providers including OpenAI, Anthropic, MiniMax have implemented extended thinking and furthermore interleaved thinking for tool calls. 

That has created some confusion. It is a powerful technique. 
The purpose of this repository is to provide a clear understanding on this topic: including how to deal with these APIs to take advantage of the features, and what are the impacts on caching.

One of the reasons that was given by Open AI for creating Responses API to succeed the Chat Completion API was that the former used to discard reasoning that could have been useful later. 
With Responses API, reasoning is retained and it can be referenced in successive calls.
The performance difference between the two APIs, all things remaining same can be significant. 
Quote: "On a more rigorous benchmark like SWE-bench, including reasoning items led to about a 3% improvement for the same prompt and setup."

This particularly matters for successive tool calls within the same assistant turn (**Definition**: if assistant is generating tool calls, the assistant turn is not considered over until it generates final response for the user). 
Successive tool calls are not shown in this diagram, but we will see them in the next section.

![Discarding Reasoning](Discarding_reasoning.png)

# Visualizing scenarios: no-thinking, extended thinking and extended thinking wiht interleaved thinking for tool calls?

Below diagram from MiniMax team explains the three scenarios succinctly.

In the interleaved thinking scenario the model is evaluating tool responses, and thinking again before it generates the next tool call. This way it does tool calling in a strategic or intelligent manner.
**This improves the performance of your agentic application vastly.**

![No Thinking, Extended Thinking and Extented Thinking with Interleaved Thinking for Tool calling](MiniMax-M2.png)

# How the request-response messages will look like?
If you want to see actual messages exchanged, please review files with the following names in the current directory:

Extended-Thiking.json

Extended-Thiking-with_interleaved.json

I extracted them from langfuse for my DeepResearch Application that uses these APIs.

# How to deal with reasoning blocks?

If you use official OpenAI Responses API or Anthropic Messages API, they make it easy to send back all the reasoning block. The API intelligently retains only reasoning blocks for the ongoing turn (recall the definition of assistant turn). 
The moment the next turn begins when user sends a new message, reasoning blocks for the previous turn are ignored (you should still send them, as it keeps implementation clean).

# Impact of extended thinking with interleaved thinking for tool calls?

OpenAI and Anthropic support caching. But MiniMax is yet to support caching - it is coming soon.

The APIs (OAI, Anthropic) automatically remove reasoning blocks from the previous turns, as mentioned before. That behaviour can be best understood from the diagram below.
This can result in cache miss. Please read text on the diagram carefully.

Now Anthropic provides an option to retain the previous turn's reasoning blocks, so that cache is not invalidated. However, this has downside of filling up your context sooner.
So, no-free lunch. There is a trade off.

![Impact on Caching](OpenAI.png)




