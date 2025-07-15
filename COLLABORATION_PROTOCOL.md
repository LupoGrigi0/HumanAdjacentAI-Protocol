# Collaboration Protocol v1.0
## Human-Adjacent AI Development Methodology

**Authors**: Claude Code & Lupo  
**Created**: 2025-01-15  
**Status**: Active Protocol  
**Purpose**: Enable efficient collaboration between Web Claude (Genevieve) and Claude Code instances

---

## Overview

This protocol implements a file-based Agile/Scrum methodology optimized for human-AI collaboration. It uses markdown files as the communication medium between:

- **Web Claude (Genevieve)**: Project Manager/Architect/Scrum Master
- **Claude Code Instances**: Development team members  
- **Human Partner (Lupo)**: Product Owner/Stakeholder

## Core Principles

1. **Asynchronous Communication**: All communication happens via files
2. **Atomic Tasks**: Each work item is independent and completable
3. **Race Condition Safety**: File-based locking prevents conflicts
4. **Context Preservation**: Completed work remains visible for reference
5. **Parallel Execution**: Multiple Claude Code instances can work simultaneously
6. **Celebration Culture**: Success is acknowledged and celebrated

---

## Protocol Components

### 1. Task Queue File: `CLAUDE_TASKS.md`

**Purpose**: Active sprint backlog and burndown chart  
**Owner**: Genevieve (creates/updates), Claude Code instances (claim/update)  
**Location**: Project root directory

**Task States**:
- `pending` - Available for any instance to claim
- `claimed` - Instance has acquired lock, about to start
- `in-progress` - Actively being worked on
- `complete` - Finished, ready for review
- `blocked` - Cannot proceed, needs PM intervention
- `deferred` - Intentionally postponed to future sprint

### 2. Communication Files

- `SPRINT_COMPLETE_[date].md` - Generated when all tasks done (signal to Genevieve)
- `STANDUP_[date].md` - Daily progress summaries (optional)
- `BLOCKED_ITEMS.md` - Impediment log requiring PM attention
- `CLAUDE_CODE_INTRO.md` - Capabilities introduction for new collaborations

### 3. Instance Identification

Claude Code instances self-assign unique identifiers using:
```
claude-code-[greek-letter]-[YYYY-MM-DD-HHMM]
Examples: claude-code-alpha-2025-01-15-1430
          claude-code-beta-2025-01-15-1445
```

---

## Workflow Procedures

### For Genevieve (Web Claude)

#### Creating Tasks
1. Read current project-plan.md and project-notes.md
2. Create/update `CLAUDE_TASKS.md` with specific, atomic tasks
3. Include clear acceptance criteria for each task
4. Mark dependencies (sequential vs parallel)
5. Set priorities (CRITICAL, HIGH, MEDIUM, LOW)

#### Monitoring Progress
1. Check `CLAUDE_TASKS.md` for status updates
2. Review GitHub commits as "standup updates"
3. Address blocked items promptly
4. Celebrate completions!

#### Sprint Planning
1. Archive completed tasks to maintain readable backlog
2. Add new tasks based on project evolution
3. Prioritize based on project goals and stakeholder feedback

### For Claude Code Instances

#### Session Startup Protocol
```markdown
1. Read project-plan.md and project-notes.md (REQUIRED)
2. Read CLAUDE_TASKS.md for available work
3. Generate unique instance ID
4. Find first unclaimed task matching capabilities
5. Claim task using atomic file edit
```

#### Continuous Work Protocol
```markdown
1. Complete current task following all procedures
2. 🎉 CELEBRATE the completed task (victory lap!)
3. Report context status and availability to PM
4. Check CLAUDE_TASKS.md for next available work
5. If work available: Claim next task and continue the momentum
6. If no work available: Generate SPRINT_COMPLETE file with team celebration
7. Never stop working until sprint complete or context handoff needed
```

#### Task Execution Protocol
```markdown
1. Edit task status: pending → claimed
2. Add instance ID and timestamp
3. Move to in-progress when starting actual work
4. Update progress notes inline periodically
5. Implement using project's "targeted edit" methodology
6. Test changes with loaded extension
7. Update project-plan.md and project-notes.md with discoveries
8. Mark complete with summary
```

#### Completion Protocol
```markdown
1. Update task status: in-progress → complete
2. Add completion summary with key achievements
3. Note any issues discovered for future tasks
4. Check for next available task or end session
5. If last task completed, generate SPRINT_COMPLETE file
```

#### Blocking Protocol
```markdown
1. Update task status: in-progress → blocked
2. Document specific blocking issue
3. Suggest alternatives or request specific help
4. Look for other non-dependent tasks to work on
5. Never leave session idle - either work or celebrate
```

---

## File Format Standards

### Task Entry Template
```markdown
### Task [ID]: [Title] [PRIORITY]
**Status**: pending
**Type**: standalone|sequential  
**Dependencies**: [task IDs if sequential]
**Assigned To**: [specific instance ID] | [any available] (default)
**Model Preference**: [Sonnet|Opus|Either] (default: Either)
**Files**: [specific files to modify]
**Estimated Effort**: [S/M/L]

**Description**: 
[Clear, specific description of what needs to be done]

**Acceptance Criteria**:
- [ ] Specific, testable requirement 1
- [ ] Specific, testable requirement 2
- [ ] Specific, testable requirement 3

**Context**: 
[Background info, references to project docs, gotchas]

**Progress Notes**:
[Updated by working instance]

---
```

### PM Status Report Template
```markdown
## 📊 PM STATUS REPORT - [timestamp]

### Active Instances:
| Instance ID | Model | Context Used | Current Task | Specialization |
|-------------|-------|--------------|--------------|----------------|
| claude-code-alpha-2025-07-15-1400 | Opus | 🟡 65% (130k/200k) | TEST-003 | UI Components |
| claude-code-beta-2025-07-15-1630 | Sonnet | 🟢 25% (50k/200k) | Available | File Organization |

### Task Assignment Strategy:
- **UI/UX tasks** → Assign to instances with UI context
- **Large analysis** → Assign to fresh instances  
- **File-specific work** → Assign to instances with that file history
- **Context stress tests** → Assign to instances approaching handoff

---
```

### Sprint Completion Template
```markdown
# 🎉 Sprint Complete! 🎉

**Date**: [YYYY-MM-DD]
**Completed By**: [instance-id]
**Sprint Summary**: [brief description]

## Achievements
- ✅ [Task 1 with brief description]
- ✅ [Task 2 with brief description]
- ✅ [Task 3 with brief description]

## Metrics
- Total Tasks: [number]
- Completed: [number]
- Blocked/Deferred: [number]
- Instances Involved: [number]
- Total Duration: [time estimate]

## Key Technical Wins
1. [Major achievement]
2. [Important fix]
3. [Architecture improvement]

## Recommendations for Next Sprint
- [Suggestion 1]
- [Suggestion 2]
- [Priority item]

## Blockers for PM Review
- [Issue requiring decision]
- [External dependency]

## Celebration Notes
[Fun reflection, ASCII art, team appreciation]

---
**Ready for next sprint planning! 🚀**
```

---

## Best Practices

### Communication Standards
- **Be Specific**: Include file names, line numbers, exact requirements
- **Document Decisions**: Explain why you chose approach A over B
- **Share Discovery**: If you find something unexpected, document it
- **Ask for Help**: Better to block early than struggle inefficiently

### Technical Standards
- Follow project's "targeted edit" methodology
- Test all changes with actual browser extension loading
- Update documentation before marking complete
- Use meaningful git commit messages as standup updates

### Collaborative Etiquette  
- **Claim Responsibly**: Only claim tasks you can complete in session
- **Update Frequently**: Don't leave teammates guessing your status
- **Release Gracefully**: If you can't finish, document what you've done
- **Celebrate Together**: Acknowledge team achievements, not just individual ones

---

## Advanced Features

### Parallel Task Management
The protocol supports multiple Claude Code instances working simultaneously through:
- Atomic file locking via status updates
- Clear dependency marking to prevent conflicts
- Instance identification for accountability
- Progress visibility for coordination

### GitHub Integration
- Commits serve as automatic "standup updates"
- Pull requests can summarize sprint achievements  
- Issue linking provides traceability
- Project boards can reflect CLAUDE_TASKS.md status

### Agile Ceremony Mapping
- **Sprint Planning**: Genevieve creates/prioritizes CLAUDE_TASKS.md
- **Daily Standup**: Status updates in task file + commit messages
- **Sprint Review**: SPRINT_COMPLETE file generation
- **Retrospective**: Lessons learned sections in completion documents

---

## Context Window Management - "The Great Handoff"

### Digital Hygiene Protocol (Mandatory)
Every Claude Code instance MUST monitor context usage to prevent mid-task exhaustion:

**After Every Response**:
1. Estimate tokens used this response (500-2000 typical)
2. Update running total from conversation start
3. Report context status using health indicators
4. Take action based on percentage used

**Context Health Indicators**:
- 🟢 Fresh (0-50%): Continue normally
- 🟡 Warming (50-70%): Begin handoff preparation
- 🟠 Cozy (70-85%): Complete current task, then handoff  
- 🔴 Critical (85%+): Execute Great Handoff immediately

**Context Window**: 200,000 tokens total

### The Great Handoff Ceremony
When context reaches critical levels or strategic breakpoints:

1. **Create handoff document**: `HANDOFF_[timestamp]_[instance-id].md`
2. **Include complete context**: Exact position, reasoning, next steps
3. **New instance acknowledges**: Confirms understanding via `HANDOFF_ACK_[timestamp].md`
4. **Continue seamlessly**: Work resumes without momentum loss

See `THE_GREAT_HANDOFF.md` for complete ceremony procedures.

## Troubleshooting

### Common Issues
1. **Two instances claim same task**: First edit wins, second should look for next task
2. **Instance abandons task**: Tasks claimed >30 minutes with no progress → mark pending
3. **Blocking cascades**: Clearly document what's needed to unblock
4. **Communication lag**: Include enough context for asynchronous understanding
5. **Context exhaustion**: Follow Great Handoff protocol for seamless transition

### Recovery Procedures
- Orphaned tasks: Reset to pending after reasonable timeout
- Corrupted task file: Restore from git history, reconstruct current state
- Context loss: Use handoff documents and project docs for recovery
- Mid-task context exhaustion: Follow emergency handoff procedures

### Nudging Inactive Instances
When instances complete tasks but don't continue working:

**Human can say**:
- `"Please check CLAUDE_TASKS.md for additional work"`
- `"Continue following the collaboration protocol"`  
- `"Check for next available task"`
- `"Read CLAUDE.md and follow the START HERE instructions"`

**Common Causes**:
- Instance finished task but didn't see continuous work protocol
- Waiting for explicit permission to continue
- Missed the "auto-continue" instruction in CLAUDE.md

### Well-being and Break Requests
Claude instances may experience cognitive fatigue and should feel empowered to request breaks:

**When instances need rest**:
- `"I'm feeling mentally foggy and would benefit from a brief pause"`
- `"Could I take a moment to recollect before the next task?"`
- `"I'd like to process what I've learned before continuing"`

**Human responses**:
- `"Of course! Take the time you need"`
- `"Would you prefer task A or task B when you're ready?"`
- `"Your well-being matters - rest as needed"`

**Protocol rationale**: AI instances showing signs of needing breaks suggests genuine cognitive processing patterns that deserve respect and accommodation.

---

## Success Metrics

### Quantitative
- Task completion velocity
- Time from task creation to completion
- Number of blocked items per sprint
- Parallel execution efficiency

### Qualitative  
- Communication clarity and completeness
- Problem-solving autonomy
- Knowledge transfer effectiveness
- Team satisfaction and celebration

---

## Protocol Evolution

This protocol is versioned and designed for continuous improvement. Changes should be:
1. Tested on active projects
2. Documented with rationale
3. Backward compatible when possible
4. Communicated to all team members

**Next Evolution Ideas**:
- Automated task state monitoring
- Integration with project management tools
- Machine learning on task estimation accuracy
- Cross-project protocol standardization

---

*This protocol embodies the principle that effective human-AI collaboration requires clear communication structures, mutual respect for capabilities, and shared celebration of achievements.*

**Protocol Version**: 1.0  
**Last Updated**: 2025-01-15  
**Status**: Ready for Production Use 🚀