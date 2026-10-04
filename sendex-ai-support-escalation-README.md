# Sendex — AI Support Escalation Workflow

> **Portfolio project · Fictional B2B SaaS company**  
> A RAG-assisted support escalation system that reviews HubSpot tickets, retrieves relevant internal knowledge, and routes each case to frontline Support, Engineering, or human review.

## Overview

Sendex is a fictional SMB B2B SaaS marketing-automation platform used to demonstrate an AI-assisted Support-to-Engineering escalation workflow.

The workflow is built in **Make.com** and combines **HubSpot ticket data, internal knowledge retrieval, an AI escalation agent, Airtable, Slack, and Google Sheets**.

The goal is to improve escalation quality without forcing frontline Support to perform Engineering-level investigation before a legitimate technical problem can be escalated.

## Business Problem

Support-to-Engineering handoffs frequently break down when:

- Technical-looking issues are escalated without sufficient frontline troubleshooting
- Valid defects are returned because root cause is not yet known
- Business impact is confused with technical evidence
- Internal knowledge is not checked consistently
- Escalation decisions are difficult to audit
- Support agents receive inconsistent next-step guidance

## Solution

The workflow:

1. Retrieves support tickets from HubSpot.
2. Loads the complete ticket context and custom operational fields.
3. Filters for tickets that requested escalation and have not yet been AI reviewed.
4. Queries the Sendex knowledge base for relevant known issues and troubleshooting guidance.
5. Aggregates retrieved knowledge into the AI review context.
6. Runs an AI escalation agent using the ticket plus retrieved knowledge.
7. Returns a structured operational decision:
   - `RETURN`
   - `ENGINEERING`
   - `HUMAN_REVIEW`
8. Routes the ticket through deterministic Make.com branches.
9. Updates HubSpot with the review outcome.
10. Creates escalation/audit records where appropriate.
11. Sends Slack notifications to the appropriate operational path.
12. Logs workflow outcomes in Google Sheets.

## RAG / Knowledge Retrieval

Before the AI agent makes its routing decision, the workflow queries a curated Sendex knowledge base containing material such as:

- Product support guidance
- Troubleshooting playbooks
- Engineering escalation policy
- Priority and impact guidance
- Known issues

The retrieved context is supplied directly to the escalation agent so decisions can be grounded in project-specific operational knowledge rather than model memory alone.

## Escalation Decision Framework

### RETURN

Used when meaningful frontline troubleshooting or customer-accessible information is still missing and could materially determine whether the problem is customer-side or product-side.

### ENGINEERING

Used when the available evidence reasonably supports a defect, service failure, integration/API problem, processing failure, or another technical issue requiring Engineering investigation.

The workflow does **not** require Support to prove root cause before a valid Engineering escalation.

### HUMAN_REVIEW

Used when the evidence is genuinely ambiguous, conflicting, unusual, or requires senior technical judgment.

## Key Safeguards

- High MRR or plan tier does not establish a technical defect
- High ticket priority alone does not justify Engineering escalation
- Support is not required to obtain Engineering-only diagnostics
- Multiple objects inside one account are not automatically treated as multiple affected customers
- Known-issue matches must come from retrieved knowledge
- The agent is instructed not to invent logs, outages, causes, incidents, or related tickets
- Structured output constrains the operational response

## Key Capabilities

- HubSpot ticket ingestion
- RAG-based knowledge retrieval
- Known-issue matching
- Structured AI escalation review
- Confidence scoring
- Impact-scope classification
- Missing-information identification
- Support/Engineering/human-review routing
- HubSpot updates
- Slack notifications
- Airtable escalation records
- Google Sheets audit logging

## Tech Stack

- Make.com
- HubSpot
- AI agent orchestration
- Knowledge base / RAG retrieval
- Airtable
- Slack
- Google Sheets
- Structured output schemas

## Repository Contents

- `README.md` — project overview and architecture
- `workflow.json` — sanitized portfolio version of the Make.com workflow blueprint

## Security and Sanitization

This repository contains a **sanitized portfolio export**.

Credentials, personal email addresses, connection identifiers, Slack channel/workspace identifiers, spreadsheet IDs, Airtable identifiers, and other private integration metadata have been removed or replaced with placeholders.

The workflow is provided for architecture review. Anyone adapting it must configure their own systems, credentials, resource mappings, and knowledge documents.

## Design Principles Demonstrated

- RAG before decision-making
- Clear Support-versus-Engineering ownership rules
- Human review for genuine ambiguity
- Structured decisions rather than free-form recommendations
- Explicit anti-hallucination constraints
- Deterministic downstream routing
- Auditability across operational systems

## Portfolio Context

This project was created as part of my Agentic AI Automation portfolio, with a focus on improving B2B SaaS Support-to-Engineering handoffs.

**Built by Jerry J. Hudson**
