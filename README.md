# LearningMaster-MCP

**LearningMaster-MCP** is an open-source Model Context Protocol (MCP) server designed to revolutionize how developers capture, organize, and retrieve their coding knowledge. By seamlessly integrating with Notion databases, it creates a persistent, searchable knowledge base that transforms debugging experiences and accelerates project development.

## Overview

In the fast-paced world of software development, valuable problem-solving insights are often lost, leading to repetitive debugging of similar issues across different projects or even within the same one. LearningMaster-MCP addresses this critical pain point by ensuring that every learning moment, every tricky bug squashed, and every clever solution devised becomes a reusable asset.

This tool empowers developers to build a personal and (eventually) team-wide library of proven solutions that grows more valuable with every project, significantly improving productivity and efficiency. Its vision is to become the ultimate personal coding knowledge base, making knowledge capture and retrieval a natural part of the coding process.

## Value Proposition

**Stop re-solving the same problems. Start building a powerful, searchable knowledge base.**

LearningMaster-MCP helps you:
-   **Capture Knowledge Systematically:** Store new coding learnings, solutions, and contextual details with structured metadata using simple MCP tools.
-   **Retrieve Information Instantly:** Quickly find relevant past solutions and insights through flexible search, multi-field filtering, and content similarity analysis.
-   **Boost Personal Productivity:** Drastically reduce time spent on re-debugging known issues and searching for forgotten solutions.
-   **Enhance Team Collaboration:** Facilitate knowledge sharing within teams by creating a centralized, accessible repository of collective learnings (a future goal).
-   **Accelerate Onboarding:** Help new team members get up to speed faster by providing access to a rich database of resolved issues and best practices.
-   **Maintain an Offline Cache:** Access your learnings even when offline, thanks to a local markdown-based cache.
-   **Integrate with Your Workflow:** As an MCP server, it's designed to be integrated with development tools and environments that support the Model Context Protocol.
-   **Promote Consistent, High-Quality Code:** By reusing proven solutions and best practices.

## Target Audience

LearningMaster-MCP is designed for:
-   **Software Developers:** Individual developers looking to improve their personal productivity and knowledge management practices.
-   **Software Engineering Teams:** Teams aiming to create a shared knowledge base to enhance collaboration and knowledge sharing (future development).
-   **Students and Learners:** Individuals learning to code and seeking a structured way to organize their knowledge and track their progress.

## Key Features & Core Tools

LearningMaster-MCP provides a suite of tools and capabilities to manage your coding knowledge:

*   **Notion Database Integration:** Seamlessly connect to and utilize your Notion databases for storing and organizing coding knowledge.
*   **Customizable Data Structures:** Define custom database schemas within Notion to tailor the knowledge base to your specific needs.
*   **Code Snippet Management:** Dedicated support for storing, managing, and retrieving code snippets with syntax highlighting and language identification.
*   **Powerful Search Functionality:** Advanced search capabilities to quickly find relevant information based on keywords, tags, language, impact, solution status, and more.
*   **Tagging and Categorization:** Flexible options to organize knowledge based on language, framework, topic, project, or custom tags.
*   **Markdown Support:** Full support for Markdown formatting in your learning entries for rich and readable content.
*   **Local Caching:** An offline-first approach with a local markdown cache ensures you can access and often manage your learnings even without an internet connection.
*   **Bidirectional Sync (Planned):** Future capabilities for robust synchronization between Notion and the local cache.

**Primary MCP Tools:**
-   `write_learning`: Store new coding learnings with structured metadata.
-   `read_learning`: Flexible search and retrieval of stored learnings.
-   `update_learning`: Modify existing learnings with version tracking.
-   `export_learnings`: Batch export learnings by specified criteria in various formats (Markdown, JSON, CSV).
-   `search_similar`: Discover related learnings through content analysis and similarity algorithms.

*(API Access for integration with other development tools is a future development goal.)*

## Getting Started

*(Detailed setup and usage instructions will be available in the `docs/` directory as the project progresses, including guides for each tool and configuration options.)*

For now, ensure you have Node.js (v18+) and npm installed. The project setup involves:
1.  Cloning the repository.
2.  Installing dependencies (`npm install`).
3.  Configuring necessary environment variables (e.g., Notion API key and Database ID).
4.  Using Taskmaster-AI tools (via MCP) to initialize the project, parse your PRD (if any), and manage tasks.

Refer to `docs/project-setup-log.md` for a detailed log of the initial setup of this repository.

## Contributing

We welcome contributions! Please see `docs/contributing.md` for guidelines on how to contribute, coding standards, and the development workflow.

## License

This project is licensed under the MIT License with Commons Clause.
See the `LICENSE` file (to be added) for full details.
