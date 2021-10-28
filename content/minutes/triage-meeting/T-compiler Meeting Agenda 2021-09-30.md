---
tags: weekly, rustc
type: docs
---

# T-compiler Meeting Agenda 2021-09-30

[Tracking Issue](https://github.com/rust-lang/rust/issues/54818)

## Announcements

- New MCPs (take a look, see if you like them!)
  - "Make `-Z binary-dep-depinfo` the default behavior" [compiler-team#464](https://github.com/rust-lang/compiler-team/issues/464)
- Old MCPs (not seconded, take a look)
  - "rustdoc is using rustc_ast_pretty, would it be possible to make it somewhat "stable"?" [compiler-team#403](https://github.com/rust-lang/compiler-team/issues/403) (last review activity: GH none, Zulip: +2months ago)
  - "CI should exercise (subset of) tests under --stage 1" [compiler-team#439](https://github.com/rust-lang/compiler-team/issues/439) (last review activity: GH none, Zulip: about 1 month ago)
  - "Accept `pc` in place of `unknown` and `unknown` in place of `pc` for `x86_64` and `i?86` targets" [compiler-team#441](https://github.com/rust-lang/compiler-team/issues/441) (last review activity: GH none, Zulip: about 1 week ago)
  - "prefer-dynamic=subset" [compiler-team#455](https://github.com/rust-lang/compiler-team/issues/455) (last review activity: GH none, Zulip: about 15 days ago)
  - "Tier 3 target proposal: x86_64-unknown-none (freestanding/bare-metal x86-64)" [compiler-team#462](https://github.com/rust-lang/compiler-team/issues/462) (last review activity: GH: 10 days ago, Zulip: about 4 days ago)
- Pending FCP requests (check your boxes!)
  - "Write text output files to stdout if options like `-o -` or `--emit asm=-` are provided" [compiler-team#431](https://github.com/rust-lang/compiler-team/issues/431)
- Things in FCP (make sure you're good with it)
  - No FCP requests this time.
- Accepted MCPs
  - "Add `pie` relocation-model" [compiler-team#461](https://github.com/rust-lang/compiler-team/issues/461)
- Finalized FCPs (disposition merge)
  - "Make *const (), *mut () okay for FFI" [rust#84267](https://github.com/rust-lang/rust/pull/84267)
  - "Make `#[derive(A, B, ...)]` cfg-eval its input only for `A, B, ...` and stabilize `feature(macro_attributes_in_derive_output)`" [rust#87220](https://github.com/rust-lang/rust/pull/87220)

### WG checkins

@_WG-self-profile_ by @**mw** and @**Wesley Wiser** ([previous checkin](https://hackmd.io/VNIxtjGBT8Owfkb92Vzt6w#WG-checkins)):

> @rylev and @mw have been working towards recording non-timestamp data like the sizes of files that the compiler emits – e.g. object files and incr. comp. on-disk data as part of the self-profile infrastructure. This hasn't quite landed yet, but significant progress has been made.

> We've also introduced new apis that allow reading older versions of the on-disk data which will help perf.rlo work more smoothly as new versions are released.

## Backport nominations

[T-compiler stable](https://github.com/rust-lang/rust/issues?q=is%3Aall+label%3Abeta-nominated+-label%3Abeta-accepted+label%3AT-compiler) / [T-compiler beta](https://github.com/rust-lang/rust/issues?q=is%3Aall+label%3Astable-nominated+-label%3Astable-accepted+label%3AT-compiler)

- :beta: "Disable the evaluation cache when in intercrate mode" [rust#88994](https://github.com/rust-lang/rust/pull/88994)
  - beta nominated by @**simulacrum** [to fix #88869](https://github.com/rust-lang/rust/pull/88994#issuecomment-921740736), a beta regression
  - @**Mara** comments this causes the regression [rust#89119](https://github.com/rust-lang/rust/pull/88994#issuecomment-923091128) now fixed by [rust#89125](https://github.com/rust-lang/rust/pull/89125)
  - seems to be perf neutral
  - should also #89125 be beta-backport nominated?
- :beta: "Don't use projection cache or candidate cache in intercrate mode" [rust#89125](https://github.com/rust-lang/rust/pull/89125)
  - opened by @**Aaron1011**
  - fixes [rust#88969](https://github.com/rust-lang/rust/issues/88969) a regression from stable to beta
- :beta: "2229: Mark insignificant dtor in stdlib" [rust#89144](https://github.com/rust-lang/rust/pull/89144)
  - seems to be perf neutral
  - nominated by @**simulacrum** to [have it for RFC2229](https://github.com/rust-lang/rust/pull/89144#issuecomment-925989791)
- :beta: "[rfc 2229] Drop fully captured upvars in the same order as the regular drop code" [rust#89208](https://github.com/rust-lang/rust/pull/89208)
  - Opened by @**Wesley Wiser**
  - We need this for Rust 2021
- :beta: "Don't normalize opaque types with escaping late-bound regions" [rust#89285](https://github.com/rust-lang/rust/pull/89285)
  - Opened by @**Jack Huey**
  - Fixes a P-medium [rust#88862](https://github.com/rust-lang/rust/issues/88862) causing a cargo build hang
- No stable nominations for `T-compiler` this time.

[T-rustdoc stable](https://github.com/rust-lang/rust/issues?q=is%3Aall+label%3Abeta-nominated+-label%3Abeta-accepted+label%3AT-rustdoc) / [T-rustdoc beta](https://github.com/rust-lang/rust/issues?q=is%3Aall+label%3Astable-nominated+-label%3Astable-accepted+label%3AT-rustdoc)

- :beta: "Use the correct edition for syntax highlighting doctests" [rust#89277](https://github.com/rust-lang/rust/pull/89277)
  - nominated by @**simulacrum** as needed for 2021 edition
  - T-rustdoc (cc @**GuillaumeGomez**) is fine with the backport
- No stable nominations for `T-rustdoc` this time.

:back: / :shrug: / :hand:

## PRs S-waiting-on-team

[T-compiler](https://github.com/rust-lang/rust/pulls?utf8=%E2%9C%93&q=is%3Aopen+label%3AS-waiting-on-team+label%3AT-compiler)

- "On macOS, make strip="symbols" not pass any options to strip" [rust#88137](https://github.com/rust-lang/rust/pull/88137)
  - @**Wesley Wiser** has a note about asking if Alex has any insight into macOS

## Oldest PRs waiting for review

[T-compiler](https://github.com/rust-lang/rust/pulls?q=is%3Apr+is%3Aopen+sort%3Aupdated-asc+label%3AS-waiting-on-review+draft%3Afalse+label%3AT-compiler)

- "Replace dominators algorithm with simple Lengauer-Tarjan" [rust#85013](https://github.com/rust-lang/rust/pull/85013) (last review activity: 4 months ago)
- "Account for incorrect `impl Foo<const N: ty> {}` syntax" [rust#85346](https://github.com/rust-lang/rust/pull/85346) (last review activity: 3 months ago)
- "Diagnostic tweaks" [rust#85102](https://github.com/rust-lang/rust/pull/85102) (last review activity: 3 months ago)
- "might_permit_raw_init: also check arrays (take two)" [rust#87041](https://github.com/rust-lang/rust/pull/87041) (last review activity: 2 months ago)
- "When recovering from a `:` in a pattern, use adequate AST pattern" [rust#87160](https://github.com/rust-lang/rust/pull/87160) (last review activity: 2 months ago)

## Issues of Note

### Short Summary

- [0 T-compiler P-critical issues](https://github.com/rust-lang/rust/issues?q=is%3Aopen+label%3AT-compiler+label%3AP-critical)
  - [0 of those are unassigned](https://github.com/rust-lang/rust/issues?q=is%3Aopen+label%3AT-compiler+label%3AP-critical+no%3Aassignee)
- [80 T-compiler P-high issues](https://github.com/rust-lang/rust/issues?q=is%3Aopen+label%3AT-compiler+label%3AP-high)
  - [54 of those are unassigned](https://github.com/rust-lang/rust/issues?q=is%3Aopen+label%3AT-compiler+label%3AP-high+no%3Aassignee)
- [1 P-critical, 5 P-high, 3 P-medium, 0 P-low regression-from-stable-to-beta](https://github.com/rust-lang/rust/labels/regression-from-stable-to-beta)
- [0 P-critical, 0 P-high, 1 P-medium, 1 P-low regression-from-stable-to-nightly](https://github.com/rust-lang/rust/labels/regression-from-stable-to-nightly)
- [0 P-critical, 46 P-high, 83 P-medium, 11 P-low regression-from-stable-to-stable](https://github.com/rust-lang/rust/labels/regression-from-stable-to-stable)

### P-critical

[T-compiler](https://github.com/rust-lang/rust/issues?utf8=%E2%9C%93&q=is%3Aopen+label%3AP-critical+label%3AT-compiler)

- No `P-critical` issues for `T-compiler` this time.

[T-rustdoc](https://github.com/rust-lang/rust/issues?utf8=%E2%9C%93&q=is%3Aopen+label%3AP-critical+label%3AT-rustdoc)

- No `P-critical` issues for `T-rustdoc` this time.

### P-high regressions

[P-high beta regressions](https://github.com/rust-lang/rust/issues?q=is%3Aopen+label%3Aregression-from-stable-to-beta+label%3AP-high+-label%3AT-infra+-label%3AT-libs+-label%3AT-release+-label%3AT-rustdoc+-label%3AT-core)

- "no errors encountered even though `delay_span_bug` issued" [rust#87757](https://github.com/rust-lang/rust/issues/87757)
  - Should be fixed by beta-backport of [rust#88996](https://github.com/rust-lang/rust/pull/88996)
- "regression: cycle in MIR opts" [rust#88972](https://github.com/rust-lang/rust/issues/88972)
  - Should be fixed by [rust#88979](https://github.com/rust-lang/rust/pull/88979) (beta-accepted)
- "Trait upcasting shadows (trait object) deref coercion" [rust#89190](https://github.com/rust-lang/rust/issues/89190)
  - Currently unassigned
  - There a [Zulip topic](https://rust-lang.zulipchat.com/#narrow/stream/144729-wg-traits/topic/Dyn.20upcasting.20vs.20deref.20coercion), involves also `T-lang`

[Unassigned P-high nightly regressions](https://github.com/rust-lang/rust/issues?q=is%3Aopen+label%3Aregression-from-stable-to-nightly+label%3AP-high+no%3Aassignee+-label%3AT-infra+-label%3AT-release+-label%3AT-rustdoc+-label%3AT-core)

- No unassigned `P-high` nightly regressions this time.

## Performance logs

> [triage logs for 2021-09-28](https://github.com/rust-lang/rustc-perf/blob/master/triage/2021-09-28.md)

The largest story for the week are the massive improvements that come from enabling the new pass manager in LLVM which leads to consistent 5% to 30% improvements across almost all test cases. The regressions were mostly minor with clear paths for addressing the ones that were not made with some specific trade off in mind.

Triage done by **@rylev**. Revision range: [7743c9fadd64886d537966ba224b9c20e6014a59..83f147b3baf21acfc367a6da1045d212cd3957e4](https://perf.rust-lang.org/?start=7743c9fadd64886d537966ba224b9c20e6014a59&end=83f147b3baf21acfc367a6da1045d212cd3957e4&absolute=false&stat=instructions%3Au)

4 Regressions, 4 Improvements, 3 Mixed; 0 of them in rollups
43 comparisons made in total

#### Regressions

Revise never type fallback algorithm [#88804](https://github.com/rust-lang/rust/issues/88804)

- Large regression in [instruction counts](https://perf.rust-lang.org/compare.html?start=2b862bed9889808b69629fd7246317189b9517a5&end=900cf5e8905ba8a2a9c99a1dfc9cb2cf4754d77a&stat=instructions:u) (up to 2.7% on `full` builds of `keccak`)

Introduce `Rvalue::ShallowInitBox` [#89030](https://github.com/rust-lang/rust/issues/89030)

- Moderate regression in [instruction counts](https://perf.rust-lang.org/compare.html?start=218a96cae06ed1a47549a81c09c3655fbcae1363&end=e9f29a851917a706c01b6f51331894df1d15770b&stat=instructions:u) (up to 1.9% on `incr-patched: println` builds of `syn`)
- Perf regression is happening in real-world optimized builds which we would expect if we're making LLVM do more work.
- The author has an idea for how to reduce the pressure on LLVM and perhaps win back some of the perf, but was unsure if the regression was large enough to warrant that investigation.
- Left a comment asking the author to think about prioritizing that [investigation](https://github.com/rust-lang/rust/pull/89030#issuecomment-929187148).

Fix spacing of links in inline code. [#88343](https://github.com/rust-lang/rust/issues/88343)

- Large regression in [instruction counts](https://perf.rust-lang.org/compare.html?start=9620f3a84b079decfdc2e557be007580b097fe43&end=addb4da686a97da46159f0123cb6cdc2ce3d7fdb&stat=instructions:u) (up to 2.1% on `incr-unchanged` builds of `webrender-wrench`)
- This change is only in doc comments for the standard library so large regressions are quite surprising.
- This has impacted the incr-unchanged scenario of only one benchmark. Perhaps the docs led to a change in how incremental cache was being stored which could have an impact?

Suggest both of immutable and mutable trait implementations [#89263](https://github.com/rust-lang/rust/issues/89263)

- Moderate regression in [instruction counts](https://perf.rust-lang.org/compare.html?start=583437a6dd58ee266839d2dac940642a0752a6dd&end=3e8f32e1c52ca493c862facb7a69e7c3f1f97a18&stat=instructions:u) (up to 2.0% on `full` builds of `diesel`)
- The regression occurs in `evaluate_obligation` which seems like it would be effected by this change, but the only impacted benchmark is diesel doc which doesn't trigger this diagnostic
- The change is large enough though that it being noise would be quite surprising.
- Left a [comment](https://github.com/rust-lang/rust/pull/89263#issuecomment-929511988)

#### Improvements

- Migrate in-tree crates to 2021 [#89103](https://github.com/rust-lang/rust/issues/89103)
- Disable visible path calculation for PrettyPrinter in Ok path of compiler [#89120](https://github.com/rust-lang/rust/issues/89120)
- Make `Duration` respect `width` when formatting using `Debug` [#88999](https://github.com/rust-lang/rust/issues/88999)
- Enable new pass manager with LLVM 13 [#88243](https://github.com/rust-lang/rust/issues/88243)

#### Mixed

Use ZST for fmt unsafety [#89139](https://github.com/rust-lang/rust/issues/89139)

- Moderate improvement in [instruction counts](https://perf.rust-lang.org/compare.html?start=30278d3cf92b581550933546370443a5d5700002&end=67365d64bcdfeae1334bf2ff49587c27d1c973f0&stat=instructions:u) (up to -1.6% on `full` builds of `cranelift-codegen`)
- Moderate regression in [instruction counts](https://perf.rust-lang.org/compare.html?start=30278d3cf92b581550933546370443a5d5700002&end=67365d64bcdfeae1334bf2ff49587c27d1c973f0&stat=instructions:u) (up to 0.5% on `full` builds of `deeply-nested-async`)
- The regressions were already triaged [here](https://github.com/rust-lang/rust/pull/89139#issuecomment-927914624).

Support `#[track_caller]` on closures and generators [#87064](https://github.com/rust-lang/rust/issues/87064)

- Large improvement in [instruction counts](https://perf.rust-lang.org/compare.html?start=15d9ba0133ce0b35348e1c8367afe00aec841ffa&end=0132f8258ae0fbc4f2b461b28d510222d22aa979&stat=instructions:u) (up to -1.8% on `incr-unchanged` builds of `webrender-wrench`)
- Small regression in [instruction counts](https://perf.rust-lang.org/compare.html?start=15d9ba0133ce0b35348e1c8367afe00aec841ffa&end=0132f8258ae0fbc4f2b461b28d510222d22aa979&stat=instructions:u) (up to 0.5% on `incr-unchanged` builds of `helloworld`)
- The large majority of performance regressions were quite small and many were historically noisy benchmarks.
- Looking at the non-noisy benchmarks nothing seemed to stand out as a clear culprit. -
- There were some test cases that indicated large jumps in incr_comp_persist_dep_graph but this did not hold true across all incremental test cases, and nothing in the changes seemed to jump out at me as potentially causing this issue.
- Added a [comment](https://github.com/rust-lang/rust/pull/87064#issuecomment-929428658) in the PR asking for additional opinions.

Don't normalize opaque types with escaping late-bound regions [#89285](https://github.com/rust-lang/rust/issues/89285)

- Very large improvement in [instruction counts](https://perf.rust-lang.org/compare.html?start=3e8f32e1c52ca493c862facb7a69e7c3f1f97a18&end=2b6ed3b675475abc01ce7e68bb75b457f0c85684&stat=instructions:u) (up to -86.7% on `full` builds of `issue-88862`)
- Moderate regression in [instruction counts](https://perf.rust-lang.org/compare.html?start=3e8f32e1c52ca493c862facb7a69e7c3f1f97a18&end=2b6ed3b675475abc01ce7e68bb75b457f0c85684&stat=instructions:u) (up to 1.3% on `full` builds of `deeply-nested-async`)
- This has already been [triaged](https://github.com/rust-lang/rust/pull/89285#issuecomment-927417324).
- Essentially it's a targeted fix for a severe perf regression that can happen in limited circumstances. The fix will be backported to the latest beta.

#### Untriaged Pull Requests

- [#89263 Suggest both of immutable and mutable trait implementations](https://github.com/rust-lang/rust/pull/89263)
- [#89125 Don't use projection cache or candidate cache in intercrate mode](https://github.com/rust-lang/rust/pull/89125)
- [#89103 Migrate in-tree crates to 2021](https://github.com/rust-lang/rust/pull/89103)
- [#89047 Rollup of 10 pull requests](https://github.com/rust-lang/rust/pull/89047)
- [#89030 Introduce `Rvalue::ShallowInitBox`](https://github.com/rust-lang/rust/pull/89030)
- [#88945 Remove concept of 'completion' from the projection cache](https://github.com/rust-lang/rust/pull/88945)
- [#88881 Rollup of 7 pull requests](https://github.com/rust-lang/rust/pull/88881)
- [#88824 Rollup of 15 pull requests](https://github.com/rust-lang/rust/pull/88824)
- [#88804 Revise never type fallback algorithm](https://github.com/rust-lang/rust/pull/88804)
- [#88719 Point at argument instead of call for their obligations](https://github.com/rust-lang/rust/pull/88719)
- [#88710 Use index newtyping for TyVid](https://github.com/rust-lang/rust/pull/88710)
- [#88703 Gather module items after lowering.](https://github.com/rust-lang/rust/pull/88703)
- [#88627 Do not preallocate HirIds](https://github.com/rust-lang/rust/pull/88627)
- [#88597 Move global analyses from lowering to resolution](https://github.com/rust-lang/rust/pull/88597)
- [#88575 Querify `FnAbi::of_{fn_ptr,instance}` as `fn_abi_of_{fn_ptr,instance}`.](https://github.com/rust-lang/rust/pull/88575)
- [#88552 Stop allocating vtable entries for non-object-safe methods](https://github.com/rust-lang/rust/pull/88552)
- [#88533 Concrete regions can show up in mir borrowck if the originated from there](https://github.com/rust-lang/rust/pull/88533)
- [#88530 Shrink Session a bit](https://github.com/rust-lang/rust/pull/88530)
- [#88435 Avoid invoking the hir_crate query to traverse the HIR](https://github.com/rust-lang/rust/pull/88435)
- [#88343 Fix spacing of links in inline code.](https://github.com/rust-lang/rust/pull/88343)
- [#88308 Morph `layout_raw` query into `layout_of`.](https://github.com/rust-lang/rust/pull/88308)
- [#87815 encode `generics_of` for fields and ty params](https://github.com/rust-lang/rust/pull/87815)
- [#87781 Remove box syntax from compiler and tools](https://github.com/rust-lang/rust/pull/87781)
- [#87688 Introduce `let...else`](https://github.com/rust-lang/rust/pull/87688)
- [#87064 Support `#[track_caller]` on closures and generators](https://github.com/rust-lang/rust/pull/87064)
- [#84373 Encode spans relative to the enclosing item](https://github.com/rust-lang/rust/pull/84373)
- [#83698 Use undef for uninitialized bytes in constants](https://github.com/rust-lang/rust/pull/83698)
- [#83302 Get piece unchecked in `write`](https://github.com/rust-lang/rust/pull/83302)

## Nominated Issues

[T-compiler](https://github.com/rust-lang/rust/issues?q=is%3Aopen+label%3AI-nominated+label%3AT-compiler)

- "On macOS, make strip="symbols" not pass any options to strip" [rust#88137](https://github.com/rust-lang/rust/pull/88137)
  - discussed in PR waiting-on-team
- "Rust can't infer appropriate generics for function when it should" [rust#89242](https://github.com/rust-lang/rust/issues/89242)
  - Issue opened by @**TheRawMeatball**
  - regression from stable to beta
  - Investigated by @**Jack Huey**, [suggests ways to move forward](https://github.com/rust-lang/rust/issues/89242#issuecomment-930760694)

[RFC](https://github.com/rust-lang/rfcs/issues?q=is%3Aopen+label%3AI-nominated+label%3AT-compiler)

- No nominated RFCs for `T-compiler` this time.

## Misc

- Handling RLS 1.0 issue during T-compiler meeting ([Zulip topic](https://rust-lang.zulipchat.com/#narrow/stream/131828-t-compiler/topic/Handling.20RLS.20issues.20during.20the.20meeting.3F))
  - @**nagisa** [comment on github](https://github.com/rust-lang/rust/issues/58858#issuecomment-927108585)
  - Can that issue be closed and perhaps remove RLS from [rust#54818](https://github.com/rust-lang/rust/issues/54818)?
