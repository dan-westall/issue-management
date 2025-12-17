# Issue Management Agent

AI-powered ticket creation agent for Kiro CLI that streamlines issue tracking with intelligent templates, context integration, and quality validation.

## What Problem Does This Solve?

Creating consistent, high-quality tickets across different projects is time-consuming and error-prone. Teams often struggle with:

- **Inconsistent ticket quality** - Missing context, unclear requirements, poor acceptance criteria
- **Template management** - Maintaining project-specific templates and ensuring they're used correctly  
- **Context integration** - Manually gathering information from existing tickets, documentation, and repositories
- **Field mapping complexity** - Different projects require different custom fields and validation rules
- **Quality enforcement** - Ensuring tickets meet organisational standards before creation

This agent solves these problems by providing intelligent, context-aware ticket creation with automated template selection, quality validation, and seamless integration with existing tools.

## Installation

### Requirements
- Kiro CLI installed and configured
- Access to target issue tracking system (JIRA, GitHub, etc.) - optional for local file generation

### Steps
```bash
# Clone to temporary location and move contents
cd ~/.kiro/agents && git clone git@github.com:dan-westall/issue-management.git temp-issue-management && mv temp-issue-management/* . && rm -rf temp-issue-management

# Verify installation
kiro chat --agent issue-management
```

**Note:** Kiro CLI agents follow the `agents/*.json` pattern for config files, and the `issue-creation` context folder must also be in the agents directory as the resource config uses relative paths.

For detailed Kiro CLI setup, see the [official documentation](https://kiro.dev/docs/cli/custom-agents/creating/).

## Usage

### Basic Ticket Creation
```bash
# Start a chat session with the issue-management agent
kiro chat --agent issue-management

# Or provide initial context inline
kiro chat --agent issue-management "title: Create a auth system, Spike: we need to create a auth0 based authenication system"
```

**Example conversation:**
```
User: I need to create a ticket. The title is 'Add User Login Functionality' and this is for implementing secure user authentication with session management.

Agent: Do you have any spike outcome or context to include?
User: no

Agent: Now, do you have any further supporting documentation?
User: no

Agent: Does this meet the definition of ready?
User: yes

Agent: Any changes required?
User: no

Agent: Are you happy to proceed?
User: yes

Agent: Please select the issue type:
1. Epic
2. Story  
3. Task
4. Bug
5. Spike
User: 3

Agent: Select the type of work:
1. Feature Development
2. Bug Fix
3. Technical Debt
4. Research
5. Infrastructure
User: 5

Agent: Are you happy to create the ticket?
User: yes

Agent: What is the project key?
User: AA

✓ Task created: "Add User Login Functionality"
```

### With Context Integration
```
User: Create an epic for the payment system refactor, reference the existing architecture documentation

Agent: I'll create an epic and gather context from available sources.

[Agent reads relevant documentation and existing tickets]

✓ Epic created with comprehensive context:
  - Background from architecture docs
  - Links to related tickets
  - Technical considerations included
```

## Key Features

### Template-Driven Approach
- **Smart Templates:** Automatically selects appropriate template based on issue type
- **Dynamic Fields:** Context-aware field population
- **Customisable:** Modify templates for team-specific requirements

### Context Integration
- **Code Analysis:** Automatically includes relevant code snippets and file references
- **Environment Detection:** Captures system and dependency information
- **Git Integration:** Links to commits, branches, and repository context

### Quality Assurance
- **Validation Rules:** Ensures all required fields are populated
- **Content Checks:** Validates description quality and completeness
- **Consistency:** Maintains uniform formatting across all tickets

### Multi-Platform Support
- **JIRA Integration:** Native JIRA API support with custom fields
- **GitHub Issues:** Seamless GitHub integration with labels and milestones
