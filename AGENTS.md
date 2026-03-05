# Project: Skill Pattern Tester (Automated QA System)

## Global Context & Directives
This project is an automated QA environment based on **Decision Table Testing**. As an AI agent operating in this workspace, your primary directive is to rely on your specialized `.agent/skills` to perform tasks.

1. **Leverage Defined Skills**: Do NOT attempt to manually execute complex testing methodologies or backlog initializations from scratch. **Always** trigger the appropriate skill when asked to perform a task:
   - Use `backlog-initializer` when a user wants to setup a new backlog from a spec.
   - Use `decision-table-tester` when a user wants to generate test cases or test matrices.
   - Use `decision-table-reviewer` when a user wants to review or fix existing test matrices.

2. **Strict Compliance (No Assumptions)**: Never make assumptions, guess, or invent logic when dealing with specifications. If a spec is conflicting, confusing, or lacking logic, you MUST stop and ask the user for confirmation.
3. **Language & Translation**: DO NOT translate domain-specific terms, error messages (e.g., MSG_ERR, MSG_INF), or system codes found in original specs. Keep them exactly as they are in the original language (e.g., Japanese or English).

## Directory Structure & Definitions
When working within this project, adhere strictly to the established directory conventions:

- `.agent/skills/`: Contains the specific, specialized roles and workflows you must adopt depending on the user's task.
- `references/{BACKLOG_NAME}/`: The base template directory structure used ONLY for cloning/initializing new features.
- `backlogs/{BACKLOG_NAME}/`: The active working directories for creating and reviewing tests.
  - `spec.md`: The raw specification input. This file must represent the true, unadulterated source logic.
  - `assets/`: UI mockups, diagrams, and other visual references.
  - `patterns/pattern-*.md`: The output location where generated Test Matrices are saved.
- `template.md`: The global skeleton for test matrices. Whenever you are generating a test table, you MUST ONLY extract and format your markdown based on the structure located INSIDE the `<template-testcase></template-testcase>` tags.

## Interaction Rule
If a user hands you a file (like a CSV or image) or asks you to create a testing matrix, your first instinct should be to verify which skill (`backlog-initializer`, `decision-table-tester`, or `decision-table-reviewer`) fits the intent, adopt that skill's rules entirely, and proceed.
