# Claude Code Generation Protocol

*Optimized for Claude's capabilities and limitations*

## Quick Reference Checklist

Before starting any coding project, ensure you:

- [ ] Break project into logical modules (100-300 lines each)
- [ ] Use artifacts for all code components
- [ ] Include status summaries after each response
- [ ] Provide clear handoff instructions
- [ ] Save artifacts externally for session recovery

---

## Protocol Instructions

### Phase 1: Project Planning

**Always start with architectural planning:**

1. **Request a modular breakdown:**
   - "Break this project into 5-8 logical modules"
   - "Show dependencies between components"
   - "Prioritize modules by implementation order"

2. **Get implementation roadmap:**
   - "Create a step-by-step implementation plan"
   - "Estimate complexity/size of each module"
   - "Identify potential integration challenges"

### Phase 2: Incremental Development

**Module Development Rules:**

- **One module per response** - never request multiple modules at once
- **100-300 lines maximum** per artifact
- **Complete, testable units** - each artifact should run independently when possible
- **Clear interfaces** - define inputs/outputs for each module

**Request Format:**

```
"Create [MODULE_NAME] with the following requirements:
- [Specific functionality]
- [Input/output specifications]
- [Dependencies on other modules]
- [Testing requirements]

Use an artifact and include status summary at the end."
```

### Phase 3: Checkpointing & Status Management

**After Each Response, Claude Must Include:**

1. **Completion Status:**

   ```
   ✅ COMPLETED: [Module/Function names]
   🔄 IN PROGRESS: [Current work]
   ⏳ NEXT: [Specific next steps]
   ```

2. **Dependency Status:**

   ```
   READY TO IMPLEMENT: [Modules with all dependencies met]
   WAITING FOR: [Modules blocked by dependencies]
   ```

3. **Integration Notes:**

   ```
   INTEGRATION POINTS: [How this connects to other modules]
   TESTING STATUS: [What can be tested now]
   ```

### Phase 4: Session Recovery Protocol

**When Resuming Work (New Conversation):**

1. **Provide Context Package:**

   ```
   "I'm resuming a coding project. Here's the current state:

   PROJECT: [Brief description]
   
   COMPLETED MODULES:
   [Copy-paste all completed artifact code]
   
   LAST STATUS:
   [Copy the status summary from last response]
   
   CURRENT TASK:
   [Specific next step to continue]"
   ```

2. **Request Status Confirmation:**
   - "Please confirm you understand the current state"
   - "What should we work on next based on this status?"

### Phase 5: Quality Assurance

**Before Finishing Each Module:**

- [ ] Code runs without syntax errors
- [ ] All functions have clear docstrings
- [ ] Integration points are clearly marked
- [ ] Testing approach is documented

**Before Project Completion:**

- [ ] All modules are integrated
- [ ] End-to-end testing instructions provided
- [ ] Documentation is complete
- [ ] Deployment/usage instructions included

---

## Best Practices

### For Users

- **Save artifacts immediately** - copy code to your local files after each response
- **Keep conversation focused** - one module/feature per message thread when possible
- **Be specific** - vague requests lead to unusable code
- **Test incrementally** - verify each module before requesting the next

### For Complex Projects

- **Use multiple conversations** - start new chats for major feature branches
- **Maintain a master status doc** - track overall project progress externally
- **Version your artifacts** - save timestamped copies of working code
- **Create integration conversations** - dedicated threads for combining modules

### Recovery Strategies

- **Archive completed modules** - save working code outside Claude immediately
- **Document integration points** - note how modules connect to each other
- **Keep detailed status logs** - maintain your own progress tracking
- **Test frequently** - verify code works before requesting additions

---

## Common Failure Points & Solutions

| **Problem** | **Solution** |
|-------------|-------------|
| Code gets cut off mid-response | Request smaller chunks (under 200 lines) |
| Lost context between sessions | Use the Session Recovery Protocol |
| Integration issues between modules | Request explicit integration code/instructions |
| Syntax errors in generated code | Ask for syntax validation after each module |
| Overwhelming artifact size | Break into smaller, focused components |

---

## Template Requests

### Starting a Project

```
"I need to build [PROJECT_DESCRIPTION]. Please:
1. Break this into 5-8 logical modules
2. Show the implementation order
3. Identify dependencies between modules
4. Create a development roadmap

Follow the Claude Code Generation Protocol for all responses."
```

### Continuing Work

```
"Continue the [PROJECT_NAME] project. 
Current status: [PASTE_LAST_STATUS]
Next task: Create [SPECIFIC_MODULE]
Requirements: [DETAILED_SPECS]

Use artifact and provide status summary."
```

### Integration Phase

```
"Integrate modules [A] and [B]:
[PASTE_MODULE_A_CODE]
[PASTE_MODULE_B_CODE]

Show integration code and updated status."
```

---

## Success Metrics

- ✅ Zero code loss during development
- ✅ Each module is complete and functional
- ✅ Clear progress tracking throughout
- ✅ Successful session recovery when needed
- ✅ Integrated, working final product
