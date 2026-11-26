## Design and Implementation of a Multidocument Retrieval Agent Using LlamaIndex

### AIM:
To design and implement a multidocument retrieval agent using LlamaIndex to extract and synthesize information from multiple research articles, and to evaluate its performance by testing it with diverse queries, analyzing its ability to deliver concise, relevant, and accurate responses.

### PROBLEM STATEMENT:
  To develop an AI-powered research paper analysis system using LlamaIndex and OpenAI that retrieves and summarizes information from multiple research papers and compares their approaches, contributions, and evaluation results.

### DESIGN STEPS:

#### STEP 1: Load the research papers and extract their contents using document tools.

#### STEP 2: Create vector and summary tools for each paper and integrate them with the OpenAI LLM using LlamaIndex Agent.

#### STEP 3: Query the AI agent to summarize, analyze, and compare RAGChecker, SWE-bench, and Knowledge Card Filling.

### PROGRAM:

```
from helper import get_openai_api_key
OPENAI_API_KEY = get_openai_api_key()

import nest_asyncio
nest_asyncio.apply()

urls = [
    "https://openreview.net/pdf?id=J9oefdGUuM",
    "hhttps://openreview.net/pdf?id=VTF8yNQM66",
    "https://openreview.net/pdf?id=WbWtOYIzIK",
]

papers = [
    "RAGChecker_A_Fine_grained.pdf",
    "SWE_bench_Can_Language_Mo.pdf",
    "Knowledge_Card_Filling_LL.pdf",
]

from utils import get_doc_tools
from pathlib import Path

paper_to_tools_dict = {}
for paper in papers:
    print(f"Getting tools for paper: {paper}")
    vector_tool, summary_tool = get_doc_tools(paper, Path(paper).stem)
    paper_to_tools_dict[paper] = [vector_tool, summary_tool]

initial_tools = [t for paper in papers for t in paper_to_tools_dict[paper]]

from llama_index.llms.openai import OpenAI

llm = OpenAI(model="gpt-3.5-turbo")

len(initial_tools)

from llama_index.core.agent import FunctionCallingAgentWorker
from llama_index.core.agent import AgentRunner

agent_worker = FunctionCallingAgentWorker.from_tools(
    initial_tools,
    llm=llm,
    verbose=True
)
agent = AgentRunner(agent_worker)

print("Name: S.Priyadharshini")
print("Reg no: 212225230218")

response = agent.query(
    "Tell me about the evaluation datasets used in these papers and how they were used."
    "Then summarize the evaluation metrics, results, and comparisons with baseline methods."
)

print("Name: S.Priyadharshini")
print("Reg no: 212225230218")

response = agent.query(
    "Give me a summary of RAGChecker, SWE-bench, and Knowledge Card Filling, "
    "including their main approach, evaluation, and key results."
)
print(str(response))

print("Name: S.Priyadharshini")
print("Reg no: 212225230218")

response = agent.query(
    "Compare the main approaches and contributions of RAGChecker, SWE-bench, and Knowledge Card Filling. "
    "Explain their key differences and evaluation results."
)
print(str(response))
```

### OUTPUT:
<img width="1457" height="1079" alt="Jupyter RAG Evaluation Notebook Output" src="https://github.com/user-attachments/assets/a9a9b85d-4293-4b73-9797-be621df73e12" />
<img width="1500" height="1049" alt="Jupyter Notebook RAG Evaluation Summary" src="https://github.com/user-attachments/assets/d2fc04e1-3d04-491e-8894-5db872dc16cf" />
<img width="1676" height="939" alt="Jupyter Notebook RAG Evaluation Output" src="https://github.com/user-attachments/assets/75653da8-deff-4510-85a5-bcd1fcbf23fd" />


### RESULT:
  Successfully developed an AI-powered research paper analysis system that summarizes three research papers, identifies their main approaches and contributions, and compares their evaluation methods and results.
