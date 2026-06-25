Contribution [2]: [React Doctor] rerender-functional-setstate: setModifiedLimit(modifiedLimit + (45 occurrences)
 #27954\
Contribution Number: 2
Student: Tish Griffiths  
Issue: [https://github.com/wso2/product-is/issues/27954](https://github.com/wso2/product-is/issues/27954)\
Status: Phase I In Progress
---
Why I Chose This Issue
[A 2–4 sentence problem summary explaining what the issue is, why it matters, and why you chose it in Why I Chose This Issue]
State updates are using the current value directly (e.g. setState(value + 1)) instead of the callback form (e.g. setState(prev => prev + 1)), which can cause bugs when the state value is stale at the time of the update. Fixing this issue will reduce warnings and improve performance. I chose this issue because I am experienced with react and state management and understand the issue. I hope to learn more about wso2 and their development environment.
---
Understanding the Issue
Problem Description
[In your own words, what's broken or missing?]
Expected Behavior
[What should happen?]
Current Behavior
[What actually happens?]
Affected Components
[Which parts of the codebase are involved?]
---
Reproduction Process
Environment Setup
[Notes on setting up your local development environment - challenges you faced, how you solved them]
Steps to Reproduce
[Step 1]
[Step 2]
[Observed result]
Reproduction Evidence
Commit showing reproduction: [Link to commit in your fork]
Screenshots/logs: [If applicable]
My findings: [What you discovered during reproduction]
---
Solution Approach
Analysis
[Your analysis of the root cause - what's causing the issue?]
Proposed Solution
[High-level description of your fix approach]
Implementation Plan
Using UMPIRE framework (adapted):
Understand: [Restate the problem]
Match: [What similar patterns/solutions exist in the codebase?]
Plan: [Step-by-step implementation plan]
[Modify file X to do Y]
[Add function Z]
[Update tests]
Implement: [Link to your branch/commits as you work]
Review: [Self-review checklist - does it follow the project's contribution guidelines?]
Evaluate: [How will you verify it works?]
---
Testing Strategy
Unit Tests
[ ] Test case 1: [Description]
[ ] Test case 2: [Description]
[ ] Test case 3: [Description]
Integration Tests
[ ] Integration scenario 1
[ ] Integration scenario 2
Manual Testing
[What you tested manually and results]
---
Implementation Notes
Week [X] Progress
[What you built this week, challenges faced, decisions made]
Week [Y] Progress
[Continue documenting as you work]
Code Changes
Files modified: [List]
Key commits: [Links to important commits]
Approach decisions: [Why you chose certain approaches]
---
Pull Request
PR Link: [GitHub PR URL when submitted]
PR Description: [Draft or final PR description - much of the content above can be adapted]
Maintainer Feedback:
[Date]: [Summary of feedback received]
[Date]: [How you addressed it]
Status: [Awaiting review / Iterating / Approved / Merged]
---
Learnings & Reflections
Technical Skills Gained
[What you learned technically]
Challenges Overcome
[What was hard and how you solved it]
What I'd Do Differently Next Time
[Reflection on your process]
---
Resources Used
[Link to helpful documentation]
[Tutorial or Stack Overflow post that helped]
[GitHub issues or discussions that helped]
