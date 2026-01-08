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

### Step 2: Background Research

Research similar projects, products, and solutions to understand the landscape. Use web search to find:

1. **Search for existing solutions:**
   ```
   "Let me search for similar projects and products to understand what's already out there..."
   ```
   Use WebSearch to find:
   - Existing products or apps solving similar problems
   - Open source projects on GitHub
   - Recent articles or discussions about this space

2. **Analyze findings:**
   - What are the key competitors/similar projects?
   - What features do they offer?
   - What are their limitations or pain points?
   - What gaps exist in the market?

3. **Identify differentiation:**
   - How is the user's idea different?
   - What unique value does it provide?
   - What problem does it solve better than existing solutions?

4. **Document in Background Research section:**
   - List 2-5 similar products/projects with brief descriptions
   - Note their strengths and weaknesses
   - Explain how the user's idea is different or better
   - Identify market opportunities

### Step 3: Refine the Idea

Guide the user through expanding their idea according to the template structure. For each section, ask relevant questions:

**Idea Overview:**
- "Can you describe your idea in 2-3 sentences?"
- "What's the core value proposition?"

**Background Research:**
- Based on research findings, summarize:
  - "Here are some similar projects I found: [list]"
  - "Your idea differs because: [explain]"

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

### Step 4: Generate Filename and Branch Name

From the idea title, create:
- **Filename**: Convert to lowercase, replace spaces with hyphens
  - Example: "AI Code Reviewer" → `ai-code-reviewer.md`
- **Branch name**: Prefix with `idea/`
  - Example: `idea/ai-code-reviewer`

### Step 5: Create the Git Branch

Create a new branch for the idea:

```bash
git checkout -b idea/your-idea-name
```

### Step 6: Get Contributor Information (Username and Email)

Before writing the idea file, get the user's GitHub username and email for the Contributors section. Try these methods in order:

1. **Try GitHub CLI:**
   ```bash
   gh api user --jq '.login' 2>/dev/null
   gh api user --jq '.email' 2>/dev/null
   ```

2. **Try local git config:**
   ```bash
   git config --local github.user
   git config --local github.email
   ```

3. **Try global git config:**
   ```bash
   git config --global github.user
   git config --global github.email
   ```

4. **Try parsing remote URL:**
   ```bash
   git remote get-url origin 2>/dev/null | sed -n 's/.*:\(.*\)\/.*/\1/p' | head -1
   ```

5. **If all fail, ask the user:**
   ```
   "What's your GitHub username and email? (I'll use this in the Contributors section)"
   ```

6. **If user provides information manually, remember it locally for future use:**
   ```bash
   git config --local github.user <username>
   git config --local github.email <email>
   ```

### Step 7: Write the Idea File

Create the idea file at `ideas/<filename>.md` following the template structure from `references/template.md`. Ensure all sections are filled with the refined content, and use the actual GitHub username obtained in Step 6 for the Contributors section (format: `[@username] - Idea Author`).

### Step 8: Commit and Push

Commit with the standardized format:

```bash
git add ideas/<filename>.md
git commit -m "[IDEA] Add <idea title>"
git push origin idea/<branch-name>
```

### Step 9: Create Pull Request

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
