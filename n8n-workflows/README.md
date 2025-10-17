# n8n-workflows

## Content Writer
 - The workflow uses the concept called Parallel Expert Synthesis
 - The worflow starts with a webhook, and then the fields can be parsed through the Edit block into the AI Agents
 - The begining fields are Topic, Platform and Tone. 


## Simple Helpdesk Agent
 - The workflow allows CSV data upload into Postgres database (local). If using Pinecone or another hosted Postgres, feel free to use the specific node type
 - The Upload process converts the text to vector data 
 - Fetching or searching the data uses Retrieval-Augmented Generation (RAG) technique for searching through the vector data



