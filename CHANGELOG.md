# Changelog

User-facing changes to SynthPilot. Install or upgrade with
`uv tool install synthpilot --upgrade --refresh`. For pricing and editions see
[synthpilot.dev](https://synthpilot.dev).

## 1.4.0 — 2026-08-17

- **One product, three FPGA platforms.** Select AMD Vivado™, TangDynasty® (TD),
  or Intel® Quartus® Prime with `synthpilot setup --platform <name>`. Each MCP
  process registers only the selected platform and the tools allowed by the
  active Free, Pro, or Max license.
- **Public tool catalogs.** The showcase repository and website now publish
  registry-derived catalogs for [Vivado](tools/vivado.md),
  [TangDynasty](tools/anlogic.md), and [Quartus](tools/quartus.md), with purpose,
  category, plan, operation type, and coarse parameter summaries.
- **TangDynasty managed workflow.** Added bounded environment diagnostics,
  project/run entry, compilation, reports, and managed process cleanup. A
  representative Windows TD 6.2.1 project and bitstream workflow has passed;
  broader command/version matrices remain in validation.
- **Quartus managed workflow.** Added diagnostics, project open/create,
  read-only design/report queries, asynchronous build status/log/cancel,
  one-file source registration, fixed `TOP_LEVEL_ENTITY` configuration, and
  close/reopen persistence. The clean-session flow is verified on Windows Lite
  25.1; Standard, Pro, and Linux vendor-live matrices remain in validation.
- **Remote Vivado over SSH (Beta).** Added remote Linux profiles, bounded
  diagnostics, and MCP registration over OpenSSH stdio. Vivado stays on a
  loopback-only Tcl listener. The complete remote Linux + Vivado end-to-end
  live matrix remains under acceptance.
- **Windows and Linux release.** Version 1.4.0 is published as Windows x64 and
  `manylinux_2_17_x86_64` wheels. Both packages report the exact three-platform
  runtime manifest.
- **Unified workflow plugin.** SynthPilot can export its shared Codex/Claude
  workflow bundle for setup, Vivado, TangDynasty, and Quartus guidance.

See the [platform pages](https://synthpilot.dev/#platforms) for the precise live,
source-complete, Beta, and pending acceptance boundaries.

## 1.3.0 — 2026-06-09

- **One-command setup.** `synthpilot setup` detects Vivado, installs the Tcl server,
  activates your license, **registers SynthPilot in your AI editor without hand-editing
  JSON** (Claude Code / Claude Desktop / Cursor / Codex), and runs a health check.
  `synthpilot doctor` diagnoses problems; `synthpilot doctor --fix` self-heals.
- **A methodology layer for every client.** The 13
  [oh-my-fpga](https://github.com/LNC0831/oh-my-fpga) FPGA workflows now ship as built-in
  **MCP prompts**, so Cursor / Codex / Claude Desktop get the same "describe the outcome"
  experience Claude Code already gets from the skill plugin.
- **Windows install no longer needs admin rights** — the Tcl server falls back to a per-user
  `Vivado_init.tcl` when the install directory isn't writable, and auto-detect now scans all
  drives.
- New `synthpilot install-mcp` registers the server in your editor(s) on demand.
- Published for Windows **and** Linux.

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
