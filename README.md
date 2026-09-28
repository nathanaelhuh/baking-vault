Baking Vault 🥐🍰
Project Status: 🏗️ In Planning & Conceptual Architecture Phase

Baking Vault is an offline-first, AI-enhanced recipe management application designed to bridge the gap between unstructured social media content (Instagram reels, web blogs, personal bookmarks) and a structured, hands-on kitchen baking workbench.
Instead of taking manual screenshots or digging through bookmarked posts, users will share links directly to Baking Vault. An async ingestion engine will scrape the raw content, use an LLM to extract clean ingredient lists, precise measurements, baking temperatures, and instructions, and push the structured result directly to an offline-first local database.
🎯 Problem Statement & Core Vision
The Problem: Modern baking recipes are scattered across Instagram captions, social video descriptions, personal blogs, and ad-heavy sites. Captions lack standardized measurements, blogs hide recipes behind narrative fluff, and web apps require active internet access at the flour-dusted workbench.
The Solution: A unified, local-first vault that ingests raw URLs, leverages AI to extract structured JSON data, and provides dedicated baking tools (baker's percentages, inline timers, ingredient scaling) that function 100% offline.
🚀 Planned Feature Matrix
1. Unified Content Ingestion
Native OS Share Target: Share URLs directly from Instagram, TikTok, or mobile browsers via native iOS/Android share sheets.
AI Recipe Extraction Engine: Multi-modal extraction pipeline using LLMs and OCR to parse messy captions, carousel images, and blog HTML into structured JSON.
Noise Reduction: Automatically strips narrative backstory, sponsor ads, and browser trackers to store clean recipe data.
2. Offline-First Storage & Synchronization
Instant Local Access: Embedded SQLite database ensures zero-latency reads, search, and recipe editing without internet access.
Asynchronous Sync Engine: Offline edits (batch notes, recipe tweaks) are queued locally and automatically synced to cloud storage (Supabase) when reconnected.
GitOps-Style Versioning Concept: Ability to fork a recipe into personal variations while preserving the original imported baseline.
3. Interactive Baking Workbench
Dynamic Ingredient Scaler: Instantly scale recipe yield by target weight, serving size, or key ingredient constraint (e.g., "I only have 350g of flour left").
Baker's Percentages & Unit Toggles: Automatic calculation of baker's percentages for bread/doughs and standard-to-metric conversions (g, ml, oz, cups).
Hands-Free Baking Assistant: Large-type screen view with step-by-step checklists and inline countdown timer triggers for proofing and baking phases.
4. Search, Tags & Batch Notes
Semantic Vector Search: Natural language search powered by vector embeddings (pgvector) allowing queries like "soft chewy cookies with brown butter" or "high-hydration sourdough".
Batch Log & Note Drawer: Attach photo logs, oven temperature adjustments, and tasting notes to every recipe version offline.
🏗️ High-Level System Architecture
 [ External Apps ]          [ Mobile Device ]                 [ Cloud Backend ]
 (Instagram, Web)            (Flutter Client)                (Python + Supabase)
        │                           │                                 │
        │── (Native Share Sheet) ──>│                                 │
        │                           │── 1. Optimistic SQLite Save ───>│
        │                           │   (Status: Pending Parse)       │
        │                           │                                 │── 2. Web Scraper & OCR
        │                           │                                 │── 3. LLM JSON Structuring
        │                           │                                 │── 4. Generate Embeddings
        │                           │                                 │
        │                           │<── 5. Supabase Realtime Push ───│
        │                           │   (Updates Local SQLite)        │
🛠️ Proposed Technology Stack
Layer	Proposed Tool	Rationale
Frontend App	Flutter (Dart)	Cross-platform desktop/mobile support, background workers, and native share extension targets.
Local Persistence	SQLite (drift)	Reactive local DB supporting live UI streams and robust offline-first synchronization.
Cloud Database	Supabase (PostgreSQL)	Managed backend with built-in Row Level Security, real-time sync channels, and vector storage (pgvector).
Ingestion Worker	Python (FastAPI + Playwright)	Headless browser execution for JS-heavy sites and web scrapers (BeautifulSoup, instaloader).
AI Processing	Gemini / Pydantic AI	High-speed structured JSON generation, vision OCR for carousel images, and embedding generation.