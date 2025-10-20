# SkillVault - Personal Skills Database

## Overview
SkillVault is a personal knowledge base to store and retrieve skills and solutions learned across various domains (e.g., IT, DIY). It allows logging problems and their solutions (e.g., "black screen GPU" → "connect to PCIe slot, tweak BIOS") and supports non-verbatim search to find entries even with vague or rephrased queries.

## Purpose
- Store problem-solution pairs with metadata (date, domain, tags).
- Enable fuzzy and semantic search for long-term usability.
- Keep the system lightweight, local, and scalable.

## Tech Stack
- **Storage**: SQLite with Full-Text Search (FTS5) for initial setup.
- **Search**: Basic keyword search (FTS), optional fuzzy search (`thefuzz`), and semantic search (`sentence-transformers` + Chroma).
- **Interface**: Streamlit for a simple web UI (optional) or Notion for no-code.
- **Language**: Python for scripting, SQL for queries.

## Setup
1. Install Python 3.8+.
2. Install dependencies: `pip install sqlite3 thefuzz sentence-transformers chromadb streamlit`.
3. Create SQLite database: `competences.db` with a virtual FTS5 table.
4. (Optional) Set up Chroma for semantic search.

## To-Do List
### Phase 1: Basic Setup (Week 1)
- [ ] Create SQLite database with table `competences` (fields: `id`, `date`, `domaine`, `probleme`, `solution`, `tags`).
- [ ] Write Python script to add entries (e.g., problem: "écran noir carte graphique", solution: "brancher dans PCIe, modifier BIOS").
- [ ] Implement basic FTS search in SQLite (e.g., `SELECT * FROM competences WHERE competences MATCH 'ecran OR gpu'`).
- [ ] Add 10-20 test entries to validate structure and search.

### Phase 2: Interface and Fuzzy Search (Week 2)
- [ ] Build a Streamlit UI for adding and searching entries (input fields for problem, solution, tags; search bar).
- [ ] Add fuzzy search with `thefuzz` to handle typos (e.g., match "ecran sombre" to "écran noir").
- [ ] Test search with varied queries (e.g., "problème affichage GPU").

### Phase 3: Semantic Search (Month 2)
- [ ] Integrate `sentence-transformers` (`all-MiniLM-L6-v2`) to generate embeddings for entries.
- [ ] Set up Chroma to store embeddings and enable semantic search.
- [ ] Test semantic search (e.g., query "problème affichage sombre" finds "écran noir carte graphique").
- [ ] Add tag auto-generation using LLM for better searchability.

### Phase 4: Long-Term Maintenance (Month 3+)
- [ ] Implement backup system (e.g., copy `competences.db` to cloud or GitHub).
- [ ] Add "last updated" field to track and revise outdated solutions.
- [ ] Evaluate scaling needs (e.g., migrate to PostgreSQL + pgvector if >1000 entries).
- [ ] (Optional) Explore no-code alternative (Notion/Airtable) for easier management.

## Usage
1. Run the Python script to initialize the database.
2. Add entries via script or UI (e.g., `python add_entry.py` or Streamlit app).
3. Search using keywords (FTS), fuzzy matching, or semantic queries.
4. Regularly back up the database.

## Notes
- Start with SQLite for simplicity; scale to vector DB (Chroma) for semantic search.
- Ensure consistent tags (e.g., "GPU" instead of "carte graphique") for better matching.
- Test `all-MiniLM-L6-v2` for French; consider `paraphrase-multilingual-mpnet-base-v2` if precision is low.
