# lib-math-js

JavaScript implementation of the `math` ports (via the `js` ffi —
`js.call("Math", ...)` / `js.call("Number", ...)`).

`src/index.hnl` implements every `math/<arrow>` contract signature:
transcendentals and `Math.*`-covered ops marshal through `js.call`
with `js_number`/`js_boolean` descriptors; the total arrows are pure
handl. `Math`-less ops are composed (`exp2` = `exp(x·ln2)`,
`fract`/`floor_div`/`round_to`/`copysign`/`degrees`/`radians`), looped
(`factorial`/`gcd`/`lcm`), or emulated with JS int32 semantics
(`bit_and`/`bit_or`/`bit_xor`/`bit_not`/`shl`/`shr`/`rotl32`/`u32` —
`Math` exposes no bitwise functions). `nextafter` raises via
`error.raise`: it needs bit-level double access `Math.*` cannot give.
`pi`/`e`/`tau` are literals, `nan` is `Math.sqrt(-1)`, `infinity` is
`Math.exp(1000)`.

Unlike `math-c`/`math-handl` this is a **single module** — import from
`"math-js"`; `math-js/<arrow>` submodule paths do not exist.

## Layout

```text
src/index.hnl  the .hnl sources (all 69 contract arrows)
pkg.hnl        package manifest — modules, deps, description, license
```

Dependencies: math, js

## Gate

```bash
HNL=../host-cli/target/debug/hnl scripts/hnl-gate.sh
```

CI skips the gate while `src/` has no `.hnl` sources.

## License

MIT.
