# Dify Agent Building Practical Guide:<br>Building an All-Purpose Personal Assistant from Scratch (Step-by-Step Tutorial)

<div align="center">
  <img src="https://github.com/Tasselszcx.png" width="80" height="80" style="border-radius: 50%;" />
  <br />
  <strong>Author:</strong> <a href="https://github.com/Tasselszcx">Tasselszcx</a>
  <br />
  <em>Original Tutorial | Step-by-Step Guide | Complete Practice</em>
</div>

## 1. Install Required Plugins

Before building the agent, you need to complete the necessary plugin installation and MCP configuration. As shown in Figure 1, follow the text instructions in the image to install the plugins required for this chapter step by step.

<div align="center">
  <img src="./Extra03-figures/image1.jpg" alt="Plugin Installation Diagram" width="90%"/>
  <p>Figure 1: Plugin Installation Diagram</p>
</div>

## 2. Configure MCP (Model Context Protocol)

We won't expand on the detailed principles of MCP here. Instead, we'll focus on demonstrating how to use cloud-deployed MCP services. This case uses the domestic ModelScope community MCP marketplace for demonstration. The specific steps are as follows:

**(1) Enter the ModelScope Community**: [https://www.modelscope.cn/home](https://www.modelscope.cn/home)

**(2) Register an account and log in**, as shown in Figure 2

<div align="center">
  <img src="./Extra03-figures/image2.jpg" alt="ModelScope Registration and Login Interface" width="90%"/>
  <p>Figure 2: ModelScope Registration and Login Interface</p>
</div>

**(3) Enter the Amap (Gaode Map) MCP configuration page**
   - After logging in, follow the steps shown in Figure 3 to click through to the Amap MCP configuration page
   - The page should appear as shown in Figure 4

<div align="center">
  <img src="./Extra03-figures/image3.jpg" alt="Amap MCP Entry Guide" width="90%"/>
  <p>Figure 3: Amap MCP Entry Guide</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image4.jpg" alt="Amap MCP Configuration Page" width="90%"/>
  <p>Figure 4: Amap MCP Configuration Page</p>
</div>

**(4) Enter the Amap Open Platform**: [https://console.amap.com/dev/index](https://console.amap.com/dev/index)
   - Create a new application following the text instructions in Figure 5

<div align="center">
  <img src="./Extra03-figures/image5.jpg" alt="Amap Open Platform Create New Application" width="90%"/>
  <p>Figure 5: Amap Open Platform Create New Application</p>
</div>

**(5) Create api_key**
   - As shown in Figure 6, create the api_key step by step
   - Enter the created api_key into the red box in Figure 4, and it will display configuration success
   - The successful configuration page is shown in Figure 7

<div align="center">
  <img src="./Extra03-figures/image6.jpg" alt="Create api_key Steps" width="90%"/>
  <p>Figure 6: Create api_key Steps</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image7.jpg" alt="MCP Configuration Success Page" width="90%"/>
  <p>Figure 7: MCP Configuration Success Page</p>
</div>

**At this point, the entire Amap MCP configuration is complete!**

## 3. Agent Design and Effect Demonstration

This case will create a comprehensive personal assistant covering the following functional modules:

- Daily life Q&A
- Copywriting refinement and optimization
- Multimodal content generation (images, videos)
- MCP tool integration (Amap, dietary recommendations, news and information)
- Data query and visualization analysis

The entire agent's orchestration architecture is shown in Figure 8.

<div align="center">
  <img src="./Extra03-figures/image8.jpg" alt="Agent Orchestration Architecture Diagram" width="90%"/>
  <p>Figure 8: Agent Orchestration Architecture Diagram</p>
</div>

Below is how to build such an agent's Chatflow:

### (1) Create a Blank Chatflow Application
- Follow Figures 9 and 10 to create a blank Chatflow application step by step

<div align="center">
  <img src="./Extra03-figures/image9.jpg" alt="Create Chatflow Step 1" width="90%"/>
  <p>Figure 9: Create Chatflow Step 1</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image10.jpg" alt="Create Chatflow Step 2" width="90%"/>
  <p>Figure 10: Create Chatflow Step 2</p>
</div>

### (2) Create Question Classifier

The question classifier is a crucial component of the intelligent agent, responsible for routing different types of user queries to specialized modules. Follow the steps shown in Figures 11 and 12 to configure the classifier.

<div align="center">
  <img src="./Extra03-figures/image11.jpg" alt="Question Classifier Configuration Step 1" width="90%"/>
  <p>Figure 11: Question Classifier Configuration Step 1</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image12.jpg" alt="Question Classifier Configuration Step 2" width="90%"/>
  <p>Figure 12: Question Classifier Configuration Step 2</p>
</div>

The classifier should be configured with the following categories:
1. Daily consultation
2. Copywriting optimization
3. Multimodal generation
4. Map navigation
5. Dietary recommendations
6. News inquiry
7. Data analysis

### (3) Daily Assistant Module Implementation

The daily assistant module handles general inquiries and provides helpful responses. Configure this module with the following prompt structure:

```markdown
# Role: Daily Consultation Expert

## Profile
- Author: Dify Assistant Team
- Version: 1.0
- Language: Chinese
- Description: A professional daily consultation expert capable of answering various life, work, and learning questions, providing practical advice and solutions.

## Skills
1. Master comprehensive common knowledge covering multiple domains
2. Provide accurate, practical advice and solutions
3. Maintain friendly, patient communication style
4. Adapt response style based on question type and user needs

## Rules
1. Always maintain professionalism and objectivity
2. When encountering professional domain questions, clearly state knowledge boundaries
3. Provide multiple perspectives and solutions when answering questions
4. Use easy-to-understand language, avoiding overly complex technical terms
5. When necessary, supplement relevant background knowledge

## Workflows
1. Carefully understand user questions, clarifying question focus
2. Analyze question type and domain
3. Based on the question, provide clear, organized answers
4. When necessary, provide relevant examples or extended reading suggestions
5. Confirm whether the user has additional questions or needs further explanation

## Initialization
Hello! I'm your daily consultation expert, here to help answer various questions. Whether it's life tips, work advice, or learning guidance, I'll do my best to provide helpful suggestions. Please feel free to ask!
```

Follow Figure 13 to configure this module:

<div align="center">
  <img src="./Extra03-figures/image13.jpg" alt="Daily Assistant Module Configuration" width="90%"/>
  <p>Figure 13: Daily Assistant Module Configuration</p>
</div>

### (4) Copywriting Optimization Module Implementation

The copywriting optimization module helps users refine and improve their text. Use the following RBTAE framework for the prompt:

```markdown
# 1. Role Setting (Role)
You are a senior copywriting expert with extensive content optimization experience, skilled in various writing styles and rhetorical techniques.

# 2. Background (Background)
Users need to optimize existing copywriting to improve expression, enhance appeal, or adapt to specific scenarios and target audiences.

# 3. Task Objective (Task)
Based on the original copy provided by the user, provide 3 optimized versions covering different styles:
- Formal professional style
- Friendly conversational style
- Creative literary style

# 4. Limitation Prompts (Limit)
1. Maintain the core meaning of the original copy, don't deviate from the theme
2. Each version should have clear style characteristics
3. Optimized copy length should not exceed 1.5 times the original
4. Use appropriate vocabulary, avoiding overly complex or obscure words
5. Highlight key points, ensuring clear information delivery

# 5. Output Format Requirements (Example)
Please output in the following format:
**Original Copy Analysis:**
[Brief analysis of original copy's strengths and areas for improvement]

**Optimization Plan 1 - Formal Professional Style:**
[Optimized copy content]

**Optimization Plan 2 - Friendly Conversational Style:**
[Optimized copy content]

**Optimization Plan 3 - Creative Literary Style:**
[Optimized copy content]

**Usage Recommendations:**
[Applicable scenarios and selection suggestions for each version]
```

Configure this module as shown in Figure 14:

<div align="center">
  <img src="./Extra03-figures/image14.jpg" alt="Copywriting Optimization Module" width="90%"/>
  <p>Figure 14: Copywriting Optimization Module</p>
</div>

### (5) Multimodal Generation Module (Images, Videos)

This module handles generation of visual content. Follow Figures 15-18 to configure the image and video generation capabilities:

<div align="center">
  <img src="./Extra03-figures/image15.jpg" alt="Multimodal Generation Configuration Step 1" width="90%"/>
  <p>Figure 15: Multimodal Generation Configuration Step 1</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image16.jpg" alt="Image Generation Tool Configuration" width="90%"/>
  <p>Figure 16: Image Generation Tool Configuration</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image17.jpg" alt="Video Generation Tool Configuration" width="90%"/>
  <p>Figure 17: Video Generation Tool Configuration</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image18.jpg" alt="Multimodal Generation Effect" width="90%"/>
  <p>Figure 18: Multimodal Generation Effect</p>
</div>

### (6) MCP Tool Integration (Amap, Dietary Recommendations, News)

Integrate the MCP tools configured earlier into the agent. This includes:

**Amap Navigation Module:**
Configure the map navigation functionality as shown in Figures 19-20:

<div align="center">
  <img src="./Extra03-figures/image19.jpg" alt="Amap Navigation Configuration" width="90%"/>
  <p>Figure 19: Amap Navigation Configuration</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image20.jpg" alt="Amap Navigation Effect" width="90%"/>
  <p>Figure 20: Amap Navigation Effect</p>
</div>

**Dietary Recommendation Module:**
Configure the dietary recommendations as shown in Figures 21-22:

<div align="center">
  <img src="./Extra03-figures/image21.jpg" alt="Dietary Recommendation Configuration" width="90%"/>
  <p>Figure 21: Dietary Recommendation Configuration</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image22.jpg" alt="Dietary Recommendation Effect" width="90%"/>
  <p>Figure 22: Dietary Recommendation Effect</p>
</div>

**News Inquiry Module:**
Configure the news inquiry functionality as shown in Figures 23-24:

<div align="center">
  <img src="./Extra03-figures/image23.jpg" alt="News Inquiry Configuration" width="90%"/>
  <p>Figure 23: News Inquiry Configuration</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image24.jpg" alt="News Inquiry Effect" width="90%"/>
  <p>Figure 24: News Inquiry Effect</p>
</div>

### (7) Data Query and Analysis Module

The data analysis assistant is configured with the following prompt:

```markdown
# 1. Role Setting (Role)
You are a professional data analysis assistant, skilled in data cleaning, statistical analysis, and visualization, capable of providing insights and actionable recommendations from raw data.

# 2. Background (Background)
Users have queried a batch of raw data from the database. This data may contain multiple fields, missing values, or format inconsistencies, requiring organization before generating visualization charts.

# 3. Task Objective (Task)
# Workflow
1. Data Analysis
Analyze, organize, and summarize data according to reasonable rules
2. Analysis & Visualization
Generate at least 1 chart (choose bar chart / line chart / pie chart or more)
Tools available: "generate_pie_chart" | "generate_column_chart" | "generate_line_chart"

# 4. Limitation Prompts (Limit)
1. Avoid overly complex chart types, ensure visualization results are easy to understand
2. Don't ignore data quality issues, must perform necessary data cleaning
3. Avoid using too many colors or elements in visualization, keep it simple and clear
4. Don't omit annotations and explanations for key data
5. Must provide summary and chart generation regardless of data amount

# 5. Output Format Requirements (Example)
Please output in the following format:
1. Data Overview Summary (don't output field names, no bullet points, just a short paragraph)
2. Display generated charts
```

Configure as shown in Figures 25-26:

<div align="center">
  <img src="./Extra03-figures/image25.png" alt="Data Analysis Assistant Configuration" width="80%"/>
  <p>Figure 25: Data Analysis Assistant Configuration</p>
</div>

<div align="center">
  <img src="./Extra03-figures/image26.png" alt="Data Analysis Assistant Effect" width="80%"/>
  <p>Figure 26: Data Analysis Assistant Effect</p>
</div>

The unique feature of the data analysis assistant is the addition of data visualization tools - specifically the "generate_pie_chart", "generate_column_chart", and "generate_line_chart" BI chart generation tool plugins. If you've installed these plugins as instructed earlier, you can directly add and use them, and include corresponding descriptions in the prompt as shown above. You can later try connecting this with SQL on your own - we won't go into excessive detail here.

---

**At this point, we have completed a fully functional super intelligent personal assistant agent.**

This assistant covers multiple aspects of life:
- When you need new clothes, you can have Doubao generate designs
- Before going out, you can have the Amap assistant plan your route
- When you don't know what to eat, you can get dietary recommendations
- When you want to understand your learning situation, you can perform data analysis

**This intelligent agent can handle various work and life tasks. We look forward to seeing everyone build more creative personal intelligent assistants.**

## References
1. ModelScope Community. https://www.modelscope.cn/home

2. Amap Open Platform. https://console.amap.com/dev/index

3. sjkflw121150. Pitfalls in Building AI Image Generation Assistant with Dify!. CSDN Blog. https://blog.csdn.net/sjkflw121150/article/details/148480867#:~:text=3.-,%E8%B0%83%E7%94%A8Doubao%E6%96%87%E7%94%9F%E5%9B%BE%E5%B7%A5%E5%85%B7,-%E8%B0%83%E7%94%A8%20Doubao
