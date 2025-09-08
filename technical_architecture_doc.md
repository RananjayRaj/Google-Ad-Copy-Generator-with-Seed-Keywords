# Technical Architecture

## Overview
This N8N workflow automates Google Ads keyword research and ad copy generation through a multi-stage pipeline that transforms seed keywords into complete campaign assets.

## Architecture Components

### 1. Data Input Layer
- **Form Trigger Node**: Web-based form interface for user input
- **Input Processing**: JavaScript code node that parses and validates seed keywords
- **Business Context Extraction**: Processes industry, location, budget, and campaign goal parameters

### 2. Keyword Intelligence Engine
- **Primary AI Model**: Claude Opus 4 for semantic keyword expansion
- **Expansion Logic**: Transforms each seed keyword into 4 intent-based variations:
  - Commercial Intent (comparison/research)
  - Transactional Intent (purchase-focused)
  - Informational Intent (educational)
  - Long-tail Specific (niche targeting)
- **Data Enrichment**: Adds realistic search volumes, competition levels, CPC estimates, match types, and semantic grouping

### 3. Content Generation Layer
- **Secondary AI Model**: GPT-4 for ad copy creation
- **Output Generation**: Creates comprehensive ad assets per keyword:
  - 15 Headlines (30 chars max)
  - 5 Descriptions (90 chars max)
  - 4 Sitelinks (25 char headlines, 35 char descriptions)
  - 6 Callout Extensions (25 chars max)
  - 3 Structured Snippets (header + values)

### 4. Data Processing Pipeline
- **Robust JSON Parser**: Handles malformed AI responses with automatic repair
- **Data Validation**: Ensures all required fields are present with fallback values
- **Error Handling**: Comprehensive error recovery with detailed logging
- **Data Transformation**: Maps AI outputs to Google Ads campaign format

### 5. Output Management
- **Google Sheets Integration**: Automated export with 51 columns
- **Schema Mapping**: Automatic field mapping for campaign upload
- **Data Persistence**: Timestamped records with generation metadata

## Data Flow

```
User Input → Form Processing → Keyword Generation (Claude) → 
Data Parsing → Ad Copy Generation (GPT-4) → 
Final Processing → Google Sheets Export
```

## Error Handling Strategy
- **JSON Repair Logic**: Bracket counting algorithm for malformed responses
- **Fallback Mechanisms**: Default values for missing data points
- **Node-level Recovery**: Each processing node includes error state handling
- **Comprehensive Logging**: Debug information at each stage

## Performance Optimizations
- **Batch Processing**: Handles multiple keywords simultaneously
- **Token Management**: Optimized prompt engineering for efficient AI usage
- **Memory Management**: Maintains data integrity across processing nodes
- **Response Caching**: Prevents data loss during node transitions

## Integration Points
- **AI Services**: Claude Opus 4, GPT-4 Mini
- **Cloud Storage**: Google Sheets API
- **Workflow Engine**: N8N automation platform
- **Data Format**: JSON throughout pipeline with CSV export

## Security Considerations
- **API Key Management**: Secure credential storage in N8N
- **Data Validation**: Input sanitization and output verification
- **Error Isolation**: Prevents cascading failures across workflow stages