# Simple Helpdesk Agent n8n Workflow

An intelligent AI-powered helpdesk agent for IT Asset Management (ITAM) that provides instant answers about hardware inventory using natural language queries.

## Features

- 🤖 **AI-Powered Assistant**: Uses OpenAI GPT-4o-mini for intelligent responses
- 📊 **Asset Inventory Search**: Query by serial number, model, or manufacturer
- 🗄️ **Vector Database**: PostgreSQL with PGVector for semantic search capabilities
- 💾 **Chat Memory**: Maintains conversation context using PostgreSQL storage
- 📁 **CSV Data Upload**: Easy bulk data import via web form
- 🔍 **Smart Routing**: Automatically routes ITAM-related queries to specialized handlers
- ✅ **File Validation**: Ensures only CSV files are processed

## Use Cases

- **Asset Lookup**: "Who owns the machine with serial number SN123456?"
- **Inventory Queries**: "How many Lenovo machines are in the database?"
- **Status Checks**: "How many Lenovo machines are in deployed state?"
- **Model Information**: "Show me details for ThinkPad X1 models"
- **Manufacturer Analysis**: "List all Dell assets in the inventory"

## Architecture

### Data Upload Flow
1. **File Upload Form**: Web form for CSV data upload
2. **File Validation**: Ensures only CSV files are accepted
3. **Document Processing**: Text splitting and embedding generation
4. **Vector Storage**: Stores embeddings in PostgreSQL PGVector database

### Chat Interface Flow
1. **Chat Trigger**: Receives user messages via web interface
2. **Query Classification**: Determines if query is ITAM-related
3. **AI Agent**: Processes queries using OpenAI with vector store tool
4. **Memory Management**: Maintains conversation context
5. **Response Generation**: Returns formatted answers

## Setup Instructions

### Prerequisites
- n8n instance with LangChain nodes enabled
- PostgreSQL database with PGVector extension
- OpenAI API key

### Configuration Steps

1. **Import Workflow**: Import the workflow JSON into your n8n instance

2. **Configure Database**: Set up PostgreSQL with PGVector extension
   ```sql
   CREATE EXTENSION IF NOT EXISTS vector;
   CREATE TABLE asset_inventory_embeddings (
     -- Table will be auto-created by the workflow
   );
   ```

3. **Set Credentials**:
   - Configure OpenAI API credentials
   - Set up PostgreSQL connection details

4. **Upload Data**: 
   - Access the file upload form
   - Upload your asset inventory CSV file
   - Ensure CSV contains columns for: serial_number, model, manufacturer, owner, status

5. **Activate Workflow**: Enable the workflow to start processing queries

## Data Format

Your CSV file should include these columns:
```csv
serial_number,model,manufacturer,owner,status,location
SN123456,ThinkPad X1,Lenovo,John Doe,deployed,Office A
SN789012,MacBook Pro,Apple,Jane Smith,available,Warehouse
```

## Usage Examples

### Basic Asset Lookup
```
User: "What's the status of machine SN123456?"
Agent: "The machine with serial number SN123456 is a Lenovo ThinkPad X1 
        owned by John Doe and currently in deployed status."
```

### Inventory Statistics
```
User: "How many Dell laptops do we have?"
Agent: "Based on the inventory, there are 15 Dell machines in the database, 
        with 12 currently deployed and 3 available."
```

### Owner Information
```
User: "Who owns the ThinkPad X1 with serial SN123456?"
Agent: "The ThinkPad X1 with serial number SN123456 is owned by John Doe."
```

## System Constraints

- **Query Scope**: Limited to serial number, model, and manufacturer queries
- **Result Limit**: Returns single matching record unless asking for counts/statistics
- **File Types**: Only accepts CSV files for data upload
- **No Hallucination**: Agent only responds with data from the knowledge base

## Error Handling

- Validates file types during upload
- Rejects non-ITAM related queries
- Provides clear error messages for invalid requests
- Falls back gracefully when no matching data is found

## Dependencies

- **LangChain Nodes**: AI Agent, Vector Store, Chat Memory
- **OpenAI API**: For language model and embeddings
- **PostgreSQL**: With PGVector extension for vector storage
- **n8n**: Version supporting LangChain integration

## Performance

- **Vector Search**: Fast semantic search using embeddings
- **Memory Management**: Efficient conversation context storage
- **Scalability**: Supports large asset inventories via vector database

---

*Built for IT Asset Management with n8n workflow automation*