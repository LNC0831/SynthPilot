# Changelog

User-facing changes to SynthPilot. Install or upgrade with `pip install -U synthpilot`
(or `uvx synthpilot@latest`). For pricing and editions see [synthpilot.dev](https://synthpilot.dev).

## 1.2.5 — 2026-06-05

- **More reliable Vivado connection under load.** Commands are now serialized, so a
  long-running synthesis no longer collides with concurrent calls and drops the link.
- **Recover stuck simulations.** New `sim_stop` tool terminates a hung xsim kernel and
  clears the locked snapshot; `sim_compile` now reports a clear, actionable message when a
  previous simulation is still holding the snapshot (instead of an opaque error).
- **Fixed** a false "simulation completed" status when a testbench's own output mentioned
  `$finish`.

## 1.2.4

- Windows compatibility and connection-stability fixes.

## 1.2.0 – 1.2.3

- **Linux support.** Native Linux runtime plus a manylinux wheel — SynthPilot now runs on
  Windows **and** Linux.
- **Simulation code coverage.** `sim_compile` can instrument statement / branch / condition
  / toggle coverage; retrieve structured results with `sim_get_coverage`.
- More robust coverage-report parsing (header-based, not fixed-column).
- Install fix so the binary reliably lands on `PATH`.

## 1.1.x

- **Multi-Vivado support** — auto port allocation and switching between several open Vivado
  instances.
- **Embedded / Vitis automation** — `emb_*` tools driving XSCT for bare-metal builds, JTAG,
  and on-chip debug.
- **Redesigned ILA trigger tools** — radix-aware values, don't-care bits, multi-probe
  AND/OR trigger conditions, and trigger reset.
- **VHDL & mixed-language simulation** — `sim_compile` now drives `xvhdl` alongside `xvlog`.
- **More BD / flow tools** — AXI VIP, JTAG-to-AXI + `hw_axi` runtime access, and
  non-project-mode (checkpoint) flow tools.
- **Verilog define management** (get / set / add).
- Generate-block signal probing in `sim_probe` / `sim_list_signals`.
- VIO / ILA property and probe-type compatibility fixes across Vivado versions.
- Serial-port tools (listing, busy detection, cleanup).
- Default synthesis mode set to out-of-context for IP and Block Design output generation.

## 1.0.0

- First public release on PyPI as **SynthPilot**, distributed via `pip` / `uvx`.
- 500+ tools covering the full FPGA flow: project management, RTL lint & syntax check,
  synthesis / implementation, timing & utilization reports, IP and Block Design
  configuration, xsim-based simulation with waveform probing, and hardware programming.
- `synthpilot install / uninstall / activate` CLI.
