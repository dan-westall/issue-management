# Service Instructions

**Version:** 1.1  
**Last Updated:** November 15, 2025  
**Owner:** Development Operations Team  
**References:** [Ticket Creation Rule](./issue-creation.md)

## Purpose
This context provides platform-specific instructions for integrating with different ticket services and documentation platforms when available tooling supports them.

## Instructions
- ALWAYS use platform-specific instructions when the corresponding service is available (ID: USE_PLATFORM_INSTRUCTIONS)
- ALWAYS follow service-specific API patterns and data structures (ID: FOLLOW_API_PATTERNS)
- ALWAYS handle service-specific authentication and permissions appropriately (ID: HANDLE_AUTH)
- When multiple services are available, ALWAYS prioritize based on user context and requirements (ID: PRIORITIZE_SERVICES)
- When editing this file, ALWAYS follow the LLM editing guidelines below (ID: FOLLOW_EDITING_GUIDELINES)

## Priority
Medium

## Error Handling
- If service-specific instructions conflict with main workflow, follow main workflow and note limitation
- If service authentication fails, fall back to manual processes and inform user
- If service API changes, use generic approaches and flag for instruction updates

---

## LLM Editing Guidelines

### When to Edit This File
- **Adding New Services**: Follow the established section structure for consistency
- **Updating API Calls**: When service APIs change or new endpoints become available
- **Enhancing Integration**: When new integration patterns or capabilities are discovered
- **Fixing Issues**: When service-specific problems are identified and resolved

### Section Structure Requirements
Each service section MUST include:
1. **Reading/Retrieval Instructions**: How to fetch data from the service
2. **Data Extraction Guidelines**: What information to extract and how
3. **Integration Patterns**: How to incorporate data into ticket creation
4. **Error Handling**: Service-specific fallback strategies

### API Documentation Standards
- **MUST specify exact API call names** (e.g., `getJiraIssue`, `getConfluencePage`)
- **MUST include parameter requirements** and expected data structures
- **MUST document authentication requirements** and permission considerations
- **MUST provide field mapping examples** for custom fields and metadata

### Content Extraction Guidelines
- **MUST specify what data to extract** from each service response
- **MUST provide examples** of how to process structured content
- **MUST include guidance** on handling different content types (text, tables, code)
- **MUST document link preservation** and reference maintenance

### Integration Pattern Standards
- **MUST explain how to merge** service data with ticket templates
- **MUST provide conflict resolution** strategies for overlapping data
- **MUST maintain traceability** to source materials
- **MUST ensure consistent terminology** across integrated content

### Adding New Services
When adding a new service section:
1. **Follow the established naming pattern**: `## [Service Name] Integration`
2. **Include all required subsections**: Reading, Extraction, Integration, Error Handling
3. **Provide specific API examples**: Use actual API call names and parameters
4. **Document field mappings**: Show how service fields map to ticket fields
5. **Add to Multi-Service Scenarios**: Update priority and consolidation guidance

### Maintenance Guidelines
- **Update API references** when services change their interfaces
- **Validate examples** against current service capabilities
- **Test integration patterns** with real service responses
- **Document breaking changes** in the change log
- **Maintain backward compatibility** where possible

### Quality Standards
- **Use clear, actionable language** for all instructions
- **Provide concrete examples** rather than abstract descriptions
- **Maintain consistency** with main workflow terminology
- **Ensure completeness** - all necessary information for implementation
- **Test instructions** with actual service integrations before committing

---

## Jira Integration

### Reading Existing Tickets
When Jira tickets are referenced:

**API Calls:**
- Use `getJiraIssue` to retrieve full ticket details
- Use `getJiraIssueRemoteIssueLinks` to get linked issues (depth of 1)

**Data Extraction:**
- Extract problem context from description and comments
- Identify technical requirements from acceptance criteria
- Capture business objectives from labels and components
- Map dependencies from linked issues and blockers
- Extract lessons learned from resolution comments

**Field Mapping:**
- `customfield`: Type of Work field for AA/AAA projects
- Standard fields: summary, description, priority, labels, components
- Link types: blocks, is blocked by, relates to, duplicates

### Project Validation
- Use `getVisibleJiraProjects` to retrieve available projects
- Validate project keys against user permissions
- Display project name, key, and description for confirmation

### Ticket Creation
- Use project-specific issue types from Jira configuration
- Apply custom field mappings from agent configuration
- Set appropriate priority, labels, and components
- Link to referenced tickets using appropriate link types

---

## Confluence Integration

### Reading Documentation Pages
When Confluence pages are referenced:

**API Calls:**
- Use `getConfluencePage` to retrieve full page content
- Use `getConfluencePageDescendants` to get child pages for comprehensive context

**Content Extraction:**
- Extract specifications and requirements from structured content
- Identify design decisions and their rationale
- Capture implementation guidelines and standards
- Map process workflows and procedures
- Extract historical context and lessons learned

**Domain Handling:**
- Support rs-components.atlassian.net domain references
- Handle page URLs and page IDs appropriately
- Process both public and restricted page access

### Context Integration
- Parse structured content (tables, lists, code blocks)
- Extract relevant sections based on ticket context
- Maintain links to source documentation
- Preserve formatting for technical specifications

---

## GitHub Integration

### Reading Issues and Pull Requests
When GitHub issues or PRs are referenced:

**API Calls:**
- Use GitHub API to retrieve issue/PR details
- Fetch related issues through labels and milestones
- Access linked discussions and comments

**Data Extraction:**
- Extract problem statements from issue descriptions
- Identify technical requirements from PR descriptions
- Capture implementation details from code changes
- Map dependencies through issue references and milestones
- Extract lessons learned from PR reviews and comments

**Repository Context:**
- Support organization/repository URL patterns
- Handle both public and private repository access
- Process issue numbers and PR numbers appropriately

### Integration Patterns
- Map GitHub labels to ticket system labels
- Convert GitHub milestones to project timelines
- Translate PR review comments to acceptance criteria
- Link GitHub issues to created tickets for traceability

---

## Multi-Service Scenarios

### Service Priority
When multiple services are available:
1. **Primary Source**: Use the service that contains the most relevant context
2. **Complementary Sources**: Gather additional context from secondary services
3. **Cross-Reference**: Link information across services for comprehensive context

### Data Consolidation
- Merge context from multiple sources into coherent ticket content
- Resolve conflicts by prioritizing most recent or authoritative source
- Maintain traceability to all source materials
- Ensure consistent terminology across integrated content

## Related Contexts
- [jira-ticket-creation-v2.md](./jira-ticket-creation-v2.md) (ID: MAIN_WORKFLOW)
- [agent-config.yaml](./config/agent-config.yaml) (ID: AGENT_CONFIG)

## Change Log
- 1.1 - November 15, 2025 - Added comprehensive LLM editing guidelines and maintenance standards - Development Operations Team
- 1.0 - November 15, 2025 - Initial service instructions creation - Development Operations Team
