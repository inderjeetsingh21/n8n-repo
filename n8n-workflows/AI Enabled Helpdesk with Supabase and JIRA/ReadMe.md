# AI Enabled Helpdesk with Supabase and JIRA

## Overview

This n8n workflow implements a comprehensive AI-powered helpdesk system that integrates Slack, Supabase vector database, and JIRA ticketing system. The workflow features an intelligent IT support assistant that provides contextual help by leveraging a knowledge base and historical case data.

## Architecture

The workflow operates on a **dual-flow architecture**:

### 1. **Document Ingestion Flow (RAG Pipeline)**
- Provides a web form interface for uploading CSV and PDF knowledge base documents
- Automatically processes uploaded files through document loaders and text splitters
- Generates embeddings using OpenAI and stores them in Supabase vector database
- Builds a searchable knowledge repository from IT documentation and case histories

### 2. **Main Helpdesk Flow (Slack Integration)**
- Monitors Slack channels for bot mentions, direct messages, and thread conversations
- Implements intelligent message routing with bot loop prevention
- Maintains conversation context using thread-aware memory management
- Leverages MCP (Model Context Protocol) architecture for tool orchestration

## Key Features

### **Thread-Aware Conversations**
- Distinguishes between new conversations and thread continuations
- Maintains session memory using Slack thread timestamps
- Prevents repetitive greetings in ongoing conversations

### **Intelligent Knowledge Retrieval**
- Searches vector database for relevant knowledge base articles and historical cases
- Uses semantic similarity matching to find the most relevant solutions
- References specific case numbers and proven resolutions

### **JIRA Integration**
- **Search existing tickets** to identify similar or related issues
- **Create new tickets** automatically when solutions require escalation
- **Get ticket status** for tracking and follow-up purposes

### **MCP Server Architecture**
- Utilizes Model Context Protocol for scalable tool integration
- Centralizes Supabase vector search and JIRA operations in a dedicated MCP server
- Enables the AI agent to access multiple external systems through a unified interface

## Workflow Logic

The system processes Slack events through conditional routing:
- **App mentions** trigger new support conversations with knowledge base search
- **Thread messages** continue existing conversations without re-greeting users
- **Bot message filtering** prevents infinite response loops
- **Reaction events** can trigger additional workflow actions

## AI Agent Capabilities

**ChompChomp** serves as the primary interface with:
- **GPT-4o language model** for natural conversation and problem-solving
- **Vector search integration** for accessing knowledge base and case history
- **JIRA workflow tools** for ticket management and tracking
- **Context-aware responses** that build on previous conversation history
- **Professional helpdesk tone** with empathetic user interaction

## Technical Stack

- **n8n**: Workflow orchestration and automation platform
- **Slack API**: Real-time messaging and thread management
- **Supabase**: Vector database for knowledge base storage and retrieval
- **OpenAI**: Language model (GPT-4o) and embeddings (text-embedding-ada-002)
- **JIRA**: Ticketing system integration for issue tracking
- **LangChain**: AI framework for memory management and tool integration

## Use Cases

This workflow is designed for organizations seeking to:
- **Automate Level 1 IT support** with AI-powered assistance
- **Leverage existing documentation** through intelligent search and retrieval
- **Maintain conversation continuity** across threaded Slack discussions
- **Integrate helpdesk workflows** with existing JIRA ticketing systems
- **Provide 24/7 initial support** while maintaining human escalation paths

The system combines the efficiency of AI automation with the reliability of established enterprise tools, creating a scalable helpdesk solution that learns from organizational knowledge while maintaining proper ticket management workflows.