# 🧐 The Skeptical Archivist Agent

## 🚀 Overview

The **Skeptical Archivist** is an AI Agent designed to demonstrate **Hallucination Mitigation** and **Fact Verification** workflows. 

Unlike standard RAG (Retrieval Augmented Generation) systems that blindly trust their data sources, this agent implements a "Trust but Verify" architecture. It cross-references internal documents with external trusted sources (Wikipedia) before committing any information to its Long-Term Memory.

## 🧠 Core Architecture & Memory

The agent operates on a strict three-step cognitive cycle:

1.  **Retrieval (Internal):** Searches internal knowledge bases (Vector Store) to find information about a user's query.
2.  **Verification (External):** If information is found, it extracts key entities and cross-references them against a trusted external API (Wikipedia) to determine if the entity is historical fact or fiction.
3.  **Archival (Long-Term Memory):**
    * **The Filter:** The agent has a "write-access" tool (`memory_tool`) that connects to a secondary FAISS Vector Database.
    * ✅ **Verified Facts:** If the entity is real, the fact is permanently saved to this memory. Future queries can retrieve this "verified truth."
    * ❌ **Fictional/Unverified:** If the entity is fictional, the agent refuses to save it, preventing the "pollution" of the database with false information.

## 🛠️ Tech Stack

* **Orchestration:** LangChain (ReAct Agent Pattern)
* **LLM:** Google Gemini 2.0 Flash
* **Vector Database:** FAISS (Facebook AI Similarity Search) - *Used for both the Book Source and the Dynamic Memory.*
* **Tools:**
    * `book_search_tool` (Read-only access to source text)
    * `wiki_tool` (External Verification via Wikipedia API)
    * `memory_tool` (Write-only access to verify & save facts)

## 📂 Project Structure

```bash
├── Skeptical_Archivist_Agent_Ver3.ipynb  # Core agent logic (Jupyter Notebook)
├── requirements.txt                      # Python dependencies
└── README.md                             # Project documentation
```
## ⚡ How to Run

### Option 1: Run in Google Colab (Recommended)
Click the "Open in Colab" badge at the top of this README to run the notebook directly in your browser.

### Option 2: Run Locally
1. **Clone the repository:**
   ```bash
   git clone [https://github.com/ergaikwadketan/skeptical-archivist-agent.git](https://github.com/ergaikwadketan/skeptical-archivist-agent.git)
   cd skeptical-archivist-agent
    ```
2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
    ```
3. **Set up your API Key:** Create a .env file or set the environment variable in your terminal:
   ```bash
   export GOOGLE_API_KEY="your_key_here"
   ```
5. **Run the Notebook:** Launch Jupyter Lab or Notebook to run
   ```bash
   Skeptical_Archivist_Agent_Ver3.ipynb.
   ```
### 🧪 Example Scenarios
**Scenario 1: The Verifiable Fact**
**User:** "Who is Nicolas Flamel?"

* **Agent Action:** Searches internal book → Finds he created the Philosopher's Stone.

* **Agent Verification:** Checks Wikipedia → Confirms Nicolas Flamel was a real French scribe (1330–1418).

* **Result:** ✅ Fact saved to memory.

**Scenario 2: The Fictional Element**
**User:** "What does the spell Lumos do?"

* **Agent Action:** Searches internal book → Finds it lights up a wand tip.

* **Agent Verification:** Checks Wikipedia for "Lumos (Spell)" → Fails to find historical record.

* **Result:** ❌ Fact rejected; not saved to memory.

---

*Created by Ketan Dilip Gaikwad*
