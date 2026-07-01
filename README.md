# Contribution 2: [React Doctor] rerender-functional-setstate: setModifiedLimit(modifiedLimit + (45 occurrences) #27954

**Contribution Number:** 2\
**Student:** Tish Griffiths  
**Issue:** [https://github.com/wso2/product-is/issues/27954](https://github.com/wso2/product-is/issues/27954)\
**Status:** Phase I In Progress

---

## Why I Chose This Issue

State updates are using the current value directly (e.g. setState(value + 1)) instead of the callback form (e.g. setState(prev => prev + 1)), which can cause bugs when the state value is stale at the time of the update. Fixing this issue will reduce warnings and improve performance. I chose this issue because I am experienced with react and state management and understand the issue. I hope to learn more about wso2 and their development environment.

---

## Understanding the Issue

### Problem Description

Several React components in identity-apps update state by reading the current state value directly (ex. setModifiedLimit(modifiedLimit + n)) instead of using the functional updater form (ex. setModifiedLimit(prev => prev + n)). If a re-render or batched update happens before the setter runs, the value used may be outdated, causing incorrect or dropped updates and triggering the lint warning 45 times across the codebase.

### Expected Behavior

State updates should always use the functional updater form when the new value depends on the previous value, so the setter always computes from the latest state rather than a value captured in a stale closure.

### Current Behavior

The setter reads the state variable directly from the surrounding closure at the time the function was defined. 

### Affected Components

45 occurrences across unrelated identity-apps modules, including:

- admin.applications.v1/components/wizard/application-create-wizard.tsx
- admin.roles.v2/components/edit-role/edit-role-permission.tsx
- admin.users.v1/components/wizard/add-user-wizard.tsx
- admin.branding.v1/providers/branding-preference-provider.tsx
- admin.connections.v1/components/wizards/authenticator-create-wizard.tsx

(Full list of 45 files/lines is in issue #27954.)

---

## Reproduction Process

### Environment Setup

- **Repository confusion:** Issue is filed on `product-is`, but a note in the issue body points to `identity-apps` at commit `b2a8f16f...` - that's the actual repository to fix.
- Forked `wso2/identity-apps`.
- Upgraded Node.js and installed `pnpm` (required package manager for this repo).
- **JDK 11:** SDKMAN blocked Java 11 installs. Switched to Eclipse Adoptium (Temurin) since it doesn't require an account or sign-in like Oracle's installer. Had to Comment out version rules in `.bashrc` so `JAVA_HOME` would point to Java 11 without being overridden.
- Installed recommended VS Code extensions (`NX Console`, `ESLint`, `Code Spell Checker`, `json-sorter`) and re-enabled the React and Redux DevTools browser extensions.
- Built a local WSO2 IS server from `product-is` source per `CONTRIBUTING.md`. Used `v7.0.0` specifically since newer versions require a JDK version incompatible with Java 11.
- Created branch `fix-issue-27954` on my `identity-apps` fork.

### Steps to Reproduce

1. Fork and clone `wso2/identity-apps`.
2. Install Node.js, `pnpm`, and JDK 11 (Adoptium build — avoid SDKMAN).
3. Build and run a local WSO2 IS server using `product-is` `v7.0.0`, following its `CONTRIBUTING.md`.
4. Open a sample of the 45 flagged files, for example:
   - `admin.applications.v1/components/wizard/application-create-wizard.tsx:192`
   - `admin.roles.v2/components/edit-role/edit-role-permission.tsx:268`
   - `admin.users.v1/components/wizard/add-user-wizard.tsx:228`
   - `admin.branding.v1/providers/branding-preference-provider.tsx:432`
5. Confirm each location calls a state setter using the current state value directly (ex.  `setModifiedLimit(modifiedLimit + n)`) instead of the functional form (`setModifiedLimit(prev => prev + n)`). 
6. Run the `react-doctor/rerender-functional-setstate` lint rule against these files and confirm a warning fires at each line.
7. Repeat steps 5–7 across all 45 files and record which still trigger the warning as of current master.

### Reproduction Evidence

- **Commit showing reproduction:** [Link to commit in your fork]
- **Screenshots/logs:** [If applicable]
- **My findings:** [What you discovered during reproduction]

---

## Solution Approach

### Analysis

Files span multiple unrelated modules, all with the same pattern - a plain useState setter feeds the current state value plus/minus an amount, instead of the updater callback form.

Examples:
- admin.applications.v1/components/wizard/application-create-wizard.tsx
- admin.roles.v2/components/edit-role/edit-role-permission.tsx
- admin.users.v1/components/wizard/add-user-wizard.tsx
- admin.branding.v1/providers/branding-preference-provider.tsx
- admin.connections.v1/components/wizards/authenticator-create-wizard.tsx

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** 45 setState calls use a stale closure value instead of the functional updater form. Root cause: the setter reads state from the render closure, not the latest value. This is risky in async callbacks or batched updates. an cause dropped or incorrect updates.

**Match:** Check for existing functional-updater usage elsewhere in identity-apps to match the project's style, and check if a shared hook/util already wraps this pattern.

**Plan:** 
1. Checklist all 45 files/lines from the issue.
2. Convert each setter call to functional form.
3. Where the update depends on other variables, pass them into the updater or move logic inside it.
4. Re-run the lint rule to confirm all 45 warnings clear.
5. Update/add unit tests for touched components.
6. Manually verify no UI regressions 
7. Group commits by module (page, component) for reviewability.
8. Open PR referencing #27954.

**Implement:** [https://github.com/TishG/identity-apps/tree/fix-issue-27954](https://github.com/TishG/identity-apps/tree/fix-issue-27954)

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** Confirm all 45 warnings are resolved (no longer exist), all current and new unit tests pass, no UI regressions

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
