# 🤖 AI Software Engineering Assistant

An AI-powered **Software Engineering Assistant** built using the **OpenAI Agents SDK**, **LiteLLM**, and **Google Gemini**.

This project demonstrates how multiple specialized AI agents can collaborate to support developers throughout the software development lifecycle — from understanding requirements to writing code, reviewing it, testing it, debugging issues, analyzing GitHub issues, and generating documentation.

---

## 🚀 Project Overview

Software development involves many repetitive and time-consuming tasks such as:

* Understanding software requirements
* Writing implementation code
* Reviewing code quality
* Finding bugs and security vulnerabilities
* Creating test cases
* Running tests
* Analyzing GitHub issues
* Maintaining project documentation
* Inspecting project files

This project creates an **AI Software Engineering Assistant** that uses multiple specialized agents to automate and assist with these tasks.

The agents are powered by **Gemini 2.5 Flash** through **LiteLLM** and coordinated using the **OpenAI Agents SDK**.

---

## 🏗️ Architecture

The project follows a multi-agent architecture where different agents specialize in different software engineering tasks.

```text
                         ┌─────────────────────┐
                         │        User         │
                         └──────────┬──────────┘
                                    │
                                    ▼
                    ┌────────────────────────────┐
                    │ AI Software Engineering    │
                    │        Assistant           │
                    └─────────────┬──────────────┘
                                  │
              ┌───────────────────┼───────────────────┐
              │                   │                   │
              ▼                   ▼                   ▼
       Requirements         Coding Assistant      GitHub Agent
          Agent                   │                   │
              │                   ▼                   ▼
              │             Code Reviewer      Issue Analysis
              │                   │
              │                   ▼
              │             Testing Agent
              │                   │
              │                   ▼
              │          Bug Investigation
              │                   │
              │                   ▼
              │             Documentation
              │
              └──────────────────────────────────────┐
                                                     │
                                                     ▼
                                          Final Development
                                             Assistance
```

---

## 🧠 Agents Implemented

### 1. Requirements Analysis Agent

Analyzes software problems and identifies:

* Main problem
* Expected behavior
* Affected components
* Technical requirements
* Acceptance criteria

The output is structured using **Pydantic models**.

---

### 2. Coding Assistant

Converts analyzed requirements into an implementation.

It generates:

* Solution explanation
* Source code
* Files that need modification

The agent is instructed to produce clean and secure Python code.

---

### 3. Code Reviewer

Reviews generated code for:

* Correctness
* Bugs
* Security issues
* Readability
* Maintainability
* Edge cases

It also determines whether the solution should be approved.

---

### 4. Testing Agent

Analyzes the generated solution and creates test scenarios covering:

* Normal cases
* Invalid inputs
* Edge cases
* Authentication failures
* Validation failures

The project also demonstrates a testing agent with a real `pytest` execution tool.

---

### 5. Bug Investigation Agent

Analyzes:

* Source code
* Code review results
* Testing results

It identifies:

* Bugs
* Root causes
* Severity
* Recommended fixes

The project demonstrates iterative improvement by feeding these findings back to the coding agent.

---

### 6. Documentation Agent

Generates technical documentation containing:

* Project summary
* Changes made
* Setup instructions
* Usage instructions

---

### 7. Code File Analyst

The project demonstrates tool-using agents that can:

* Read files
* Search source code
* Analyze project files

Example tools include:

```python
read_file()
search_code()
```

---

### 8. GitHub Requirements Analysis Agent

The project integrates with the GitHub API to retrieve public GitHub issues.

It can analyze:

* Issue title
* Issue description
* Software problem
* Expected behavior
* Affected components
* Technical requirements

The notebook demonstrates analysis of a GitHub issue from the Flask repository.

---

### 9. Handoff Agent

The project demonstrates **agent handoffs**, where one specialized agent transfers a task to another specialized agent.

Example:

```text
User
  │
  ▼
Requirements Agent
  │
  │ Handoff
  ▼
Coding Agent
  │
  ▼
Implementation
```

This allows different agents to specialize in different parts of the development workflow.

---

### 10. Conversation Memory

The project also demonstrates conversational memory using:

```python
OpenAIConversationsSession
```

This allows an agent workflow to maintain conversational context across interactions.

---

## 🛠️ Technologies Used

| Technology        | Purpose                                 |
| ----------------- | --------------------------------------- |
| Python            | Core programming language               |
| OpenAI Agents SDK | Multi-agent orchestration               |
| LiteLLM           | Model/provider integration              |
| Google Gemini     | Large Language Model                    |
| Gemini 2.5 Flash  | Primary AI model                        |
| Pydantic          | Structured agent outputs and validation |
| FastAPI           | Example API/application                 |
| bcrypt            | Password hashing                        |
| Pytest            | Automated testing                       |
| GitHub API        | GitHub issue retrieval                  |
| Google Colab      | Development environment                 |

---

## 🔄 Development Workflow

The main workflow demonstrated in the project is:

```text
Software Problem
       │
       ▼
Requirements Analysis
       │
       ▼
Code Generation
       │
       ▼
Code Review
       │
       ▼
Testing
       │
       ▼
Bug Investigation
       │
       ▼
Fix Generation
       │
       ▼
Second Code Review
       │
       ▼
Documentation
```

This creates an iterative AI-assisted software engineering workflow.

---

## 🔐 Example: FastAPI Login Problem

The project uses a FastAPI login endpoint as an example problem.

### Initial Problem

```text
My FastAPI login endpoint crashes when
the password field is empty.
```

The Requirements Agent analyzes the problem and produces structured requirements.

The Coding Agent then generates a solution.

The Code Reviewer identifies issues such as:

* Hardcoded credentials
* Weak password validation
* Maintainability concerns

The Bug Investigation Agent then analyzes these problems and recommends fixes.

---

## 🔧 Security Improvements

The improved solution demonstrates several security improvements:

### Password Hashing

Instead of storing plaintext passwords, the improved version uses:

```python
bcrypt.hashpw()
```

and verifies passwords using:

```python
bcrypt.checkpw()
```

### Improved Password Validation

The solution also handles:

* Empty passwords
* Whitespace-only passwords
* Missing password fields

### Centralized Error Messages

Validation messages are stored in a centralized dictionary:

```python
ERROR_MESSAGES = {
    "password_empty": "...",
    "password_required": "...",
    "validation_error_default": "..."
}
```

---

## 🧪 Testing

The project demonstrates automated testing using `pytest`.

Example test cases include:

* Valid login
* Invalid password
* Invalid username
* Empty password

The notebook reports:

```text
4 tests passed
0 tests failed
```

The testing agent is also instructed not to claim tests passed unless actual test execution confirms the result.

---

## 🔗 GitHub Issue Integration

The project uses the GitHub API to retrieve public issues.

Example tool:

```python
get_github_issue(
    owner,
    repo,
    issue_number
)
```

The agent then analyzes the retrieved issue instead of inventing issue information.

Example workflow:

```text
GitHub Repository
       │
       ▼
GitHub API
       │
       ▼
Issue Retrieval
       │
       ▼
Requirements Analysis Agent
       │
       ▼
Technical Requirements
```

---

## 🧰 Agent Tools

The project demonstrates function tools including:

```python
read_file()
write_file()
search_code()
run_tests()
get_github_issue()
```

These tools allow agents to interact with the development environment instead of only generating text.

---

## 📁 Project Structure

A recommended GitHub repository structure is:

```text
AI-Software-Engineering-Assistant/
│
├── README.md
├── sdk_final_capstone_project.ipynb
│
├── sample_app.py
├── test_sample_app.py
│
├── requirements.txt
│
└── .gitignore
```

> The uploaded notebook contains the complete experimental implementation and demonstrations.

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/AI-Software-Engineering-Assistant.git
cd AI-Software-Engineering-Assistant
```

### 2. Install dependencies

```bash
pip install openai-agents
pip install litellm
pip install google-generativeai
pip install fastapi
pip install uvicorn
pip install pydantic
pip install bcrypt
pip install pytest
pip install requests
```

Or install from a requirements file:

```bash
pip install -r requirements.txt
```

---

## 🔑 API Key Configuration

The notebook uses a Gemini API key through Google Colab secrets.

Example:

```python
from google.colab import userdata
import os

os.environ["GEMINI_API_KEY"] = userdata.get("GEMINI_API_KEY")
```

Create a Gemini API key and store it securely.

**Never commit API keys to GitHub.**

Do not put keys directly inside your source code:

```python
# ❌ Don't do this
GEMINI_API_KEY = "your-secret-key"
```

Use environment variables or secret managers instead.

---

## ▶️ Running the Project

The primary project is implemented as a Google Colab notebook.

Open:

```text
sdk_final_capstone_project.ipynb
```

Then:

1. Open the notebook in Google Colab.
2. Add your `GEMINI_API_KEY` to Colab Secrets.
3. Run the installation cell.
4. Run the initialization cells.
5. Execute the agent demonstrations.
6. Experiment with different software engineering problems.

---

## 📌 Example Usage

A user can provide a problem such as:

```text
My FastAPI login endpoint crashes when
the password field is empty.
```

The system can then:

```text
Analyze Requirements
        ↓
Generate Code
        ↓
Review Code
        ↓
Generate Tests
        ↓
Investigate Bugs
        ↓
Generate Improved Code
        ↓
Review Again
        ↓
Generate Documentation
```

---

## 📊 Key Features

* 🤖 Multi-agent software engineering workflow
* 🧠 Gemini-powered reasoning
* 🔀 Agent handoffs
* 🛠️ Function/tool calling
* 📋 Structured outputs with Pydantic
* 🔍 Requirements analysis
* 💻 Code generation
* 👀 Code review
* 🧪 Automated testing
* 🐛 Bug investigation
* 🔐 Security analysis
* 📄 Documentation generation
* 📂 File analysis
* 🐙 GitHub issue analysis
* 💬 Conversation memory
* 🔄 Iterative code improvement

---

## ⚠️ Limitations

This project is a capstone/prototype implementation rather than a production-ready autonomous coding platform.

Some components are demonstrated using simulated or example environments.

For production use, additional features would be required, including:

* Secure authentication
* Real database integration
* Secure JWT generation
* Rate limiting
* Sandboxed code execution
* Permission management
* Better error recovery
* Production-grade logging
* Comprehensive automated testing
* Secret management

---

## 🚀 Future Improvements

Possible future enhancements include:

* GitHub pull-request analysis
* Automatic pull-request generation
* Repository-wide code understanding
* Vector database integration
* RAG-based documentation search
* CI/CD integration
* Automatic issue-to-code workflow
* Docker-based sandbox execution
* Multi-model fallback
* Web interface for the agent system
* Persistent project memory
* Automated code patch generation

---

## 🎯 Learning Outcomes

Through this project, the following concepts are demonstrated:

* Multi-agent AI systems
* Agent orchestration
* Agent handoffs
* Tool calling
* Structured AI outputs
* LLM integration using LiteLLM
* Software requirement analysis
* AI-assisted coding
* Automated code review
* AI-assisted testing
* Bug analysis
* GitHub API integration
* Conversational memory
* Iterative software development

---

## 👨‍💻 Author

**Swayam Sachdeva**

B.Tech Computer Science & Engineering

Interested in:

* Artificial Intelligence
* Machine Learning
* Generative AI
* Software Development
* AI Agents
* Data Analytics

---

## ⭐ Acknowledgements

This project was developed as a capstone project exploring **AI agents and AI-assisted software engineering workflows**.

If you find this project useful, consider giving the repository a ⭐ on GitHub.
