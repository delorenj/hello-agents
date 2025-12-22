# Context Engineering Supplementary Knowledge

## Introduction

Why has context engineering become hot again recently? It originates from a conversation between Chroma founder and CEO Jeff on the Len Space [podcast](https://youware.app/project/7529x70z4p).
Chroma is the open-source leader in the vector database field. Even the famous Voyager paper uses it.
The title of CEO Jeff's conversation is about the concept of "RAG is dead." In the video, he clearly explained the limitations of traditional RAG and the importance of context engineering today.

![alt text](./images/Extra02-figures/image-1.png)

In this chapter, we will first comprehensively explain the concept of "context engineering", and at the end of the article, we will discuss our views on "RAG is dead."

## What is Context Engineering?

We can make an analogy: Agents are like a [new type of operating system](https://www.youtube.com/watch?si=-aKY-x57ILAmWTdw&t=620&v=LCEmiRjPEtQ&feature=youtu.be&ref=blog.langchain.com). LLMs are like CPUs, and their [context windows](https://docs.anthropic.com/en/docs/build-with-claude/context-windows?ref=blog.langchain.com) are like RAM, serving as the model's working memory. Like RAM, LLM context windows have [limited capacity](https://lilianweng.github.io/posts/2023-06-23-agent/?ref=blog.langchain.com) and cannot handle context from various sources. Context engineering is like an operating system managing the CPU's RAM, managing the LLM's context window and deciding what content to fill in and when. [Karpathy summarized it well](https://x.com/karpathy/status/1937902205765607626?ref=blog.langchain.com):
_"Context engineering is... the subtle art and science of filling the context window with just the right information for the next step."_

![llm_context_engineering](https://blog.langchain.com/content/images/2025/07/image-1.png)

## [The Concept of Context Engineering](https://blog.langchain.com/context-engineering-for-agents/)

![alt text](./images/Extra02-figures/image-2.png)

Context is everything the model "sees". The model doesn't just respond to questions based on the prompt we input; there is other information that cooperates to generate responses. Context engineering serves as an umbrella term for several different context types:

- **Instructions Context**: Prompts, memory, few-shot examples, etc. (prompt engineering), including:
  - System prompts: Define AI's role, behavioral guidelines, and response style
  - User instructions: Describe specific tasks and requirements
  - Few-shot examples: Input-output examples to help understand expected format
  - Tool descriptions: Specifications and usage instructions for functions or tools
  - Format constraints: Requirements for output format and structure

- **Knowledge Context**: Facts, knowledge bases, etc. (RAG), including:
  - Domain knowledge: Factual information from specific industries or specialties
  - Memory: User preferences, historical interactions, and conversation logs
  - Knowledge base: Relevant information retrieved from databases or knowledge bases
  - Real-time data: Dynamically updated current state information

- **Tools Context**: Tool descriptions and feedback from tool calls (agent), including:
  - Function call results: API responses or query results
  - Tool execution status: Success, failure, or error feedback
  - Multi-step tool chains: Dependencies and data transfer between tools
  - Execution history: Records and results of tool calls

### Example - Smart Assistant for a Travel App

![alt text](./images/Extra02-figures/image-5.png)

To clearly distinguish these four concepts, let's set up a unified practical scenario and see how each method solves this problem.

**Scenario: A Smart Assistant for a Travel App**

**User Requirement:** "Help me plan a three-day family trip to Beijing. We are two adults and one 5-year-old child, interested in history and culture, and also want some relaxing and fun activities. Our total budget is 8,000 yuan."

---

#### 1. Prompt Engineering

This is the most basic and direct method. Its core is **how to ask a language model (LLM) a good question**, expecting it to give the best answer based solely on its internal general knowledge base.

*   **Core Idea:** Optimize the instructions (Prompt) input to the model to make it output results that better meet expectations.
*   **How It Works:**
    1.  Developers or users carefully construct all requirements into a detailed prompt.
    2.  Send this prompt directly to a general large language model (such as GPT-4).
    3.  The model relies entirely on its internal knowledge up to its training date (e.g., 2023) to answer.

*   **Example:**
    ```
    You are a professional travel planner. Please design a detailed itinerary for a three-day family trip to Beijing.
    
    # Family Members
    - 2 adults
    - 1 5-year-old child
    
    # Interests
    - History and culture (Forbidden City, Great Wall, etc.)
    - Relaxing and fun children's activities
    
    # Budget
    - Total budget not exceeding 8,000 RMB. Please provide a rough cost estimate.
    
    # Output Requirements
    - Daily itinerary (morning, afternoon, evening)
    - Transportation suggestions
    - Dining recommendations (including child-friendly restaurants)
    - Budget breakdown
    ```

*   **Limitations:**
    *   **Outdated information:** Cannot provide real-time ticket prices, opening hours, or latest traffic information.
    *   **Inaccurate information:** Budget estimates may be very rough because it doesn't know current hotel and flight prices.
    *   **Lack of personalization:** Cannot make recommendations based on users' historical preferences.
    *   **Confidently wrong:** May fabricate non-existent "children's parks" or restaurants.

---

#### 2. Retrieval-Augmented Generation (RAG)

To solve the "outdated knowledge" problem of prompt engineering, RAG introduces **external knowledge bases**.

*   **Core Idea:** Before generating an answer, first retrieve relevant information from a specific, trusted database, then provide this information along with the user's question to the model.
*   **How It Works:**
    1.  **Knowledge base preparation:** Prepare in advance a database containing the latest travel guides, attraction introductions, hotel lists, and restaurant reviews (such as a bunch of PDFs, web pages, or database records).
    2.  **Retrieve:** When users ask questions, the system first searches the knowledge base for document fragments related to "Beijing family travel" and "historical and cultural attractions."
    3.  **Augment:** Combine the retrieved information (e.g., "The latest ticket price for the Forbidden City is 60 yuan, closed on Mondays," "Beijing Universal Studios is a popular family project") with the user's original question to form a new, richer prompt.
    4.  **Generate:** Send this augmented prompt to the LLM to generate an itinerary based on these "fresh" materials.

*   **Example:**
    The system finds three pieces of text in its internal knowledge base: A) Opening hours and ticket prices from the Forbidden City's official website; B) A blog about "visiting the Temple of Heaven with kids"; C) A list of "Beijing family-friendly hotels."
    Then, it instructs the LLM: "Based on the following information: [content of text segments A, B, C], plan a three-day Beijing family trip for the user with a budget of 8,000 yuan."

*   **Limitations:**
    *   **Passive response:** It can only answer based on the information you provide; it cannot actively perform tasks. It cannot "check" flights, only use flight information "available" in your database.
    *   **One-way interaction:** After completing one retrieval and generation, it ends; it cannot perform multi-step reasoning and action.
    *   **Knowledge base dependence:** Effectiveness heavily depends on the quality and update frequency of the knowledge base.

---

#### 3. Agent

Agents evolve AI from a "Q&A bot" to an **"actor" that can think and use tools**.

*   **Core Idea:** Give the model a "reasoning-action loop" (Reasoning-Action Loop), allowing it to autonomously plan steps and use external tools (such as APIs) to complete complex tasks.
*   **How It Works:**
    1.  **Think and Plan:** The LLM (as the Agent's brain) receives user requirements and first thinks: "To complete this task, I need to: 1. Check flight and hotel prices; 2. Check attraction tickets; 3. Plan routes; 4. Compile into an itinerary."
    2.  **Choose Tool (Action):** It decides to use the first tool: `search_flight_api(from="Shanghai", to="Beijing", date="...")`.
    3.  **Observe Results (Observation):** The API returns flight prices: 5,000 yuan.
    4.  **Think Again:** "Flights cost 5,000, leaving 3,000 in budget. I need to find hotels with nightly rates below 800 yuan."
    5.  **Act Again:** Use tool `search_hotel_api(city="Beijing", price_max=800, family_friendly=true)`.
    6.  This loop continues until it collects all necessary information and finally completes the plan.

*   **Example:**
    This assistant works like a real human assistant:
    *   "Okay, I'm checking for you... I found that flights to Beijing next Friday cost about 5,000 yuan."
    *   "Considering the budget, I've screened several highly-rated family hotels priced at 600-800 yuan/night."
    *   "Forbidden City tickets have been checked through `ticket_api`; children are free. I've added this information to the itinerary."

*   **Limitations:**
    *   **Complex and unstable:** Agent behavior paths are not fixed; it may make mistakes (such as getting stuck in loops, misusing tools), making debugging and control difficult.
    *   **High cost:** Each step of thinking and tool calling may be an LLM API call, resulting in higher costs.

---

#### 4. Context Engineering

Context engineering is **a more macro and rigorous discipline** that focuses on **how to build the optimal "context window" for models (whether simple RAG or complex Agents)**. It is an optimization and sublimation of all the above methods.

*   **Core Idea:** Carefully design and orchestrate all information entering the model's context (instructions, retrieved data, historical conversations, tool outputs, etc.) to achieve the most efficient and reliable output. It is a science about "what to feed" and "how to feed."
*   **How It Works:**
    It is not an independent system type, but a methodology for optimizing RAG and Agents. Back to the travel planning example:
    1.  **Gather Stage:**
        *   **Parallel retrieval:** Not just retrieving from the travel guide library (RAG), but also simultaneously:
            *   Calling `weather_api` to check Beijing's weather for the next few days.
            *   Calling `events_api` to check if there are special children's exhibitions or activities.
            *   Retrieving from the user profile database (CRM) that "this user booked museum tickets on their last trip."
            *   Multi-path search for the user's vague request for "relaxing and fun activities," including "Beijing amusement parks," "Beijing Science and Technology Museum," "performances suitable for children."
    2.  **Glean & Compact Stage:**
        *   **Reranking:** It discovers that the weather forecast shows rain on the second day, so it lowers the priority of outdoor Great Wall visits and increases the recommendation weight for indoor science museums.
        *   **Compression:** It doesn't throw a long hotel review article at the model but extracts key information: "This hotel has a children's play area and provides cribs."
        *   **Formatting:** It integrates all the collected, messy information (weather, flights, user preferences, attraction introductions) into a highly structured, concise JSON object.
    3.  **Final Delivery:** Finally, it delivers this "perfect" context package to the Agent's brain (LLM), with instructions like: "Please generate the final itinerary for the user based on this verified, organized structured data `[JSON object]`."

*   **Example:**
    The output of context engineering is not the itinerary directly for users, but an optimized "battle map" for the model. Because of context engineering optimization, the Agent's work becomes extremely simple and efficient. It doesn't need to laboriously trial and error step by step but can directly perform final planning generation based on a perfect brief.

#### Summary Comparison

| Concept | Core Idea | How It Works | Limitations |
| :--- | :--- | :--- | :--- |
| **Prompt Engineering** | Ask the right question | Carefully design a perfect Prompt | Outdated knowledge, cannot interact with the external world |
| **RAG** | Provide reference materials | Retrieve relevant information from knowledge base before asking | Passive response, cannot execute tasks, depends on knowledge base |
| **Agent** | Grant action capability | Use "think-act" loop to use tools and complete tasks | Complex, unstable, high cost |
| **Context Engineering** | Build perfect input | Systematically collect, filter, compress, and format all information to provide optimal context for the model | It's a methodology/discipline, not a specific system; implementation is complex |

Simply put, they are progressive in capability:
*   **Prompt Engineering** is a **conversationalist**.
*   **RAG** is a **conversationalist with a reference book**.
*   **Agent** is an **assistant** who can make phone calls, search online, and book tickets for you.
*   **Context Engineering** is the **chief of staff** behind this assistant, responsible for collecting and organizing all intelligence in advance to ensure the assistant makes the wisest decisions.

## Why Did Context Engineering Emerge?

![alt text](./images/Extra02-figures/image-3.png)

As LLMs become better and better at reasoning and tool calling, interest in Agents has grown significantly. Agents interweave LLM calls with tool calls, typically for long-running tasks. Agents use tool feedback to decide the next action.

However, long-running tasks and accumulated tool call feedback mean Agents typically use a large number of tokens. This can lead to many problems: possibly exceeding context window size, increasing cost/latency, or degrading Agent performance.

As context windows get longer, we originally thought "throwing all conversation history and materials into the model" would solve memory problems. But experiments show that reality is far more complex than imagined. As context length grows, models find it increasingly difficult to maintain information accuracy and consistency, behaving like "**memory rot**."

![alt text](./images/Extra02-figures/image-4.png)

This phenomenon is called Context Rot in Chroma's research—performance "corrosion" of models in long contexts. This is the fundamental reason for the birth of the Context Engineer role: someone needs to combat and repair this "context rot" through pruning, compression, reorganization, and retrieval augmentation to maintain reliable performance within limited attention resources.

## Context Challenges

Context challenges mainly exist in [four aspects](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html?ref=blog.langchain.com), described as:

- Context Poisoning - When a hallucination enters the context
- Context Distraction - When the context overwhelms the training
- Context Confusion - When superfluous context influences the response
- Context Clash - When parts of the context disagree

### Context Poisoning: When a Hallucination Makes It into the Context

Context Poisoning refers to hallucinations (i.e., incorrect or fabricated information generated by the model) or other errors entering the context window and being repeatedly referenced, thereby embedding misinformation and causing agent performance to derail. This "poisons" key parts such as objectives or summaries, making the model stubbornly fixate on impossible or irrelevant goals, leading to repetitive, meaningless behavior.

### Context Distraction: When the Context Overwhelms the Training

Context Distraction occurs when the context grows too long (e.g., exceeding 100,000 tokens), causing the model to over-rely on historical details while ignoring its pre-training knowledge or ability to generate novel solutions. This triggers repetitive actions rather than creative problem-solving, and performance degrades before the context window is full.

When models face hundreds of thousands of tokens of input, they cannot uniformly remember all information like a hard drive. Experiments find that streamlined input (only a few hundred tokens) actually performs better than complete input (tens of thousands of tokens). Research results show that model performance on streamlined versions is significantly better than complete versions. This indicates that when input is too long with too much noise, even the most advanced models struggle to capture key information.

### Context Confusion: When Superfluous Context Influences the Response

Context Confusion refers to irrelevant or redundant information (such as redundant tool definitions) being included in the context, forcing the model to consider it, thereby producing suboptimal responses. Even if the extra content is harmless, it dilutes focus and reduces quality. In real conversations and materials, there is often "noise" that is semantically similar but irrelevant. In short contexts, models can distinguish, but in long contexts, they are more easily misled. This requires someone to filter and denoise the context, allowing the model to focus on truly relevant information. In long contexts, models not only need to find relevant information but also distinguish "which is the correct needle, and which are just distractions."

### Context Clash: When Parts of the Context Disagree

Context Clash is a more severe form of confusion, referring to conflicting information in the context (such as new tools or facts contradicting existing content), thereby undermining reasoning, usually because the model locks onto early assumptions. This is more destructive than mere irrelevance: "This is a more problematic version of Context Confusion: the bad context here isn't irrelevant, it directly conflicts with other information in the prompt." In multi-step interactions, early errors propagate, and the model relies on flawed premises.

Lack of "computer-like" reliability: We hope LLMs achieve consistent quality output. Even for the simplest copying tasks, models make errors with long inputs. It is not a character-by-character symbolic processor but a probabilistically-driven language generator. Therefore, we cannot expect it to process long contexts as precisely as a database or computer; we must use structured design to compensate.

Therefore, effective context window management and context engineering are essential.

## Context Engineering Strategies

The previous section mentioned that context faces so many challenges, so how to overcome them? This relies on context engineering. Among them, context engineering strategies are mainly divided into four types: write (store), select, compress, and isolate.

![alt text](./images/Extra02-figures/image-6.png)

### Write Context

**Write context** means saving it outside the context window to help Agents perform tasks.
Mainly divided into two types:
- **Scratchpad**
A temporary workspace that records the model's intermediate reasoning, making the thought process visible. Taking notes on the "scratchpad" is a way to persistently save information when Agents execute tasks. The idea is to save information outside the context window so that Agents can use it.
- **Memory**
Agents combine new context with existing memories, process them, and write updated memory.

![alt text](./images/Extra02-figures/image-8.png)

### Select Context

When the amount of information grows, how to select is more important than how to store. Selecting context means picking out truly relevant parts from all available information sources and putting them into the window each time the model is called.

Specific contexts available for selection include:

- **Scratchpad:** The temporary scratchpad mentioned above, serving as the model's "working memory" space for recording reasoning processes, intermediate results, and thinking steps. In multi-step tasks, the model can write current reasoning status, completed sub-tasks, pending problems, etc., into the scratchpad for reference and strategy adjustment in subsequent steps.

- **Memory:** Includes two levels: short-term memory and long-term memory. Short-term memory stores historical conversations and context information in the current session, ensuring conversation continuity; long-term memory stores user preferences, historical interaction patterns, personalized settings, and other cross-session persistent information, helping the model provide more personalized and consistent service experiences.

- **Tools:** In Agent systems, tools themselves are a type of context. When the model calls APIs, plugins, or external functions, it must understand the tool's description (including function description, parameter requirements, return format, etc.) and choose the right tool in appropriate scenarios. Feedback results after tool calls also serve as new context input, guiding the model's next decision. Tool availability, execution status, and call history are all important context information.

- **Knowledge:** Mainly refers to external knowledge bases in RAG (Retrieval-Augmented Generation). Includes structured data (such as database tables), unstructured documents (such as technical documentation, product manuals), semantic retrieval results in vector databases, etc. These external knowledge compensate for the timeliness limitations of model training data and insufficient knowledge coverage, enhancing the accuracy and professionalism of model answers through dynamic retrieval of relevant information.

### Compress Context

![alt text](./images/Extra02-figures/image-9.png)

Compressing context involves retaining only the tokens needed to perform the task, optimizing the use efficiency of the context window by reducing redundant information.

#### Context Summarization

**Conversation Summarization:**
In long multi-turn interactions, fully retaining all historical conversations quickly consumes the context window. Through conversation summarization technology, early conversation turns can be compressed into concise summary form, retaining key information (such as user preferences, important decisions, pending problems, etc.) while discarding redundant pleasantries and repetitive content. This maintains conversation continuity while leaving sufficient space for new interactions.

**Tool Summarization:**
Tool calls often return large amounts of raw data (such as complete API responses, database query results, etc.). Through tool summarization, the most relevant result fields can be extracted and retained, filtering out metadata, debugging information, and other unnecessary content. For example, a weather API may return detailed meteorological parameters, but after summarization, only core information such as temperature and weather conditions is retained, significantly reducing token consumption.

#### Context Pruning

**Rule-based Pruning:**
Hard-coded heuristics can be used to proactively delete outdated or low-priority context. Common strategies include:
- Removing older messages from conversation history, retaining the most recent N conversation turns
- Removing completed sub-task records, only retaining information related to current tasks
- Deleting expired temporary data or invalidated tool call results

**Intelligent Pruning:**
More advanced methods can dynamically select which context fragments to retain based on relevance scores. Through semantic similarity calculation or importance scoring, information most relevant to the current task is prioritized, automatically eliminating historical content with low relevance.

### Isolate Context

Isolating context involves splitting context to help Agents perform tasks.

#### Multi-Agent Architecture

![alt text](./images/Extra02-figures/image-10.png)

**Separation of Concerns:**
Split complex large tasks into multiple independent sub-tasks, each responsible for a specific sub-task. This design follows the single responsibility principle, allowing each Agent to focus on a specific domain, improving overall system maintainability and scalability.

**Agent Isolation Characteristics:**
Each sub-Agent has independent resources and configuration:
- **Dedicated toolset:** Each Agent can only access specific tools needed to complete its task, avoiding tool proliferation leading to choice difficulty
- **Independent system instructions:** System prompts customized for specific tasks, clarifying the Agent's role positioning and behavioral guidelines
- **Isolated context windows:** Each Agent maintains its own context space, without interference, avoiding pollution from irrelevant information

**Agent Collaboration Mechanism:**
Multiple Agents communicate and transfer data through clear interfaces. The master Agent or routing layer is responsible for task assignment and result integration, forming collaborative workflows.

#### Execution Environment Isolation

![alt text](./images/Extra02-figures/image-11.png)

**Separation of Context and Execution:**
Isolate the code execution environment from the LLM's context window. The LLM doesn't need to directly access all raw output data from tools.

**Processing Layer Design:**
Add a processing layer between tool execution and LLM:
- Tools execute in independent sandbox environments, producing raw output
- Processing layer filters, transforms, and summarizes raw results
- Only refined key information is passed to the LLM context

This isolation improves both security and reduces token consumption, allowing the LLM to focus on high-level decision-making rather than low-level detail processing.

### Summary

The four actions of context engineering—write, select, compress, isolate—are not scattered techniques but a systematic method.
They respectively address problems of information loss, information redundancy, information overload, and information conflict.
When these four strategies are systematically executed, Agents can operate stably in complex environments.

## Implementation of Context Engineering

Use LangSmith and LangGraph for context engineering. For specific content in this section, please refer to Chapter 9.

## Summary and Reflection: RAG is Dead?

![alt text](./images/Extra02-figures/image.png)

Jeff mainly criticized traditional RAG for forcibly bundling three different concepts—"Retrieval, Augmented, Generation"—together, leading to conceptual confusion and practical ambiguity. Re-examining RAG from the context engineering perspective, it can be broken down into clearer steps:

**Traditional RAG vs Context Engineering Perspective (Advanced RAG):**

| Stage | Traditional RAG | Context Engineering Method |
|------|---------|----------------|
| **Retrieval** | Simple vector similarity search | Hybrid retrieval: combining vector retrieval, keyword matching, reranking, and other strategies |
| **Filtering** | Usually missing or rudimentary | Intelligent filtering: eliminating redundant, outdated, or task-irrelevant content |
| **Ranking** | Based on single similarity score | Multi-dimensional ranking: considering relevance, freshness, credibility, and other factors, prioritizing the most critical information |
| **Evaluation** | Lack of systematic evaluation | Building golden datasets, quantitatively evaluating retrieval quality, answer accuracy, and context utilization efficiency |

**Core Improvements:**
- **Diversification of retrieval strategies:** No longer relying on single vector retrieval, but combining dense retrieval, sparse retrieval, semantic reranking, and other technologies based on task characteristics
- **Context quality priority:** Emphasizing that what is fed to the LLM is not "the more the better" but "the more precise the better," ensuring high-quality context through filtering and ranking
- **Closed-loop optimization:** Continuously iterating optimization of retrieval strategies, filtering rules, and ranking algorithms through evaluation datasets, forming a measurable, improvable engineering process

This perspective transforms RAG from a black-box process into a decomposable, optimizable context engineering problem, making it more operational and scalable.

Therefore, context engineering is both a systematic engineering practice and an art requiring tradeoffs. It requires us to accurately judge the following 4 questions among massive information:

- **Write** — What information should be included in the context?
- **Select** — What content is most relevant and necessary?
- **Compress** — What can be summarized or simplified?
- **Isolate** — What needs to be separated into independent spaces?

Only by understanding these questions can we achieve effective context engineering, realizing the perfect combination of art and engineering.

![alt text](./images/Extra02-figures/image-12.png)

## References

Canghai Jiusu (沧海九粟). Context Engineering: Key Technology for Optimizing Agent Performance[EB/OL]. (2025-07-10)[2025-10-21]. https://www.bilibili.com/video/BV1w3GNzeEHb/?spm_id_from=333.1387.upload.video_card.click&vd_source=0f47ed6b43bae0b240e774a8fd72e3e4

Drew Breunig. How Long Contexts Fail[EB/OL]. (2025-06-22)[2025-10-21]. https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html?ref=blog.langchain.com

Latent.Space, Jeff Huber, Swyx. RAG is Dead, Context Engineering is King[EB/OL]. (2025-08-19)[2025-10-21]. https://www.latent.space/p/chroma
