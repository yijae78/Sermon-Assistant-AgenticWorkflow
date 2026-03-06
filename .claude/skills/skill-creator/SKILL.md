# Skill Creator

Meta-skill for generating new Claude Code skill packages. Creates standardized skill directories with SKILL.md and references/ following the AgenticWorkflow DNA inheritance pattern.

## Trigger
When the user requests creation of a new skill: "create a skill for X", "make a new skill", "skill for Y".

## Absolute Criteria (Inherited DNA)
1. **Quality**: Generated skills must be production-ready, not stubs.
2. **SOT**: Skills do not write to state.yaml directly. Skills guide the Orchestrator (main session).
3. **CCP**: Analyze existing skills before creating new ones to maintain consistency.

## Process

### Step 1: Gather Requirements
Ask the user (max 4 questions, P4 rule):
1. What domain/task does this skill cover?
2. What are the key inputs and outputs?
3. Does it require sub-agents? If so, which expertise areas?
4. Any specific quality requirements or constraints?

### Step 2: Analyze Existing Skills
Read existing skills for structural reference:
- `.claude/skills/workflow-generator/SKILL.md`
- `.claude/skills/doctoral-writing/SKILL.md`
- `.claude/skills/sermon-orchestrator/SKILL.md`

### Step 3: Generate Skill Package

Create directory structure:
```
.claude/skills/{skill-name}/
├── SKILL.md          (skill definition + absolute criteria)
└── references/       (domain-specific reference files)
```

### SKILL.md Template

```markdown
# {Skill Name}

{Description — what this skill does and when to use it}

## Trigger
{When this skill activates}

## Absolute Criteria (Inherited DNA)
1. **Quality**: {Domain-specific quality standard}
2. **SOT**: {How this skill interacts with state.yaml}
3. **CCP**: {Code change considerations}

## Process
{Step-by-step execution protocol}

## References
{List of reference files and external resources}
```

### Step 4: Validate
- Verify SKILL.md follows DNA inheritance pattern
- Confirm all referenced files exist
- Check for conflicts with existing skills

## Output
- Created skill directory with SKILL.md
- Any necessary reference files in references/
- Summary of what was created

## Tools
- Read, Glob, Grep (analyze existing skills)
- Write (create new files)
- Bash (create directories)
