# lib-math-js

JavaScript implementation of the `math` ports (via the js ffi). This repo
is a **skeleton**: the layout and gate are in place, the implementation has
not landed yet.

## Layout

```text
src/        the .hnl sources (empty until the implementation lands)
pkg.hnl     package manifest — modules, deps, description, license
```

Dependencies: math

## Gate

```bash
HNL=../host-cli/target/debug/hnl scripts/hnl-gate.sh
```

CI skips the gate while `src/` has no `.hnl` sources.

## License

MIT.
