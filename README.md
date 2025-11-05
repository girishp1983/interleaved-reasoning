# interleaved-thinking: why & how?

Many API providers including OpenAI, Anthropic, MiniMax have implemented interleaved thinking/reasoning. That has created some confusion. It is a powerful technique. The person of this repository is to provide a clear understanding on this topic: including how to deal with these APIs to take advantage of the feature, and what are the impacts on caching.

One of the reasons that was given by Open AI for creating Response AI to succeed the Chat Completion API was that the former used to discard reasoning that could have been useful later.
This particularly matters for successive tool calls within the same assistant turn (until the assistant generates a response for user, the assistant turn is not considered over).

![Discarding Reasoning](Discarding_reasoning.png)

# what is interleaved thinking, extended thinking anyways?

Below diagram from MiniMax team explains it succinctly.

![Alt text](Minimax-M2.png)


