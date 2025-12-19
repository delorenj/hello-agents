# Hello-Agents Datawhale Frequently Asked Questions (FAQ)

> This document is based on Q&A organized from the 2024-12-01 live broadcast and the first course construction Q&A collection, serving as extended reading for Datawhale's "Hello-Agents Zero-to-Hero Introduction" course.
> It is recommended to study this together with the main course documentation:
> - 🔗 [Course Documentation](https://datawhalechina.github.io/hello-agents/#/)
> - ⌛️ Course Videos (Coming soon)

---

## 1. Multi-Agent Architecture and Parallel Scheduling

**Q1. How do multi-agent systems achieve "multi-threaded parallelism"? For parallel steps decomposed by the task planning Agent, how can multiple execution Agents claim tasks themselves and automatically handle dependencies? Are there ready-made frameworks?**

- Key points:
  - First, the "task planning Agent" performs task dependency decomposition to form parallel and dependent sub-tasks.
  - The execution layer can be designed as multiple specialized Agents, each only handling the sub-tasks they are responsible for.
  - Parallel scheduling is usually implemented through queues/API polling, etc. Most scenarios require business-specific customization; there is no completely universal one-click solution.
- Course guidance: Chapters on multi-agent paradigms and system architecture (classic paradigms + framework practice).

---

## 2. Framework Ecosystem and Communication Protocols

### 2.1 Mainstream Frameworks and Hello-Agents' Positioning

**Q2. What are the current mainstream Agent frameworks? What problems does Hello-Agents mainly solve?**

- Key points:
  - A systematic comparison of mainstream frameworks and their update frequency is concentrated in Chapter 6, not repeated here.
  - **Hello-Agents' positioning**: Focuses on teaching and learning, emphasizing "clear structure + practical + easy to generalize," helping beginners establish a complete Agent knowledge and practice framework.
- Course guidance: Chapter 6 "Framework Development Practice."

**Q7. Hello-Agents looks very comprehensive. If we want to use it for production, what capabilities roughly need to be supplemented?**

- Key points:
  - The framework itself leans toward "teaching + usable." Real production deployment requires secondary development combined with business needs.
  - Core enhancement points usually include:
    - Business knowledge modeling and scenario understanding;
    - More robust logging, monitoring, evaluation, and rollback mechanisms;
    - Performance optimization and cost control.
- Course guidance: Framework section + project practice chapters.

### 2.2 Hello-Agents Integration with LangGraph / Other Frameworks

**Q4. How to use Hello-Agents in combination with LangGraph? Who calls whom?**

**Q11 / Q15. Want to know how to use A2A to combine Hello-Agents with LangGraph?**

- Key points (combined answer):
  - Can use **A2A protocol + Agent Card** to expose "an Agent in one framework" as a "remote capability" callable by another framework.
  - Analogy to Function Calling: LangGraph nodes can call Agents in Hello-Agents as "remote functions," and vice versa.
- Course guidance: Chapter 10 "Agent Communication Protocols." Chapter 6 "Framework Development Practice."

**Q17. Will the learning process introduce DeepResearch and other open-source/ready-made frameworks?**

- Key points:
  - DeepResearch belongs to Workflow content and will be supplemented later.
  - Framework-related content is concentrated in **Chapters 5 and 6**, covering everything from "single framework" to "multi-framework ecosystem."
- Course guidance: Chapters 5 and 6 (frameworks and application cases).

**Q18. When writing Agents with LangGraph, it feels more like a "large model workflow script." What should be considered for real project implementation? Is this covered in the course?**

- Key points:
  - From "script" to "project" requires more consideration of: module boundaries, configuration management, monitoring and evaluation, error recovery, and team collaboration.
  - Course **Part 4** specifically guides you to build a complete project from scratch for practical reference.
- Course guidance: Part 4 "Building Projects."

### 2.3 Communication Protocols: A2A & ANP

**Q5. A2A and ANP were explained too quickly. Can they be explained in more detail with code examples?**

- Key points:
  - The course will progressively unfold from "motivation → abstraction → protocol fields → code examples."
  - Recommended supplementary reading: Datawhale's "Hands-on Agent Application Development" chapter on "Agent Communication Protocols" (explained by ANP community authors).
- Course guidance: Chapter 10; can be linked to Datawhale official documentation in README's "Extended Reading."

**Q6. For practical applications, is local deployment or direct API usage recommended?**

- Key points:
  - Course **Chapter 7** provides both routes: local deployment and cloud API.
  - Learning phase: Prioritize API (lower barrier); consider local only when cost control or offline deployment is needed.
- Course guidance: Chapter 10

Related course guidance:
- 🔗 Chapter 5 "Building Agents with Low-Code Platforms." [Jump to Chapter 5](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter5/Chapter5-Building-Agents-with-Low-Code-Platforms.md)
- 🔗 Chapter 6 "Framework Development Practice." [Jump to Chapter 6](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter6/Chapter6-Framework-Development-Practice.md)
- 🔗 Chapter 7 "Building Your Agent Framework." [Jump to Chapter 7](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter7/Chapter7-Building-Your-Agent-Framework.md)
- 🔗 Chapter 10 "Agent Communication Protocols." [Jump to Chapter 10](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter10/Chapter10-Agent-Communication-Protocols.md)

---

## 3. Course Positioning, Learning Path, and Target Audience

**Q9. Where will future courses be released?**

- Key points:
  - Github repository (course code and documentation)
  - Datawhale Bilibili (videos)
  - Datawhale official website (course entry portal)

**Q10. Is it suitable for complete beginners?**

- Key points:
  - Yes, but you need to "go slower + review code breakdowns more."
  - Students without Python foundation need extra time to supplement syntax; the course itself is not completely "zero programming" difficulty.
  - Python recommendation: Datawhale's exclusive course: 🔗 [Learn Python the Smart Way](https://datawhalechina.github.io/learn-python-the-smart-way-v2/)
  - With Python basics, the recommended learning path is:
    1. Environment setup, preface
    2. 🔗 [Chapter 1: Introduction to Agents](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter1/Chapter1-Introduction-to-Agents.md)
    3. 🔗 [Chapter 2: History of Agents](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter2/Chapter2-History-of-Agents.md)
    4. 🔗 [Chapter 3: Large Language Model Fundamentals](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter3/Chapter3-Fundamentals-of-Large-Language-Models.md)
    5. 🔗 [Chapter 4: Building Classic Agent Paradigms](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter4/Chapter4-Building-Classic-Agent-Paradigms.md)
    6. 🔗 [Chapter 5: Building Agents with Low-Code Platforms](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter5/Chapter5-Building-Agents-with-Low-Code-Platforms.md)
    7. 🔗 [Chapter 6: Framework Application Development Practice](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter6/Chapter6-Framework-Development-Practice.md)

**Q12. Chapters 1.1 and 2.1 seem similar. What are their respective focuses?**

- Key points:
  - **2.1**: Systematically reviews Agents along the development timeline, extending to cases like expert systems, leaning more toward "historical context + panoramic view."
  - **1.1**: As an opening introduction, briefly introduces basic concepts and background.

**Q13. How should working professionals study? How to use it at work after learning? What's the difference from workflow tools like n8n?**

- Key points:
  - Learning suggestion: Combine with your business scenario, prioritize creating a "small but complete" Agent application, even if it only replaces a small workflow segment.
  - Core difference from workflows (n8n, etc.):
    - Workflow: Processes and branches are basically fixed, used to solve "relatively certain structure" tasks.
    - Agent: Suitable for more complex, uncertain tasks that can make autonomous decisions during runtime (calling tools, planning sub-tasks, etc.).
- Course guidance: Concept chapters + classic paradigms and project practice sections.

**Q14. Which chapters specifically cover Agent testing and evaluation?**

- Key points:
  - There's a dedicated evaluation chapter (Chapter 12), and other chapters also form "closed-loop evaluation" practical cases.
- Course guidance: Testing and evaluation chapter + related project practice.
- 🔗 [Chapter 12](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter12/Chapter12-Agent-Performance-Evaluation.md)

**Q16. What are the minimum hardware requirements for course experiments? Is a GPU needed?**

- Key points:
  - **Agentic RL chapter**: GPU environment with ≥ 4G VRAM recommended for better experience.
  - Other chapters can be completed entirely with API; local GPU not mandatory.
- Course guidance: Agentic RL related chapters.

**Q20. Is this course suitable for students?**

- Key points:
  - Very suitable; treat it as an entry-level project in the "AI + software engineering" interdisciplinary direction.
  - Recommended to combine with your capstone project/research project to enhance practical value.
  - Capstone project results can be submitted to this project via PR:
    - 🔗 [Co-creation-projects](https://github.com/datawhalechina/hello-agents/tree/main/Co-creation-projects).

---

## 4. Knowledge and Tools: RAG / KAG / Knowledge Graphs / RL, etc.

**Q3. Is RAG necessary for building Agents?**

- Key points:
  - RAG is not a mandatory option for Agents, but a common type of "external knowledge tool."
  - Course **Chapter 8** implements a RAG solution from scratch, helping understand the differences in system design between "with RAG / without RAG."
- Course guidance: Chapter 8.
- 🔗 [Chapter 8: Memory and Retrieval](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter8/Chapter8-Memory-and-Retrieval.md)

**Q21. What's the relationship between KAG / knowledge graphs and Agents?**

- Key points:
  - KAG / knowledge graphs can be understood as a "tool" or "knowledge foundation" for Agents:
    - Agents handle decision-making and calling;
    - Knowledge graphs provide structured knowledge and retrieval capabilities.

**Q22. According to Chapter 1's classification of "learning-based Agents and LLMs-based Agents," where do RL, LLM, and RLHF fit?**

- Key points:
  - RL, LLM, and RLHF are more like **components or implementation technologies** of Agents, not separate "Agent types."
  - For example: LLMs can serve as the Agent's brain; RL/RLHF can be used to train or fine-tune the Agent's policy.

---

## 5. Performance and Context Management

**Q19. Complex tasks have very long system prompts, consuming many tokens per call, causing slow responses; this problem worsens as context grows. How to balance this?**

- Key points:
  - The key is "context pruning and management": conversation history, tool call results, system prompts, etc., should be preserved hierarchically and by priority.
  - Can reduce token pressure through "summary + memory modules + retrieval-based context."
  - Course **Chapter 9** specifically covers context processing strategies.
- Course guidance: Chapter 9.
- 🔗 [Chapter 9: Context Engineering](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter9/Chapter9-Context-Engineering.md)

---

## 6. Projects and Career Development

**Q8. Can the case projects in the course be included in resumes?**

- Key points:
  - Yes, provided you truly understand and can clearly explain:
    - What problem the project solved;
    - What Agent designs were used;
    - What specific work was done in tool calling/evaluation/deployment.
  - Recommended to use "Problem-Solution-Result" structure in resumes to describe these projects, with Github links attached.

---

## 7. Environment Configuration, Model Usage, and API Call Related Issues

**Q17. How are APIs configured in the course? Encountering call failures**

- Key points:
  - Course project model API support:
    - [Silicon Flow Inference API](https://modelscope.cn/models);
    - [Deepseek API](https://platform.deepseek.com/usage);
    - [OpenAI API](https://platform.openai.com/docs/quickstart);
    - Others...
  - Configuration process: Obtain API_KEY, MODEL_ID, BASE_URL and set in environment variable `.env` file.
  - ModelScope community model API acquisition method: https://www.modelscope.cn/models/Qwen/Qwen3-VL-8B-Instruct
    - Click on model library, find models supporting API-Inference, click to enter model details page, find API-Inference
    - ![alt text](./images/Extra04-figures/3f1b68eedc9d9e556fbb51358bf49f9d.png)
    - ![alt text](./images/Extra04-figures/e7dd177f-4867-4af0-bd0e-03771a3a040e.png)

**Q18. When implementing ReAct workflow, are there alternatives to the serpApi web search tool?**

- Key points:
  - Requires VPN; if VPN unavailable, change solution;
  - Can consider other search engines like: duckduckgo, googlesearch, etc.

**Q21. The inference model being used only supports streaming output and cannot enter the agent's subsequent loop**

- Key points:
  - DeepSeek, Qwen, and other inference models only provide streaming APIs by default; correct concatenation is needed rather than simple string concatenation (refer to Chapter 7 for specific concatenation methods)

**Q23. Not sure how to understand associating memory with knowledge base.**

- Key points:
  - My understanding: For example, agents typically have short-term and long-term memory. Short-term memory is like what we do during the day, which we can directly input to the model via context. But long-term memory is like taking notes; we can't input so much information in context at once, so we create a tool for the model to call. The model can generate a query and then retrieve from our knowledge base through RAG, i.e., long-term memory.

**Q24. Tsinghua mirror request error, 403**

- Key points:
  - Network issue, switch to USTC mirror:
    - https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
    - https://mirrors.ustc.edu.cn/anaconda/pkgs/free/

**Q25. Model API call 401 error**

- Key points:
  - Insufficient model balance, need to recharge.

## 8. Mathematical Foundations

**Q22. How to understand P(w_2∣w_1) in probability formulas**

- Key points:
  - Conditional probability in probability theory, i.e., the probability of w_2 occurring given that w_1 has occurred

## 9. Other Issues

### 9.1 Capstone Project Related

**Q26. After submitting a capstone project, how to showcase it in resume and personal repository?**

- Key points:
  - See Section 5 of [Chapter 16](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter16/Chapter16-Graduation-Project.md)
  - Recommended resume format (example):
    - "Intelligent Travel Itinerary Planning Assistant Based on Hello-Agents Framework"
      - Responsibilities: Agent role design, tool call orchestration, RAG retrieval and conversation evaluation
      - Results: Automatically generates multi-day itinerary plans, supporting budget constraints and personalized preferences
      - Link: `https://github.com/<your-id>/hello-agents/tree/main/projects/<your-folder>`
  - Key points to explain during interviews:
    - Why design the Agent structure this way;
    - What evaluation methods were used;
    - What problems were encountered (e.g., overly long context, call costs, etc.) and how you addressed them.

---
