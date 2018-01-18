Code Review
======


Before you create PR
-----------------
Basics
-----------------
- Identify places which were over-engineered.
- Merge is done by the reviewer who approves the PR as the last one, except for a situation when deployment of the code in PR requires some additional configuration in target environment (setting env variables, migrations etc).
- Identify ways to simplify the code while still solving the problem.
- If discussions turn too philosophical or academic, move the discussion face to face or hipchat. The outcome of this discussion should be placed in the comment.
- Offer alternative implementations, but assume the author already considered them.
- What do you think about changing it one-line if-statement?
    - In our guidelines we us ‘ instead of “, is there any particular reason you used “ here?
    - Try to understand the author's perspective.
- Don’t be sarcastic
- You can mark you comment as optional using [opt]

When your code is reviewed:
-----------------
- Don't take it personally. It’s a review of the code, not you.
- Try to understand the reviewer's perspective
- Try to respond to every comment - this means that every comment from a reviewer should result in a response or a code change.

When you review someone’s code
-----------------
- Remember that you can ask for clarification.
- Avoid using terms that could be seen as referring to personal traits. [dumb, stupid]. Assume everyone is intelligent and well-meaning.
- Be explicit. Remember people don't always understand your intentions.
