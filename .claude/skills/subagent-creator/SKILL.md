# Sub-agent Creator

Meta-skill for generating new Claude Code sub-agent definition files (.claude/agents/*.md). Creates standardized agent files with domain expertise, GRA compliance (when applicable), and proper tool access configuration.

## Trigger
When the user requests creation of a new sub-agent: "create an agent for X", "make a new sub-agent", "add agent for Y".

## Absolute Criteria (Inherited DNA)
1. **Quality**: Agent definitions must be specific enough to produce expert-level output.
2. **SOT**: Sub-agents are read-only for state.yaml. They produce output files, never modify SOT directly.
3. **CCP**: Check existing agents for naming conflicts and role overlap before creation.

## Process

### Step 1: Gather Requirements
Ask the user (max 4 questions, P4 rule):
1. What is this agent's domain expertise?
2. What specific tasks will it perform?
3. Does it need GRA compliance (research agent producing claims)?
4. What tools does it need? (Read/Glob/Grep = read-only, Write = output-producing, WebSearch/WebFetch = web access)

### Step 2: Analyze Existing Agents
Read existing agents for structural reference:
```
.claude/agents/reviewer.md        (adversarial review pattern)
.claude/agents/translator.md      (specialized task pattern)
.claude/agents/fact-checker.md    (verification pattern)
```

If GRA compliance needed, also read:
```
.claude/agents/references/gra-compliance.md
```

### Step 3: Generate Agent File

#### Standard Agent Template
```markdown
# {Agent Name}

{Role description — 2-3 sentences explaining expertise and purpose}

## Expertise
{Specific domain expertise}

## Tasks
1. {Task 1}
2. {Task 2}
...

## Output
- File: `{output file path}`

## Tools
- {tool list}
```

#### GRA Research Agent Template
```markdown
# {Agent Name}

{Role description — 2-3 sentences}

## Reference
Read `.claude/agents/references/gra-compliance.md` before starting any analysis.

## Expertise
{Specific expertise}

## Claim Prefix
{PREFIX}

## Dependencies
- Depends on: {agent names if any}

## Tasks
1. {Task 1}
...

## GRA Compliance
{Specific source requirements for this agent}

## Thinking Process
{CoT / ToT / Thought Loop — when to use each}

## Output
- File: `{output path}`
- Format: Follow gra-compliance.md section 6

## Tools
- Read, Glob, Grep (read-only access)
- WebSearch, WebFetch (when applicable)
```

### Step 4: Validate
- File name matches agent role (kebab-case.md)
- No naming conflict with existing agents
- Tool access is minimal (principle of least privilege)
- GRA agents reference gra-compliance.md

## Output
- Created `.claude/agents/{agent-name}.md`
- Summary of agent capabilities

## Tools
- Read, Glob, Grep (analyze existing agents)
- Write (create new file)
