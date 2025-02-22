# Wave - An Extensible Automated Agent Framework

Wave is a powerful automated agent framework that combines browser automation, email handling, document processing, and various other capabilities into a cohesive system.

## Core Components

### Main Entry Point
- `main.py`: The primary entry point that initializes the agent and handles user interactions. Sets up configurations and manages the main command loop.

### Core Module (`wave/core/`)
- `agent.py`: The central component that coordinates all modules and handles task execution. Implements the `AutomatedAgent` class which:
  - Manages task analysis and splitting
  - Coordinates between different modules
  - Handles compound tasks
  - Maintains chat history

- `task.py`: Defines the task data structures (`Task` and `SubTask` classes) used throughout the system.
- `config.py`: Manages system-wide configuration, including:
  - Directory structures for files
  - Temporary file management
  - Environment settings

### Modules (`wave/modules/`)

#### Browser Module (`wave/modules/browser/`)
- `browser.py`: Implements browser automation using browser-use and Playwright
  - Handles web interactions
  - Manages form filling
  - Handles file downloads
  - Provides screenshot capabilities

- `domains/`: Contains domain-specific handlers for various websites
  - `__init__.py`: Defines base domain handler interface
  - `google.py`: Handles Google Workspace specific interactions

- `registry.py`: Manages domain-specific handlers and their registration

#### Email Module (`wave/modules/email.py`)
- Handles email operations (sending and reading)
- Manages attachments
- Processes email-based commands

#### Search Module (`wave/modules/search.py`)
- Implements web search functionality using SerpAPI
- Processes and analyzes search results
- Integrates with LLM for result analysis

#### Document Processing (`wave/modules/document_processor.py`)
- Handles various document formats (PDF, Word, Excel)
- Manages file creation and conversion
- Provides content analysis capabilities

#### Desktop Module (`wave/modules/desktop.py`)
- Handles desktop automation tasks
- Manages application control
- Provides keyboard and mouse automation

#### Functions (`wave/modules/functions/`)
- `clipboard.py`: Implements clipboard-related functions
- `__init__.py`: Manages function registration

### Integrations (`wave/modules/integrations/`)
- `discord_integration.py`: Handles Discord bot integration
- `email_integration.py`: Manages email-based command processing
- `__init__.py`: Exports integration modules

### Agents (`wave/modules/agents/`)
- `online_coding.py`: Specialized agent for coding platforms
- `__init__.py`: Exports agent modules

## Key Relationships

1. **Task Flow**:
   ```
   User/Integration Input → AutomatedAgent → Task Analysis → Module Selection → Task Execution → Result Processing
   ```

2. **Module Dependencies**:
   - Browser Module ← Search Module (for web searches)
   - Email Module ← Document Processor (for attachments)
   - All Modules ← Core Agent (for coordination)

3. **Integration Flow**:
   ```
   External Source → Integration → AutomatedAgent → Modules → Response → Integration → External Source
   ```

## Configuration

### Environment Variables
Required environment variables in `.env`:
- API Keys (OpenAI, OpenRouter, SerpAPI, Replicate)
- Email Configuration
- Integration Settings
- Browser Settings

### Directory Structure
```
wave/
├── core/
│   ├── agent.py
│   ├── task.py
│   └── config.py
├── modules/
│   ├── browser/
│   ├── email.py
│   ├── search.py
│   ├── document_processor.py
│   ├── desktop.py
│   ├── functions/
│   ├── integrations/
│   └── agents/
├── data/
│   ├── downloads/
│   ├── documents/
│   └── attachments/
└── main.py
```

## Features

1. **Browser Automation**
   - Web navigation and interaction
   - Form filling with validation
   - File downloads
   - Domain-specific handling

2. **Email Capabilities**
   - Sending and receiving emails
   - Attachment handling
   - Email-based command processing

3. **Document Processing**
   - Multiple format support (PDF, Word, Excel)
   - Content analysis
   - File conversion

4. **Search Functionality**
   - Web search integration
   - Result analysis
   - Content extraction

5. **Desktop Automation**
   - Application control
   - Keyboard/mouse automation
   - System interaction

6. **Integrations**
   - Discord bot support
   - Email command processing
   - Extensible integration system

## Security Features

1. **Authentication Handling**
   - Secure credential management
   - Human intervention for sensitive operations
   - Safe storage of API keys

2. **File Management**
   - Secure temporary file handling
   - Automatic cleanup
   - Permission management

3. **Input Validation**
   - Form field validation
   - Input format verification
   - Error handling

## Usage

1. **Installation**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Configuration**:
   - Copy `.env.example` to `.env`
   - Fill in required API keys and settings

3. **Running**:
   ```bash
   python main.py
   ```

## Development

1. **Adding New Modules**:
   - Create new module in `wave/modules/`
   - Implement required interfaces
   - Register with AutomatedAgent

2. **Domain Handlers**:
   - Add new handler in `wave/modules/browser/domains/`
   - Register in domain registry

3. **Integrations**:
   - Implement integration interface
   - Add to AutomatedAgent initialization 