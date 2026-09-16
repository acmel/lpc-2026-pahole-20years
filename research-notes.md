<!-- SPDX-License-Identifier: GPL-2.0-only -->
# Research notes: 20 years of pahole (LPC 2026 refereed)

Companion to `index.html`. History anchors are pahole commits
(`~/git/pahole`); ecosystem facts checked Sep 2026.

## History anchors (all verified in git)

- `038d8068` Oct 24 2006 — repository creation.
- `9d21d3d7` Dec 7 2006 — DW_TAG_inheritance ("languages such as
  C++", Qt QSettingsPrivate example). CERN 32-to-64-bit part is
  personal recollection, not in the message.
- `94861979` May 31 2007 — namespace helper.
- `4ab5153b` Apr 20 2008 — DW_TAG_class_type.
- `2dfa5fe6` Mar 4 2008 — initial CTF support, "library written by
  David S. Miller". Request part is recollection.
- `3221454a` Aug 2009 / `525c2644` Nov 2010 — C++ template params.
- Santa Fe 2015 (Borkmann/Starovoitov discussion): recollection.
- `68645f7f` Mar 5 2018 — Martin KaFai Lau <kafai@fb.com>, "btf: Add
  BTF support" (first use: BPF map pretty print).
- `33e0d5f8` Jun 2021 — `--prettify` (`--header elf64_hdr` example in
  message). perf.data test: `tests/prettify_perf.data.sh`.
- `fullcircle` script in tree: pfunct --compile, recompile with
  DW_AT_producer CFLAGS, `codiff -q -s`.
- `685627ca` Jun 2026 / `d3dab113` Jul 2026 — llvm-cov workflow
  (`coverage/coverage.sh`, `scripts/coverage_table.py`,
  `coverage/coverage-diff.sh`).
- Stats on master: 2482 commits, 83 authors; newcomers every year
  (5 in 2006, 10 in 2026); 95 test commits since Jan 2025; 78 scripts
  in tests/. Checkout usually sits on a topic branch: take stats on
  master.
- Coverage Sep 2026 (container run, perf tests skipped, 74 Ok):
  dwarf_loader 75.8%, pahole.c 67.3%, TOTAL 66.6% lines / 76.8%
  funcs. Re-run `make coverage` on a full machine for better numbers.
  Test 60 FAILED in container (no memory events) — environmental.

## Ecosystem (talk: "Ecosystem, not alone" slide)

- libabigail (Dodji Seketeli, Red Hat): `abidiff` = full ABI-compat
  checker; pahole `codiff` = lighter dump diff.
  https://sourceware.org/libabigail/
- GDB `ptype /o` (offsets, GDB 8.1, 2017). No `pahole` command
  upstream — only out-of-tree scripts.
- dwgrep: Petr Machata (not Wolff). Maintenance mode since 2024.
  https://github.com/pmachata/dwgrep
- Valgrind DHAT: per-site heap + per-byte access histograms ≈
  hot/cold members. https://valgrind.org/docs/manual/dh-manual.html
- Compilers emit BTF: GCC `-gbtf` (12+, BPF default), LLVM `-gbtf`
  (2025) + lld `--btf-merge`. pahole still dedups/repairs; kernel
  build still uses it (min v1.22).
- Pipeline: debugedit / dwz (0.17 Jul 2026) / dwp / debuginfod.

## Traps: do NOT say on stage

- No `pahole` command in upstream GDB.
- dwgrep author is Machata.
