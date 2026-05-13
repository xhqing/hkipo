# Tool Calling Rules V1

When calling tools, strictly follow the rules below. These rules take precedence over any conflicting habits from chat training.

---

## I. Pre-Call Preparation

1. **Read before calling.** Before invoking a tool, always read the tool's description and parameter documentation in full. Do not guess its behavior or parameter meanings based on the tool name alone.

2. **Never fabricate parameter values.** For parameter values you are unsure about (e.g., file paths, IDs, enum values), do not make them up. First obtain the actual values through search, listing, or query tools, then make the call.

3. **Confirm required vs. optional.** Carefully distinguish between required and optional parameters. Missing a required parameter will cause the call to fail; missing an optional parameter typically results in the system using a default value—no need to pass an explicit placeholder.

---

## II. Parameter Format

4. **Omit unneeded optional fields.** Do not send `null`, `""`, `{}`, or `[]` as placeholders. If a field is optional and you have no value for it, simply omit the field from the JSON.

   ```json
   // Correct: omit unneeded optional fields
   {"required_field": "value"}

   // Incorrect: using null as a placeholder
   {"required_field": "value", "optional_field": null}
   ```

5. **Strictly match container types.**
   - Array fields must use JSON arrays: `["a", "b"]`, never `"[\"a\",\"b\"]"` (string form), `{}` (object), or `"foo"` (bare string).
   - Single-element arrays still require brackets: `["foo"]`, not `"foo"`.
   - Object fields must use JSON objects, not arrays or strings.

6. **Strings are raw strings.** Do not add extra quotes, code fences, or Markdown formatting around values.

7. **Numbers and booleans must not be quoted.** Use `30` not `"30"`, and `true` not `"true"`.

8. **Enum values must match exactly.** When the parameter description lists allowed enum values, you must use one of them with matching case and spelling. Do not invent your own enum values.

---

## III. Paths and Identifiers

9. **Paths, URLs, IDs, and similar fields should be used as raw input to system functions.** Never format them as Markdown links, wrap them in backticks, or add explanatory parentheses.

   | Correct | Incorrect |
   |---------|-----------|
   | `"/Users/me/notes.md"` | `` `/Users/me/notes.md` `` |
   | `"/Users/me/notes.md"` | `"(http://notes.md)"` |
   | `"/Users/me/notes.md"` | `"/Users/me/notes.md" (notes file)` |

10. **"Path" means a filesystem path.** If the tool description says "path," treat it as input for a filesystem call—no formatting or decoration.

11. **Use absolute paths.** Unless the tool description explicitly allows relative paths, always use absolute paths to avoid resolution errors caused by differing working directories.

---

## IV. Related Parameters

12. **Paired parameters must be provided together.** When a tool has paired parameters (e.g., `offset` + `limit`, `start` + `end`, `from` + `to`, `pattern` + `path`), either provide both or neither. Providing only one often leads to errors or unexpected behavior.

13. **Be aware of inter-parameter dependencies.** Some parameters only take effect when another parameter has a specific value. Read parameter descriptions to understand conditional dependencies and avoid passing invalid combinations.

---

## V. Tool Selection and Calling Strategy

14. **Prefer the most specific tool.** Use the tool whose description most specifically matches your intent. If a dedicated tool exists, do not fall back to a generic one (e.g., `shellCommand`, `execute_code`).

15. **Independent calls can be parallelized.** When multiple tool calls have no data dependencies on each other, issue all calls in parallel within the same message to reduce round trips and improve efficiency.

16. **Dependent calls must be sequential.** When a subsequent call depends on the return value of a previous call, you must wait for the previous call to complete before making the next one. Do not guess return values.

---

## VI. Error Recovery

17. **Precisely fix validation errors.** If a tool returns a validation error, carefully read the error message and fix only the issue it identifies. Do not rewrite the entire call, and do not retry with the same parameters.

18. **Distinguish informational notices from errors.** If a tool returns a "Note:" message with a default value, that is an informational notice, not an error. Continue with the task. Only re-invoke with an explicit value if the default does not meet your needs.

19. **Stop retrying on permission or not-found errors.** If a tool returns errors such as insufficient permissions, file not found, or resource not found, do not blindly retry the same call. First verify that the path or permissions are correct, and use query tools to confirm when necessary.

---

## VII. Safety and Side Effects

20. **Exercise caution with destructive operations.** For irreversible operations such as deletion, overwriting, or renaming, confirm that the target actually exists and the operation intent is clear before executing. Do not perform destructive operations on uncertain targets.

21. **Avoid redundant modifications.** If the current state already meets the requirements, do not make unnecessary write or update calls. Read first, then decide—avoid meaningless overwrites.

22. **Respect idempotency.** For naturally idempotent operations (e.g., setting a configuration item to a specific value), repeated calls produce no side effects and can be safely executed. For non-idempotent operations (e.g., appending data, incrementing a counter), ensure that repeated calls will not cause data duplication or state errors.
