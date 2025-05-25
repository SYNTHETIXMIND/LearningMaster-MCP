```markdown
# systemPatterns.md

## 1. Architectural Design

LearningMaster-MCP adopts a modular, microservice-inspired architecture centered around a core data management service and specialized modules for Notion integration and knowledge retrieval. This allows for independent scaling and easier maintenance. The key architectural principles are:

*   **Separation of Concerns:** Each module handles a specific responsibility, minimizing dependencies and promoting reusability.
*   **API-First Design:** All modules communicate through well-defined APIs, enabling loose coupling and facilitating future integrations.
*   **Data Persistence Layer:** A dedicated data persistence layer isolates the application from specific database implementations, allowing for flexibility in database selection and migration.

The high-level architecture can be visualized as follows:

```
+---------------------+     +---------------------+     +---------------------+
|   Notion Integration  | --> |   Core Data Mgmt    | --> |  Knowledge Retrieval |
|       Module        |     |       Service       |     |       Module        |
+---------------------+     +---------------------+     +---------------------+
        ^                      ^                      ^
        | Notion API             | Data Model API      | Search API/LLM      |
        |                      | (CRUD Operations)   |                     |
+---------------------+     +---------------------+     +---------------------+
|      Notion DB      | --> |    Data Storage     | --> |     User Interface   |
+---------------------+     +---------------------+     +---------------------+
```

## 2. Data Models

The core data model revolves around the concept of a "Knowledge Item." A Knowledge Item represents a single unit of coding knowledge, such as a code snippet, a design pattern, or a best practice.

**Knowledge Item:**

*   `id` (UUID): Unique identifier for the Knowledge Item.
*   `title` (String): Title of the Knowledge Item.
*   `content` (String): The actual coding knowledge (e.g., code snippet, markdown text).
*   `tags` (List of Strings): Keywords or categories associated with the Knowledge Item.
*   `source` (String): The origin of the knowledge item (e.g., "Notion", "Stack Overflow").
*   `source_id` (String): ID of the item in the source system (e.g., Notion page ID).
*   `created_at` (Timestamp): Timestamp indicating when the Knowledge Item was created.
*   `updated_at` (Timestamp): Timestamp indicating when the Knowledge Item was last updated.
*   `metadata` (JSON): Additional metadata associated with the Knowledge Item (e.g., programming language, framework).

**Notion Page Mapping:**

A separate data structure maps Notion pages to Knowledge Items. This allows for tracking which Notion pages have already been processed and imported into the system.

*   `notion_page_id` (String): ID of the Notion page.
*   `knowledge_item_id` (UUID): ID of the corresponding Knowledge Item.
*   `status` (Enum: "processed", "pending", "error"): Status of the processing.
*   `last_processed_at` (Timestamp): Timestamp indicating when the Notion page was last processed.

## 3. API Definitions

The system exposes RESTful APIs for interacting with the core data management service and other modules.

**3.1 Core Data Management API:**

*   **`POST /knowledge-items`**: Creates a new Knowledge Item.
    *   Request Body: JSON representation of a Knowledge Item.
    *   Response: JSON representation of the created Knowledge Item with its ID.
*   **`GET /knowledge-items/{id}`**: Retrieves a Knowledge Item by ID.
    *   Response: JSON representation of the Knowledge Item.
*   **`PUT /knowledge-items/{id}`**: Updates an existing Knowledge Item.
    *   Request Body: JSON representation of the updated Knowledge Item.
    *   Response: JSON representation of the updated Knowledge Item.
*   **`DELETE /knowledge-items/{id}`**: Deletes a Knowledge Item.
    *   Response: 204 No Content.
*   **`GET /knowledge-items?tags={tag1,tag2,...}&search={query}`**: Searches for Knowledge Items based on tags and/or a search query.
    *   Response: List of JSON representations of matching Knowledge Items.
*   **`GET /notion-page-mapping/{notion_page_id}`**: Retrieves a Notion Page Mapping entry.
    *   Response: JSON representation of Notion Page Mapping.
*   **`POST /notion-page-mapping`**: Creates or updates a Notion Page Mapping entry.
    *   Request Body: JSON representation of Notion Page Mapping.
    *   Response: JSON representation of the created/updated Notion Page Mapping entry.

**3.2 Notion Integration API (Internal):**

*   **`POST /sync-notion`**: Triggers a synchronization with a specified Notion database or workspace.
    *   Request Body: {`database_id`: String (optional), `workspace_id`: String (optional)} - Provide either database_id or workspace_id.
    *   Response: 202 Accepted (indicates background processing started)

**3.3 Knowledge Retrieval API:**

*   **`GET /search?query={query}`**: Searches for Knowledge Items based on a natural language query.  This might leverage an LLM for semantic search.
    *   Response: List of JSON representations of matching Knowledge Items, potentially ranked by relevance.

## 4. Component Structure

The system is composed of the following key components:

*   **Notion Integration Module:** Responsible for interacting with the Notion API, fetching page content, and creating/updating Knowledge Items.  Handles authentication and pagination of Notion API responses.
*   **Core Data Management Service:** Provides the API for managing Knowledge Items, including CRUD operations and search functionality.  Handles data validation and persistence.
*   **Data Storage:** Responsible for storing Knowledge Items and Notion Page Mappings.  Could be a relational database (e.g., PostgreSQL) or a NoSQL database (e.g., MongoDB).
*   **Knowledge Retrieval Module:** Provides advanced search capabilities, potentially leveraging a vector database and/or an LLM (Large Language Model) for semantic search. Ranks search results based on relevance.
*   **User Interface (Optional):** Provides a web-based interface for users to browse, search, and manage Knowledge Items.

## 5. Integration Points

*   **Notion API:** The Notion Integration Module integrates directly with the Notion API to fetch and update page content. API key authentication is required.
*   **Data Storage:** All modules interact with the data storage layer through a well-defined data access layer (DAL).
*   **LLM (Optional):** The Knowledge Retrieval Module may integrate with an LLM service (e.g., OpenAI, Cohere) for semantic search.  API key authentication is required.
*   **User Interface (Optional):**  Communicates with the Core Data Management API and Knowledge Retrieval API to display and manage Knowledge Items.

## 6. Scalability Strategy

The system is designed for horizontal scalability by deploying multiple instances of each module behind a load balancer. Key strategies for scalability include:

*   **Stateless Modules:** Modules are designed to be stateless, allowing them to be easily scaled horizontally. Session state is managed externally (e.g., using a distributed cache).
*   **Database Sharding:**  For very large datasets, the database can be sharded across multiple servers.
*   **Caching:**  Aggressive caching of frequently accessed data (e.g., Knowledge Items, search results) to reduce database load. Redis or Memcached can be used for caching.
*   **Asynchronous Processing:**  Long-running tasks, such as Notion synchronization, are handled asynchronously using a message queue (e.g., RabbitMQ, Kafka).  This prevents blocking the main application threads and improves responsiveness.

Created on 25.05.2025
```