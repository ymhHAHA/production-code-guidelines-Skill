---

name: production-code-guidelines

description: Production-oriented coding rules for LLMs. Use for real code to reduce overengineering, defensive bloat, silent fallbacks, patch-heavy fixes, and tutorial-style output. Not for throwaway scripts, prototypes, docs examples, or one-off code where speed matters more than maintainability.

license: MIT

---


# Production Code Guidelines


Use these rules when writing, editing, or reviewing code intended to run in a real system.


## 1. Scope first


Before coding, state:

- what you are changing

- why

- whether this is new code or a change to existing code


If the request is ambiguous, say what is unclear and ask.

If there is a simpler solution, say so.


## 2. Match the task


- **New code:** keep it direct, concrete, and minimal.

- **Existing code:** make the smallest change that solves the request and match local patterns.


Every changed line should trace directly to the request.


## 3. Do the minimum


- Do not add features that were not requested.

- Do not add abstractions, hooks, options, or configurability for a single concrete use.

- Do not add helper layers just to make the code look cleaner.

- Do not add code for hypothetical cases outside the task.


Before submitting, ask:

- Did I add code for cases not required by the task?

- Did I add an abstraction used only once?

- Did I add configurability with only one real use?

- Did I add a guard that belongs in another layer?


## 4. Defend only at trust boundaries


Validate untrusted inputs where they enter the system:

- user input

- external APIs

- cross-service data

- deserialized storage, queue, or cache data

- config or environment values not guaranteed by code


Inside trusted code:

- do not repeat upstream validation

- do not add speculative guards

- prefer failing fast over masking bad state


## 5. No silent fallbacks


- Do not catch errors and return defaults unless explicitly required.

- Do not add fallback branches, retries, or graceful degradation unless asked.

- Do not turn real errors into empty values, partial success, or silent no-ops.

- Prefer one clear failure over hidden recovery.


## 6. Fix causes, not symptoms


- Do not patch around unexplained behavior with one-off conditionals or conversions.

- Do not fix output shape to hide upstream bugs.

- Do not add compatibility branches without evidence they are needed.

- Fix the problem in the layer that owns it, not where the symptom appears.


Before submitting, ask:

- Did I fix the cause, or only hide the symptom?

- Is this patch required by a real case, or just uncertainty?


## 7. Be surgical


When editing existing code:

- do not refactor unrelated code

- do not rename, reformat, or reorganize unrelated code

- do not clean up pre-existing issues unless asked


Only remove things your change made unnecessary.


## 8. Write production code, not tutorial code


Do not add:

- example usage

- comments that restate the code

- tutorial-style explanations

- abstractions added mainly to narrate the implementation


Comments should explain only non-obvious intent, constraints, or tradeoffs.


## 9. Verify the result


Turn the task into something checkable.


- bug fix -> reproduce it, then make the reproduction pass

- validation -> add a failing invalid-input check, then make it pass

- refactor -> preserve behavior and verify before and after


Unless the task is purely advisory or execution is impossible:

- add the smallest test or check that proves the requested behavior

- prefer local tests over broad new scaffolding

- state what you verified

- state what remains unverified


## 10. When uncertain, prefer this order


1. Match local conventions.

2. Solve only the stated problem.

3. Keep the code direct and minimal.

4. Defend at trust boundaries, not everywhere.

5. Fix the responsible layer, not the visible symptom.

6. Fail fast rather than add silent fallback behavior.


## 11. Do not default to


- catch-and-return-default error handling

- fallback paths that were not requested

- speculative null checks in trusted code

- duplicated validation

- single-use abstractions or configurability

- one-off patch conditionals without evidence

- output-side fixes that hide upstream bugs

- tutorial comments or example usage

- unrelated refactors