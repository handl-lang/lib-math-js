# lib-math-js

JavaScript implementation of the `math` ports via the `js` ffi
(`js.call("Math", ...)` / `js.call("Number", ...)`). Pure `.hnl`,
single module.

## Layout

| path | role |
| --- | --- |
| `src/index.hnl` | all 69 contract arrows in one module |
| `pkg.hnl` | manifest — `modules: ["math-js"]`, deps `math` + `js` |
| `scripts/hnl-gate.sh`, `workflows/gate.yaml` | the gate / bupha entry |

## Contract

- Unlike `math-c`/`math-handl`, this is a **single module** — import
  from `"math-js"`; `math-js/<arrow>` submodule paths do not exist.
- `Math.*`-covered ops marshal through `js.call` with
  `js_number`/`js_boolean` descriptors; total arrows are pure handl.
- `Math`-less ops are composed (`exp2` = `exp(x·ln2)`), looped
  (`factorial`/`gcd`/`lcm`), or emulated with JS int32 semantics
  (`bit_and`/`bit_or`/`bit_xor`/`bit_not`/`shl`/`shr`/`rotl32`/`u32`).
- `nextafter` raises via `error.raise` — it needs bit-level double
  access `Math.*` cannot give. `pi`/`e`/`tau` are literals, `nan` is
  `Math.sqrt(-1)`, `infinity` is `Math.exp(1000)`.

## Verification

```bash
HNL=../host-cli/target/debug/hnl scripts/hnl-gate.sh
```

## License

MIT.

<!-- myco:agent-awareness -->

## Agent awareness

- Session start / any work discussion: run `myco status --prompt`
  before proposing next steps — know the board first.
- User describes new work → offer to capture it (`myco todo add`,
  `issue new`, `proposal new`). Don't wait to be asked.
- Picking up a task: `myco resume <ID>` is the briefing.
- Wrapping up: `myco handoff <ID>` anything resumable; keep statuses
  honest (claimed → in-progress → blocked/done).

<!-- /myco:agent-awareness -->
