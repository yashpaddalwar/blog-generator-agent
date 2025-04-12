# 🧠 Blog Generator using LangGraph, Groq & Tavily

This project is an **automated blog generation pipeline** that leverages **LangGraph**, **Groq's Qwen model**, and **Tavily's real-time search API** to create high-quality, well-researched blogs from just a single topic input.

---

## 🚀 What It Does

Given a user-defined blog topic, the pipeline:
1. Enhances the query to improve search relevance.
2. Uses Tavily API to fetch real-time information.
3. Refines the retrieved web content.
4. Generates a structured blog outline.
5. Produces a complete blog post incorporating real-time data and structure.

---

## 🧩 Tech Stack

- **LangGraph** – for building a stateful, node-based execution graph.
- **Groq + Qwen-2.5-32B** – fast LLM with low-temperature settings for precise, factual responses.
- **Tavily API** – to fetch recent web results and current information.
- **LangChain** – to invoke models and structure the pipeline components.

---

## 🧠 Pipeline Stages

### 1. `enhance_search_query`
- **Purpose**: Transforms a simple blog prompt into a refined, high-quality search query.
- **Role**: Uses the model to think like an information retrieval expert.

### 2. `web_search`
- **Purpose**: Queries Tavily with the enhanced query and pulls recent (last 30 days) search results.
- **Output**: Top 5 relevant search snippets.

### 3. `refine_web_results`
- **Purpose**: Curates the raw search results to extract only the most relevant insights.
- **Role**: The model acts as a precise data curator, avoiding hallucinations.

### 4. `generate_blog_outline`
- **Purpose**: Generates a structured and engaging outline for the blog.
- **Role**: Shapes the structure to ensure readability and flow.

### 5. `generate_blog`
- **Purpose**: Writes the complete blog based on the outline and refined information.
- **Role**: The model functions as a full-fledged blog writer.

---

## 🧾 State Definition

The shared `BlogState` across all graph nodes contains:

- `query`: Original blog topic input.
- `enhanced_query`: Model-generated refined query.
- `web_results`: Raw web search results from Tavily.
- `refined_web_results`: Cleaned, summarized relevant content.
- `outline`: Blog structure generated from curated data.
- `blog`: Final blog post.

---

## 🔁 Graph Flow

```text
START
  ↓
enhance_search_query
  ↓
web_search
  ↓
refine_web_results
  ↓
generate_blog_outline
  ↓
generate_blog
  ↓
END
