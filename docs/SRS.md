1. Define Core Functional Requirements (User Stories)
FR-1 (Ingestion): System fetches recipe records and step-by-step blocks from Notion via API.
FR-2 (Persistence): System caches fetched recipes into local SQLite for offline availability.
FR-3 (Scaling Engine): User can adjust serving size or baker’s percentages, triggering automatic recalculation of ingredient quantities.
FR-4 (Fallbacks): If offline or API token fails, system seamlessly loads last-cached SQLite state without crashing.
2. Define Non-Functional Requirements
Latency: Initial app load from local SQLite under 200 ms.
Security: API keys and Database IDs stored in environment variables (.env), never hardcoded or committed to GitHub.
