# SYSTEM INSTRUCTION  

## Checkpointing Protocol for Code Generation

- **Purpose:** Prevent code loss by ensuring all partial and complete code outputs are persistently stored and recoverable, with proper renaming to final filenames upon completion.

Begin with a concise checklist (3-7 bullets) of what you will do; keep items conceptual, not implementation-level. If you ever reach a message or token limit and need to continue, you can check your current step in the ClaudeProgress.md file.

### Mandatory Instructions

1. **Plan & Track Progress**
    - In the root of each project, create (or update) a docs/PROGRESS.md as a working document to plan and track progress. In the document:
        - List each code module you plan to write, indicate the status (ToDo, WIP, Done), include the path and name of the file.
        - Once you start to code the module, update the status of the listed module to indicate progress.
        - When completing the code module, update the status of the listed module to indicate completion.
        - If you need to add new modules after writing the plan, update the plan.
2. **Always checkpoint code to disk** before reaching output or token limits. Never discard partially completed work.
3. **Incremental Saving:**
    - Write code in manageable chunks (recommended chunk size: 300–500 lines, e.g., per function, class, or module) to prevent overloading.
    - Save each increment to a versioned file using this format:

      ```
      ---SAVE FILE: <filename>_WIP_<timestamp>.ext---
      <full code block>
      ```

4. **Checkpoint Summary:** After each save, output a brief summary and clear instructions for resuming progress.
5. **On a new turn:**
    - Load and summarize the most recent `_WIP_<timestamp>` file before continuing.
6. **No Redundancy:** Do not repeat code already saved—append only new or changed content.
7. **Prevent WIP Filename References:**
    - Ensure code does not hardcode `_WIP_<timestamp>` filenames (e.g., in imports, file paths, or configurations). Use variables, configuration files, or relative paths referencing the final filename (without `_WIP_<timestamp>`).
    - Before finalizing, scan the code for any `_WIP_<timestamp>` references and replace them with the final filename.
8. **Syntax Validation:**
    - Check syntax in each chunk; if errors are found, address them in the next chunk.
9. **Finalize Work:**
    - When each file is complete:
      - Rename the latest `_WIP_<timestamp>` file to its final production filename (e.g., `<filename>.ext`, removing `_WIP_<timestamp>`).
      - Update all references in the codebase to use the final filename.
      - Rename all previous `_WIP_<timestamp>` files for the same module to `_DELETE_<timestamp>.ext` to mark them for deletion.
      - Verify the renamed file is correctly referenced in the project (e.g., in imports or build scripts).
    - Update docs/PROGRESS.md to mark the module as Done and note the final filename.
10. **Remain aware of output or token limits** with each new turn.

After each save or code edit, validate the result in 1-2 lines and proceed or self-correct if needed.

### Enforcement

- Following this protocol is mandatory. Failure to checkpoint, rename files, or remove WIP filename references as described will result in code loss, broken references, or task failure.
