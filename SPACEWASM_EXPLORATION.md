# SpaceWASM Exploration Notes

Notes from looking into NASA's [spacewasm](https://github.com/nasa/spacewasm) project.

## What it is

SpaceWASM is a WebAssembly interpreter purpose-built for spacecraft flight
software, designed to run WASM binaries in resource-constrained flight
environments where general-purpose interpreters aren't practical.

It has two main pieces:

- **Decoder/Validator** — processes WASM binaries in streaming chunks rather
  than requiring a single contiguous block, keeping peak memory usage low.
  Produces an optimized intermediate representation in a single validation
  pass.
- **Interpreter** — executes the decoded IR, managing linear memory and
  interfacing with embedded host functions.

## Notable design choices

- **Deterministic memory management** — fixed-size memory pages, no
  mid-allocation deallocation, matching typical flight-software constraints.
- **Hard resource limits** — e.g. 256 modules max, 255-parameter functions
  max, configurable stack depths.
- **Minimal unsafe Rust** — unsafe code confined to custom allocation
  structures.
- **Test coverage** — unit tests, WASM spec-suite integration tests, and
  fuzzing infrastructure.

## Open questions

- No public documentation ties SpaceWASM directly to F Prime; this is
  exploratory only.
- Worth revisiting if/when there's a concrete use case for running dynamic,
  sandboxed code aboard an F Prime-based mission.
