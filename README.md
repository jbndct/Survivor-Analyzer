# 🔪 Survival Analytics Engine: Director's Cut

A cinematic, AI-powered analytics dashboard that transforms raw text logs from survival and reality simulators into dramatic, cohesive television episodes. 

**Designed specifically for use with:** [Slasher Movie Sim: Final Girl](https://slashermoviesim.com/finalgirl.html) (and highly adaptable to traditional reality TV simulators).

Unlike standard text parsers, the *Director's Cut* engine doesn't just read data—it acts as an Executive Producer. It tracks shifting alliances, generates in-character confessionals, calculates episode volatility, and builds a dynamic season-long Edit Logic (Edgic) matrix so you can track who is getting the "Winner's Edit" and who is merely cannon fodder.

---

## ✨ Core Features

* **📺 The "TV Edit" Recap:** Converts dry simulation logs into dramatic, multi-paragraph narrative summaries focusing on camp paranoia, betrayals, and tribal tension.
* **🗣️ Faux Confessionals:** Automatically invents highly realistic, in-character quotes based on the specific events of the episode.
* **📊 Dynamic Edgic Matrix:** A season-long, color-coded visual grid that tracks the narrative visibility (CP, OTT, UTR, MOR, INV) of every surviving character across the season.
* **🔥 The Chaos Meter:** An algorithmic 1-10 rating scale that visualizes how chaotic a round was (from boring unanimous votes to idol-playing, rock-drawing bloodbaths).
* **🏆 Narrative Superlatives:** Awards specific flavor titles each episode (e.g., *The Mastermind*, *The Camp Mess*, *The Silent Assassin*) with AI-generated justifications.
* **⏪ Safe Rewind System:** A "Delete Latest Episode" function that safely rolls back the database and restores the AI's contextual memory to its exact prior state.

---

## 🛠️ Tech Stack (100% Free Tier)

* **Frontend:** HTML5, CSS3, Vanilla JavaScript, Bootstrap 5 (Dark Theme)
* **Database:** Supabase (PostgreSQL / REST API)
* **AI Engine:** Google Gemini 2.5 Flash (via Google AI Studio)
* **Hosting:** Completely Serverless (Can be run locally via `file://` or hosted on GitHub Pages)

---

## 🚀 Setup & Installation

### 1. Supabase (Database) Setup
1. Create a free account at [Supabase](https://supabase.com/).
2. Create a new project and open the **SQL Editor**.
3. Run the following schema to build the required tables:

\`\`\`sql
CREATE TABLE franchises (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

CREATE TABLE seasons (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  franchise_id UUID REFERENCES franchises(id) ON DELETE CASCADE,
  season_number INT NOT NULL,
  season_context TEXT DEFAULT 'A new nightmare begins. The cast has arrived.',
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

CREATE TABLE episodes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  season_id UUID REFERENCES seasons(id) ON DELETE CASCADE,
  episode_number INT NOT NULL,
  previous_season_context TEXT,
  episode_title TEXT,
  episode_recap TEXT,
  confessional JSONB,
  superlatives JSONB,
  strategic_rating INT,
  entertainment_rating INT,
  production_rating INT,
  chaos_index INT,
  edgic_ratings JSONB,
  eliminated_player TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Disable Row Level Security for local public API access
ALTER TABLE franchises DISABLE ROW LEVEL SECURITY;
ALTER TABLE seasons DISABLE ROW LEVEL SECURITY;
ALTER TABLE episodes DISABLE ROW LEVEL SECURITY;
\`\`\`
4. Go to **Project Settings > API** and copy your `Project URL` and `anon` public key.

### 2. Google AI Studio Setup
1. Go to [Google AI Studio](https://aistudio.google.com/).
2. Click **Get API Key** and generate a new key for the Gemini 2.5 Flash model.

### 3. Running the Engine
1. Clone or download this repository.
2. Open `index.html` in any modern web browser.
3. In the top **API CONFIG** bar, paste your Supabase URL, Supabase Anon Key, and Gemini API Key.
4. Click **Save Keys** (these will safely persist in your browser's local storage).

---

## 🎬 How to Use

1. **Initialize a Franchise:** Click "New Franchise" to create a container (e.g., "Camp Blood Season 1").
2. **Start a Season:** Click the **+** button next to the Season dropdown to initialize Season 1.
3. **Run the Simulator:** Go to [Slasher Movie Sim: Final Girl](https://slashermoviesim.com/finalgirl.html) and simulate a round/episode.
4. **Ingest Data:** Copy the raw text output from the simulator and paste it into the "Ingest Simulation Data" text box.
5. **Generate:** Click **Generate TV Edit**. The AI will parse the logic, write the story, assign Edgic ratings, update its internal memory, and render the episode card to your dashboard.