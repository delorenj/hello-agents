# LLM & VLM & Agent Interview Questions Summary

This document is a collection of interview "fundamentals" organized during the preparation for the 2025 autumn recruitment.

The author primarily applied for positions including: Large Model Algorithm Engineer, Agent Engineer, AI Development Engineer, Algorithm Evaluation Engineer, etc., with interviews mainly at major domestic internet companies. Therefore, the depth and breadth of questions in this document are centered around the requirements of these positions, covering the entire technology stack from LLM/VLM core theory, to RAG/Agent application development, to RLHF alignment technology and model/Agent evaluation. All questions are compiled from real experiences in multiple online technical interviews.

**Usage Recommendations**
This document is for learning and reference purposes only. For best results, it is strongly recommended to think independently about each question first, try to construct your own answers, and then compare with the reference ideas provided in the document to identify gaps. Know the what, and more importantly, know the why. Rote memorization is the least efficient approach.

Wishing everyone a smooth job search and success in landing your desired offer!

---

### 1. LLM Fundamentals

1.  Please explain in detail how the self-attention mechanism in the Transformer model works. Why is it more suitable for processing long sequences than RNN?
2.  What is positional encoding? Why is it necessary in Transformers? Please list at least two implementation methods.
3.  Please introduce ROPE in detail. What are its advantages and disadvantages compared to absolute positional encoding?
4.  Do you know the differences between MHA, MQA, and GQA? Please explain in detail.
5.  Please compare several common LLM architectures, such as Encoder-Only, Decoder-Only, and Encoder-Decoder, and explain the types of tasks they are each best suited for.
6.  What are Scaling Laws? What relationship do they reveal between model performance, computational resources, and data volume? What guidance do they provide for LLM development?
7.  In the inference phase of LLMs, what are some common decoding strategies? Please explain the principles, advantages, and disadvantages of Greedy Search, Beam Search, Top-K Sampling, and Nucleus Sampling (Top-P).
8.  What is tokenization? Please compare BPE and WordPiece, two mainstream subword segmentation algorithms.
9.  What do you think is the biggest difference between NLP and LLM? What are their similarities and differences?
10. What are L1 and L2 regularization? In what scenarios are they appropriate to use?
11. "Emergent abilities" is a highly discussed phenomenon in large models. How do you understand this concept? At what model scale does it typically appear?
12. Are you familiar with activation functions? What activation functions are commonly used in LLMs? Why are they chosen?
13. How do Mixture of Experts (MoE) models effectively scale up model parameters without significantly increasing inference costs? Please briefly describe how they work.
14. When training an LLM with hundreds of billions or trillions of parameters, what are the main engineering and algorithmic challenges you face? (For example: memory, communication, training instability, etc.)
15. Which open-source frameworks are you familiar with? Have you studied papers on Qwen or Deepseek? What are the main innovations in them?
16. What recent cutting-edge papers on LLMs have you read? Discuss their methods, the problems they address, the approaches they propose, and the comparative experiments conducted.

---

### 2. VLM Fundamentals

1.  What are the core challenges of multimodal large models (such as VLMs)? Specifically, how to achieve effective alignment and fusion of information from different modalities (such as vision and language)?
2.  Please explain how the CLIP model works. How does it connect images and text through contrastive learning?
3.  How do models like LLaVA or MiniGPT-4 connect a pre-trained vision encoder with a large language model (LLM)? Please describe the key architectural design.
4.  What is visual instruction tuning? Why is it a key step in enabling VLMs to have good conversation and instruction-following capabilities?
5.  When processing multimodal data such as videos, what additional problems do VLMs need to solve compared to static images? (For example, how to represent temporal information?)
6.  Please explain the meaning of Grounding in the VLM field. How do we evaluate whether a VLM can accurately map text descriptions to specific regions in an image?
7.  Please compare at least different VLM architecture paradigms (such as shared encoder vs. cross-modal attention fusion) and analyze their pros and cons.
8.  In VLM applications, how do you handle high-resolution input images? What computational and model design challenges does this bring?
9.  VLMs also encounter "hallucination" problems when generating content, but how does this manifest differently from pure text LLMs? Please provide examples.
10. Besides image captioning and visual question answering (VQA), what other cutting-edge or promising application directions can you list for VLMs?
11. Have you done any fine-tuning related to VLMs? What model?

---

### 3. RLHF Fundamentals

1.  Compared with traditional SFT, what core problems does RLHF aim to solve in language models? Why is SFT alone insufficient to achieve the desired "alignment" goal?
2.  Please elaborate on the three core stages of the classic RLHF process. In each stage, what are the inputs, outputs, and key objectives?
3.  In the RM training stage, we typically collect pairwise comparison data rather than having human annotators directly assign an absolute score to responses. What do you think are the main advantages and potential disadvantages of this approach?
4.  The design of the reward model is crucial. How is its model architecture typically chosen? What is its relationship to the LLM we ultimately want to optimize? What is the commonly used loss function when training the reward model? Please explain the mathematical principles behind it (for example, you can explain it in conjunction with the Bradley-Terry model).
5.  In the third stage of RLHF, PPO is the most mainstream reinforcement learning algorithm. Why choose PPO instead of other simpler policy gradient algorithms (such as REINFORCE) or Q-learning algorithms? What key role does the KL divergence penalty term in PPO play?
6.  If the coefficient β of the KL divergence penalty term is set too large or too small during PPO training, what problems will each cause? How would you adjust this hyperparameter through experiments and observations?
7.  What is "reward hacking"? Please give an example in a specific LLM application scenario and discuss several possible mitigation strategies.
8.  The RLHF process is complex and unstable. In recent years, some alternatives have emerged, such as DPO. Please explain the core idea of DPO and compare its main differences and advantages with traditional RLHF (based on PPO).
9.  Imagine that your trained RLHF model performs excellently in offline evaluation with high reward model scores, but after going online, user feedback shows that its answers are becoming increasingly "formulaic," flattering, and lacking in information. What do you think could be the reasons? From what aspects would you analyze and solve this problem?
10. Do you know Deepseek's GRPO? What are the main differences from PPO? What are the advantages and disadvantages?
11. Have you heard of GSPO and DAPO? How do they differ from GRPO?
12. How to solve the credit assignment problem? What are the differences between token-level and seq-level rewards?
13. In addition to human feedback, we can also use AI's own feedback for alignment, i.e., RLAIF. Please discuss your understanding of RLAIF. What are its potential and risks?

---

### 4. Agent

1.  How do you define an LLM-based agent? What are the core components it typically consists of?
2.  Please explain the ReAct framework in detail. How does it combine reasoning and action to complete complex tasks?
3.  In Agent design, "planning capability" is crucial. Please discuss what mainstream methods currently exist to endow LLMs with planning capabilities? (For example, CoT, ToT, GoT, etc.)
4.  Memory is a key module of Agents. How do you design short-term and long-term memory systems for Agents? What external tools or technologies can be leveraged?
5.  Tool Use is an effective way to extend Agent capabilities. Please explain how LLMs learn to call external APIs or tools? (You can explain from the Function Calling perspective)
6.  Please compare two popular Agent development frameworks, such as LangChain and LlamaIndex. How do their core application scenarios differ?
7.  When building a complex Agent, what do you think is the main challenge?
8.  What is a multi-agent system? What advantages does having multiple LLM Agents work collaboratively have over a single Agent? What new complexities does it introduce?
9.  When an Agent needs to perform tasks in a real or simulated environment (such as robotics, games), what is the essential difference from purely software tool-based Agents?
10. How do you ensure that an Agent's behavior is safe, controllable, and aligned with human intent? What alignment methods exist in Agent design?
11. Are you familiar with the A2A framework? What is the difference from ordinary Agent frameworks? Mention one most critical difference.
12. What Agent frameworks have you used? How did you make the selection? What are the evaluation metrics for your final scenario?
13. Have you fine-tuned Agent capabilities? How was the dataset collected?

---

### 5. RAG

1.  Please explain how RAG works. Compared to directly fine-tuning LLMs, what problem does RAG mainly solve? What are the advantages?
2.  What are the key steps in a complete RAG pipeline? Please describe the entire process in detail from data preparation to final generation.
3.  When building a knowledge base, text chunking strategy is crucial. How would you choose the appropriate chunk size and overlap length? What are the tradeoffs?
4.  How do you choose a suitable embedding model? What metrics are used to evaluate the quality of an embedding model?
5.  Besides basic vector retrieval, what other techniques do you know that can improve RAG retrieval quality?
6.  Please explain the "Lost in the Middle" problem. What phenomenon does it describe in RAG? What methods can mitigate this problem?
7.  How do you comprehensively evaluate the performance of a RAG system? Please propose evaluation metrics from both retrieval and generation stages.
8.  In what scenarios would you choose to use a graph database or knowledge graph to enhance or replace traditional vector database retrieval?
9.  Traditional RAG process is "retrieve then generate." Are you aware of more complex RAG paradigms, such as multiple retrievals during generation or adaptive retrieval?
10. What challenges might a RAG system face in actual deployment?
11. Are you familiar with search systems? What are the differences from RAG?
12. Do you know or have used any open-source RAG frameworks such as Ragflow? How to choose the appropriate scenario?

---

### 6. Model Evaluation & Agent Evaluation

1.  Why do traditional NLP evaluation metrics (such as BLEU, ROUGE) have significant limitations in evaluating the generation quality of modern LLMs?
2.  Please introduce several widely used comprehensive LLM benchmarks in the industry and explain their respective focuses. (For example: MMLU, Big-Bench, HumanEval)
3.  What is "LLM-as-a-Judge"? What are the advantages and potential biases of using an LLM to evaluate another LLM's output?
4.  How do you design an evaluation scheme to measure specific capabilities of an LLM, such as "factuality/hallucination level," "reasoning ability," or "safety"?
5.  Why is evaluating an Agent more difficult and complex than evaluating a foundational LLM? What are the differences in evaluation dimensions?
6.  What benchmarks specifically designed for evaluating Agent capabilities are you aware of? How are test environments and tasks typically constructed in these benchmarks?
7.  When evaluating an Agent's task completion, besides the correctness of the final result, what other process metrics are worth paying attention to? (For example: efficiency, cost, robustness)
8.  What is red teaming? What role does it play in discovering security vulnerabilities and biases in LLMs and Agents?
9.  When conducting human evaluation, how do you design reasonable evaluation criteria and processes to ensure objectivity and consistency of evaluation results?
10. How do you continuously monitor and evaluate the performance of a deployed LLM application or Agent service to respond to potential performance degradation or behavioral drift?

---

### 7. LLM Prospects & Development

1.  How far do you think current LLMs are from Artificial General Intelligence (AGI)? What is the most critical missing capability?
2.  From GPT-4 to future models, where do you think multimodal fusion will go? Is it just the combination of text and images, or will it expand to more sensory dimensions?
3.  How do you view the competition and coexistence of open-source and closed-source model ecosystems? What are their respective advantages, and how will they evolve in the future?
4.  As model capabilities strengthen, the "world model" or intrinsic simulation capabilities of LLMs are also receiving attention. How do you understand this concept? What significance does it have for achieving higher-order reasoning and planning?
5.  "Data" is the fuel for training LLMs. What role do you think high-quality artificially synthesized data will play in future model training?
6.  Embodied AI, the combination of LLMs and robots, is considered the next wave of AI. How do you think LLMs will empower robots, and what challenges will it bring?
7.  Personalization is an important direction for LLM applications. In achieving highly personalized Agents or assistants, how should we balance effectiveness, privacy, and security?
8.  Do you think the Transformer architecture will dominate this field for a long time? Or do you see potential in new architectures like State Space Models (SSM, such as Mamba)?
9.  Looking ahead 3-5 years, in which industry or field do you think LLM and Agent technologies are most likely to achieve disruptive applications first? Why?

---

### 8. Others

1.  What do you think is the biggest bottleneck limiting Agent capabilities and adoption? (For example: model capability, cost, reliability, or something else?)
2.  In the past six months, which paper or open-source project about Agents impressed you the most? Why?
3.  How do you view "emergent abilities" in the Agent field? Should we pursue more powerful foundation models or more sophisticated Agent architectures?
4.  In the next 1-2 years, in which industry or scenario do you think Agent technology is most likely to achieve large-scale commercial deployment first?
5.  If you were free to explore, what kind of Agent would you most want to create to solve what problem?
6.  For beginners who want to enter the Agent field, what advice would you give them? What technologies should they focus on learning?
7.  In summary, what do you think are the core qualities a top-tier AI Agent engineer should possess?
8.  Do you use AI regularly? What for? If I want to use AI, for example in the coding field, what advice do you have for me?
