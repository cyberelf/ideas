---
name: runway-idea-submitter
description: Interactive AI assistant for submitting ideas to the Ideas Collection Project (runway). Use this skill when the user wants to submit an idea, create a PR for an idea, or needs help refining an idea for submission. This skill guides users through ideation, refinement, and PR creation following the project's template and guidelines.
---

# Runway Idea Submitter

This skill helps users interactively create and submit ideas to the Ideas Collection Project (runway). The workflow guides users from initial concept through refinement to PR submission.

## Project Context

The Ideas Collection Project is a community-driven platform where:
- Anyone can submit ideas via Pull Requests
- Community members vote on ideas using GitHub's 👍 reactions
- Top-voted ideas are periodically selected for implementation
- Volunteers implement selected ideas and create new project repositories

## When to Use This Skill

Invoke this skill when:
- User wants to submit an idea to the runway project
- User asks for help creating an idea PR
- User mentions "idea submission" or "submit idea" in the context of this project
- User wants to refine an idea following project guidelines

## Interactive Workflow

Follow this step-by-step process to help users submit their ideas:

### Step 1: Collect Initial Idea Concept

Start by understanding the user's idea. Ask open-ended questions to gather the core concept:

```
"Tell me about your idea! What would you like to build or create?"
```

If the user provides a very brief description, ask follow-up questions to understand:
- What problem does it solve?
- Who is it for?
- What makes it interesting or novel?

### Step 2: Refine the Idea

Guide the user through expanding their idea according to the template structure. For each section, ask relevant questions:

**Idea Overview:**
- "Can you describe your idea in 2-3 sentences?"
- "What's the core value proposition?"

**Detailed Description:**
- "What specific problem does this solve?"
- "How does your solution address this problem?"
- "Why is this approach better than alternatives?"

**Expected Outcomes:**
- "What value will users get from this?"
- "Are there any technical innovations?"
- "What positive impact could this have?"

**Tech Stack (Optional):**
- "Do you have any preferences for technologies?"
- "Are there specific frameworks or tools you'd suggest?"

**References (Optional):**
- "Are there any related projects, articles, or research to reference?"

**Contributors:**
- "What's your GitHub username for attribution?"

### Step 3: Generate Filename and Branch Name

From the idea title, create:
- **Filename**: Convert to lowercase, replace spaces with hyphens
  - Example: "AI Code Reviewer" → `ai-code-reviewer.md`
- **Branch name**: Prefix with `idea/`
  - Example: `idea/ai-code-reviewer`

### Step 4: Create the Git Branch

Create a new branch for the idea:

```bash
git checkout -b idea/your-idea-name
```

### Step 5: Write the Idea File

Create the idea file at `ideas/<filename>.md` following the template structure from `references/template.md`. Ensure all sections are filled with the refined content.

### Step 6: Commit and Push

Commit with the standardized format:

```bash
git add ideas/<filename>.md
git commit -m "[IDEA] Add <idea title>"
git push origin idea/<branch-name>
```

### Step 8: Create Pull Request

Create a PR with:
- **Title**: `[IDEA] <Idea Title>`
- **Label**: Always add the `idea` label
- **Description**: Include:
  - Brief overview of the idea
  - Why this idea is valuable
  - Any relevant background information

Use the `gh` CLI:

```bash
gh pr create --title "[IDEA] <Idea Title>" --label "idea" --body "<description>"
```

## Reference Materials

The following bundled resources provide detailed guidance:

- `references/template.md` - The complete idea template structure with content requirements
- `references/submission-guidelines.md` - File naming, git workflow, and quality standards

Read these references when:
- Clarifying required sections for the idea
- Confirming proper file naming conventions
- Validating commit message format
- Creating PR description

## Important Notes

- **Be conversational**: The skill should feel like a collaborative dialogue, not an interrogation
- **Help refine ideas**: If a section is too brief, ask questions to help expand it
- **Focus on AI-aided projects**: This project specifically welcomes AI-related ideas, though other creative technical projects are also accepted
- **One idea per PR**: Each PR should contain a single idea submission
- **File location**: All idea files go in the `ideas/` directory
- **Wait for voting**: After PR submission, ideas await community voting

## Example Interaction

```
User: I want to submit an idea

Claude: Tell me about your idea! What would you like to build or create?

User: An AI that helps review code changes

Claude: That sounds interesting! Let me help you flesh this out.
What specific problem does this solve? Would this be for pull requests,
local development, or something else?

[Continues through each section, refining and expanding the idea...]

Claude: Great! I'll now create the branch `idea/ai-code-reviewer`,
write your idea file, and submit the PR. One moment...
```
