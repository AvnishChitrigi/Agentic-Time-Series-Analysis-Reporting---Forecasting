# Project Scribe: Interactive AI for Time Series Forecasting

It is an autonomous, interactive AI agent designed to perform end-to-end time series analysis and forecasting. It leverages a Large Language Model (LLM) as its core reasoning engine to replicate the entire workflow of a professional data scientist. The agent can inspect unfamiliar datasets, interact with the user to clarify goals, and then autonomously execute a robust statistical analysis pipeline, culminating in tailored reports for both technical and business audiences.

This project represents a paradigm shift from static automation scripts to dynamic, intelligent agents that can reason, act, and collaborate to solve complex analytical problems.

## Core Features

*   **Autonomous Operation:** Driven by the ReAct (Reason + Act) framework, the agent independently plans and executes a complex sequence of analytical tasks, from data discovery to final reporting.

*   **Interactive & Collaborative (Human-in-the-Loop):** The agent is designed as a collaborative partner. It automatically scans for available datasets, identifies filterable columns, and then pauses its workflow to ask the user for guidance, making it practical for real-world, ambiguous data.

*   **Dynamic Data Discovery:** The agent is not hard-coded for one dataset. It begins by exploring for unfamiliar CSV files, inspecting their structure, and dynamically adapting its entire analytical plan based on the user's choices.

*   **Robust Statistical Engine:** The agent's "toolbox" grounds its reasoning in fact. It includes an automated grid search to programmatically find the optimal SARIMA model and an intelligent decomposition function that automatically determines the appropriate seasonal model.

*   **Dual-Audience Reporting:** The agent synthesizes its findings into tailored technical and non-technical reports, effectively bridging the critical communication gap between data scientists and executive decision-makers.

## GenAI Architecture

This project's intelligence is built on several key Generative AI methodologies, orchestrated by the LangChain framework.

#### 1. The ReAct Framework (Reason + Act)
The agent operates on a continuous **Thought -> Action -> Observation** loop. This is the core of its autonomy. The LLM (Gemini 2.0 Flash) forms a plan (Thought), chooses a Python tool to execute (Action), and then receives a factual result from that tool (Observation) to inform its next thought.

#### 2. Tool-Augmented Generation (Grounding)
The LLM is "grounded" in reality by a robust toolbox (`tools.py`). It cannot "hallucinate" a statistical result because it is forced to call a Python function that performs the real mathematical calculation. The `description` of each tool acts as the "API documentation" that the LLM reads to learn how to use its capabilities.

#### 3. Advanced Prompt Engineering
The agent's "programming" is contained within the master prompt in `agent.py`. We use several techniques, including **Role-Prompting** (assigning an expert persona), **Chain of Thought** (providing a high-level methodology), and **Few-Shot Prompting** (providing a concrete example of a correctly formatted output) to ensure reliable and intelligent behavior.

## Technology Stack

| Component                  | Technologies                                                              |
| -------------------------- | ------------------------------------------------------------------------- |
| **Generative AI & Agents** | `langchain`, `langchain-google-genai` (for Google's Gemini 2.0 Flash) |
| **Data Analysis & Stats**  | `pandas`, `numpy`, `statsmodels`, `scikit-learn`                            |
| **Plotting & Visualization** | `matplotlib`, `seaborn`                                                   |
| **Environment Management** | `python-dotenv`                                                           |

## Project Structure

```
project_scribe/
├── .env                  # Stores the GOOGLE_API_KEY
├── config.json           # Main configuration for paths
├── main.py               # The main entry point to LAUNCH the agent
├── README.md             # This file
├── requirements.txt      # Python package dependencies
|
├── data/
│   └── input/            # Place your CSV files here
|
├── outputs/
│   ├── temp/             # Temporary storage for the prepared time series
│   ├── logs/             # The final JSON analysis log
│   ├── plots/            # All generated plots (.png)
│   └── reports/          # Final text reports (.txt)
|
└── src/
    └── scribe/
        ├── agent.py      # The agent's "brain" and assembly
        └── tools.py      # The agent's "toolbox" of Python functions
```

## Setup and Installation

Follow these steps to get the project running.

**1. Clone the Repository**
```bash
git clone <your-repository-url>
cd project_scribe
```

**2. Create and Activate a Virtual Environment**
```bash
# For Windows
python -m venv venv
venv\Scripts\activate

# For macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

**3. Install Dependencies**
```bash
pip install -r requirements.txt
```

**4. Set Up Your API Key**
Create a new file named `.env` in the root directory of the project. Add your Google AI Studio API key to this file.
```
# .env
GOOGLE_API_KEY="your_api_key_here"
```

**5. Add Your Data**
Place one or more CSV files into the `data/input/` directory.

## How to Run

After completing the setup, start the AI Analyst with a single command from the root directory:

```bash
python main.py
```
The agent will begin its workflow. Be ready to provide input in the console when it asks you a question.

## Future Work

*   **Expand the Analytical Toolbox:**
    *   Integrate additional forecasting models like **Prophet** and **Exponential Smoothing**.
    *   Enable **SARIMAX** analysis by allowing the agent to identify and incorporate external regressors.
    *   Add tools for **anomaly detection** to proactively flag unusual data points.

*   **Enhance Agent Intelligence:**
    *   **Rebuild with LangGraph:** Transition from a simple ReAct loop to a more robust state machine, enabling explicit error handling paths and more complex, cyclical reasoning.
    *   **Implement Long-Term Memory:** Use a vector database to allow the agent to "remember" past analyses and apply learnings to new, similar datasets.

*   **Improve User Experience:**
    *   **Build a GUI:** Create a web-based front-end with **Streamlit** or **Gradio** to provide an interactive, user-friendly interface.
    *   **Prototype with Langflow:** Use Langflow's visual, drag-and-drop canvas to rapidly prototype and visualize new agent architectures and workflows.
