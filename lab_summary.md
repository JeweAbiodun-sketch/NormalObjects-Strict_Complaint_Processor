# Lab Summary

## Project Title

Strict Complaint Processor

## Goal

Build a structured LangGraph workflow that processes fictional **Downside Up** complaints in a controlled, auditable way.

## What It Does

The notebook accepts a complaint, assigns an initial category, validates whether the complaint is in scope, then either rejects it or continues through severity assessment, resolution planning, and final response formatting.

## Main Components

- `ComplaintState`: shared TypedDict used across all nodes
- `intake_node`: performs initial categorization
- `validate_node`: checks if the complaint is truly relevant
- `reject_node`: returns a polite rejection for invalid complaints
- `categorize_node`: assigns severity for valid complaints
- `resolve_node`: generates actionable resolution steps
- `output_node`: formats the final response

## Workflow

`intake -> validate -> [reject | categorize -> resolve -> output]`

This branching structure makes the process predictable and easy to inspect.

## Tools and Libraries

- LangGraph for the state machine
- LangChain for model calls and message handling
- OpenAI API for LLM responses
- `python-dotenv` for loading environment variables
- Jupyter Notebook for interactive development and testing

## Key Learning Outcomes

- How to use a typed shared state in a graph workflow
- How conditional edges control branching logic
- How to keep AI-driven processing auditable
- How LangGraph differs from a freeform agent approach

## Testing

The notebook includes five sample complaints:

- Four valid Downside Up complaints
- One invalid complaint that should be rejected

The final assertion checks that the invalid complaint is rejected successfully.

## Reflection

This lab shows how structured orchestration can make LLM workflows more reliable than ad hoc prompting alone. The explicit state, branching rules, and workflow trace make the output easier to debug and easier to explain.
