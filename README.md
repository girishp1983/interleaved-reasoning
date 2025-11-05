# interleaved-thinking: why & how?

Many API providers including OpenAI, Anthropic, MiniMax have implemented interleaved thinking/reasoning. That has created some confusion. It is a powerful technique. The person of this repository is to provide a clear understanding on this topic: including how to deal with these APIs to take advantage of the feature, and what are the impacts on caching.

One of the reasons that was given by Open AI for creating Responses API to succeed the Chat Completion API was that the former used to discard reasoning that could have been useful later.
This particularly matters for successive tool calls within the same assistant turn (until the assistant generates a response for user, the assistant turn is not considered over). 
Successive tool calls are not shown in this diagram, but next one.

![Discarding Reasoning](Discarding_reasoning.png)

# what is interleaved thinking, extended thinking anyways?

Below diagram from MiniMax team explains the three scenarios succinctly.

![No Thinking, Extended Thinking and Extented Thinking with Interleaved Thinking for Tool calling](MiniMax-M2.png)

# How to deal with reasoning blocks?
If you want to see actual messages exchanged, please review files with the following names in the current directory:
Extended-Thiking.json
Extended-Thiking-with_interleaved.json

# How to deal with reasoning blocks?

If you use official Responses API or Claude Messages API, they make it easy to send back all the reasoning block. The API intelligently retains only reasoning blocks for the ongoing turn. The moment the next turn begins, reasoning blocks for the previous turn are ignored (you should still send them, as it keeps implementation clean).

# Impact of extended thinking with interleaved thinking for tool calls?

OpenAI and Anthropic support caching. But MiniMax is yet to support caching - it is coming soon.

The APIs (OAI, Anthropic) automatically remove reasoning blocks from the previous turns, as mentioned before. That behaviour can be best understood from the diagram below.
This can result in cache miss. Please read text on the diagram carefully.

Now Anthropic provides an option to retain the previous turn's reasoning blocks, so that cache is not invalidated. However, this has downside of filling up your context sooner.
So, no-free lunch. There is a trade off.

![Impact on Caching](OpenAI.png)




