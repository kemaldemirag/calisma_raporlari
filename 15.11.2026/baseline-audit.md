# U02 MBSE-ECAD Software Integration - G0 Baseline Audit

## Document control

| Field | Value |
|---|---|
| Gate | G0 - Baseline Audit |
| Audit time | 2026-11-16, Europe/Istanbul |
| Scope | U02 `lensless-holography-workbench` and its 15.11.2026 evidence baseline |
| Audit mode | Read-only inspection plus the requested regression executions |
| Source-code changes | None |
| Git index/history/remote changes | None |
| Overall result | **BLOCKED** |

The U02 repository itself is clean, synchronized with its locally recorded
`origin/main`, and its current regression suite passes. G0 is nevertheless
`BLOCKED` because the mandatory "15.11.2026 İş Akışı ve Kabul Planı v2" is not
present, and the workspace verifier fails against paths and evidence hashes
that were not reconciled after later development and the relocation of the
Model Raporları files.

This report is the only persistent artifact created by G0. It is outside the
U02 Git repository. No production code, test, schema, tracked document, Git
index, commit, branch, tag, remote, or history was changed.

## Gate report

| Reporting item | Result |
|---|---|
| Gate ID | G0 |
| Inspected files | Workspace control documents, v1 plan fallback, U02 repository, source/tests/schemas, K03 package and validation records, historical 27-test record |
| Operations | File discovery, content inspection, SHA-256 verification, Git inspection, current full regression execution, workspace verifier execution |
| U02 regression | **PASS** - 164 discovered, 161 passed, 0 failed/errors, 3 condition-based skips |
| Workspace verifier | **FAIL** - 83/88 checks passed |
| Mandatory v2 input | **BLOCKED** - missing |
| Physical tests | **NOT_RUN** - no hardware and not authorized by the evidence baseline |
| U02-T2 acceptance | **NOT_RUN / NOT_EVALUATED** |
| U02-T3 acceptance | **NOT_RUN / field data required** |
| Recommended transition | Do not start G1 as an authoritative baseline until v2 is supplied or the owner explicitly authorizes provisional use of the master task plus v1 |

## 1. Mandatory input audit

| Mandatory input | Status | Verified location / note |
|---|---|---|
| Workspace `README.md` | FOUND | `15.11.2026/README.md` |
| `DECISIONS.md` | FOUND | `15.11.2026/DECISIONS.md` |
| `NEXT-TASKS.md` | FOUND | `15.11.2026/NEXT-TASKS.md` |
| `PROJECT-MANIFEST.json` | FOUND | `15.11.2026/PROJECT-MANIFEST.json` |
| 15.11.2026 İş Akışı ve Kabul Planı v2 | **MISSING / BLOCKER** | Not found in the active tree or inside `15.11.2026_Model_Raporlari_v1.zip` |
| İş Akışı ve Kabul Planı v1 | FOUND, informational only | Root-level `.docx` and `.pdf`; not accepted as a substitute for v2 |
| U02 source, tests, Git history | FOUND | `002-Proje Çıktıları/lensless-holography-workbench` |
| K03 experiment package and validation | FOUND | `003-Proje Kayıtları/deneyler/15.11.2026` |

### 1.1 Missing v2 evidence

Recursive filename inspection and ZIP-entry inspection found only:

- `15.11.2026_02_Is_Akisi_ve_Kabul_Plani_v1.docx`
- `15.11.2026_02_Is_Akisi_ve_Kabul_Plani_v1.pdf`

The v1 identities are:

- DOCX SHA-256:
  `39f5b355323b71ff4c26c2ca5ee53bed2e25549d5b57b34e49564033e8eaf91b`
- PDF SHA-256:
  `6210344dfe8d99eb8b4203cbc4ae72ccf1f4ccc0b0cbd3a22e466c191773cf4d`
- PDF pages: 5

V1 was read only to understand the historical baseline. It defines U02-T1 as
a 512 x 512, central 256 x 256, 0-20 um / 1 um numerical repeat; leaves U02-T2
`BEKLİYOR`; and requires real RAW/exposure/gain/sensor-mode/time correlation
for U02-T3. No v2 content was inferred or invented.

### 1.2 Controlling decisions

- U02 is the primary product; `shelf-load-monitor` is explicitly out of scope.
- The K03 archive is immutable evidence and product code must not silently
  replace or vendor its inputs.
- U02-T1 is a numerical reproduction, not physical-focus validation.
- U02-T2 remains `BEKLİYOR`; comparisons remain `NOT_EVALUATED` until a
  threshold is registered before evaluation.
- U02-T3 requires real Pi RAW frames and uniquely correlated metadata.
- The current master task overrides earlier standing commit/push practices:
  this audit created no commit, push, PR, merge, rebase, reset, or history
  change.

## 2. Git baseline

| Attribute | Observed value |
|---|---|
| Repository | `15.11.2026/002-Proje Çıktıları/lensless-holography-workbench` |
| Active branch | `main` |
| HEAD | `584486a4272e7a4a077db70d6688b4146a69f524` |
| HEAD subject | `docs(autofocus): document numerical navigation boundary` |
| Upstream | `origin/main` |
| Local tracking difference | `+0 / -0` |
| Worktree | Clean |
| Remote | `https://github.com/kemaldemirag/lensless-holography-workbench.git` |
| Commit count | 42 |
| Tracked files | 56 |
| Tags | None |

No `fetch` was performed. Therefore `+0/-0` proves equality with the locally
recorded remote-tracking ref, not an independent live query of GitHub.

Most recent four commits:

1. `584486a` - docs(autofocus): document numerical navigation boundary
2. `5ae8f11` - feat(autofocus): serialize source-bound focus results
3. `d33403b` - feat(autofocus): add deterministic coarse-to-fine search
4. `129f3cd` - feat(focus): add deterministic focus metric primitives

## 3. Actual tracked repository tree

```text
.gitattributes
.gitignore
README.md
configs/
  u02-t1.json
docs/
  acceptance.md
  autofocus.md
  development-status.md
  external-fixtures.md
  point-source-backend.md
  unal-k18-source-profile.md
  windows-release.md
  windows-workflow.md
pyproject.toml
requirements.txt
requirements-release.lock
release/windows/
  PORTABLE-README.txt
  THIRD-PARTY-NOTICES.txt
  launcher.py
  lensless_holography_workbench.spec
schemas/
  session.schema.json
  unal-k18-fixture.schema.json
src/lensless_holography_workbench/
  __init__.py
  autofocus.py
  cli.py
  comparison.py
  depth_scan.py
  desktop_workflow.py
  focus_metrics.py
  image_io.py
  opened_session.py
  point_source.py
  session.py
  unal_fixture.py
  windows_app.py
tests/
  __init__.py
  negative/
    __init__.py
    test_invalid_inputs.py
  reproducibility/
    __init__.py
    test_k03_real_data.py
    test_unal_k18_fixture.py
  unit/
    __init__.py
    test_autofocus.py
    test_cli.py
    test_comparison.py
    test_depth_scan.py
    test_desktop_workflow.py
    test_focus_metrics.py
    test_image_io.py
    test_opened_session.py
    test_point_source.py
    test_session.py
    test_unal_fixture.py
    test_windows_app.py
    test_windows_release.py
tools/
  __init__.py
  windows_release.py
```

Ignored build, artifact, and `.test-tmp` content exists physically but is not
part of the 56-file tracked baseline.

## 4. Current software baseline

| Item | Value |
|---|---|
| Project version | 0.3.1 |
| Required Python | >=3.12 |
| Audit runtime | CPython 3.12.14, 64-bit |
| NumPy | 2.3.5 |
| Pillow | 13.0.0 |
| Runtime dependencies | NumPy and Pillow only |
| Optional release dependencies | PyInstaller 6.22.3 and hooks package |
| CLI | `holography-workbench` |
| GUI | `holography-workbench-gui` |

The Windows-installed `python` command is Python 3.12.10 and lacks the audit
runtime's pinned NumPy environment. The current regression was therefore run
with the workspace runtime documented by the evidence records: Python 3.12.14,
NumPy 2.3.5, and Pillow 13.0.0.

Existing production responsibilities:

- `depth_scan.py`: normalization, `PreparedWavefront`, propagation and depth
  scan metrics.
- `session.py`: session 1.0, TIFF/CSV/JSON, input snapshots and SHA-256
  publication.
- `opened_session.py`: strict file-set, hash and semantic reopen checks.
- `desktop_workflow.py`: asynchronous desktop scan state, caching, export and
  reopen orchestration.
- `cli.py`: file-based signal/background/reference workflow.
- `windows_app.py`: Tkinter shell.
- `autofocus.py` / `focus_metrics.py`: numerical navigation only.
- `comparison.py`: comparison without an acceptance decision.
- `point_source.py` / `unal_fixture.py`: separate KH numerical backend and
  fail-closed external-fixture boundary.

No `DeviceAdapter`, `VirtualLED`, `VirtualCamera`, device command schema,
ACK/NACK contract, device control service, or `SIMULATED` acquisition record
exists in the baseline.

## 5. Test commands and new G0 execution

### 5.1 Documented full command

```powershell
$env:PYTHONPATH='src'
python -m unittest discover -s tests -t . -v
```

For G0, `python` was replaced only by the verified workspace Python 3.12.14
executable; all unittest arguments were unchanged.

### 5.2 Targeted K03 command

```powershell
$env:PYTHONPATH='src'
python -m unittest tests.reproducibility.test_k03_real_data -v
```

The full suite already executed this K03 case, so a redundant second run was
not used as separate evidence.

### 5.3 New G0 regression result

| Field | Result |
|---|---|
| Start | 2026-11-16T17:48:14.4967817+03:00 |
| End audit sample | 2026-11-16T17:48:49.2765973+03:00 |
| unittest-reported duration | 8.282 s |
| Process exit | 0 |
| Discovered/run | 164 |
| Passed | 161 |
| Failed | 0 |
| Errors | 0 |
| Skipped | 3 |
| Result | **PASS with 3 explicit condition-based skips** |

Skipped conditions:

1. External UNAL K18 manifest is not configured (`UNAVAILABLE:NOT_CONFIGURED`).
2. Windows symlink creation privilege is unavailable for the manifest-symlink
   test (`WinError 1314`).
3. The same privilege limitation applies to the asset-symlink test.

The K03 21-row real-data reproducibility test passed inside this run. Git
status remained clean after the tests.

### 5.4 Workspace verifier result

Command:

```powershell
python scripts/verify_workspace.py
```

Result: **FAIL**, exit 1, 83/88 checks passed.

The five failures were:

1. Missing old path
   `Model Raporları/15.11.2026_TESLIM_MANIFESTI.json`.
2. Missing old path
   `Model Raporları/15.11.2026_kaynak_envanteri.csv`.
3. Missing old path
   `Model Raporları/15.11.2026_urun_test_matrisi.csv`.
4. Model-report ZIP hash check used the missing old `Model Raporları/` path.
5. The point-source evidence file-set hash check failed because
   `src/lensless_holography_workbench/__init__.py` changed after that evidence
   record. The other three recorded point-source files still match.

The moved root-level model-report ZIP still matches the manifest SHA-256:

`9d2c760b1762dfbfd947d9c4ffdffb12e9dfb7b5dcfbdbd52cf1b61675eaf06a`

This is workspace metadata/verifier drift, not a current U02 unit-test
failure. The verifier also hard-codes the old `d76abec` / 38-commit / 137-test
baseline and compares the manifest to those constants rather than comparing
the manifest with the actual repository HEAD. Its PASS lines for those fields
must not be read as proof that the manifest is current.

## 6. Historical 27-test record versus the new run

### 6.1 Historical record

Evidence file:

`003-Proje Kayıtları/U02/20261115-u02-t2-headless-core-v4.PROVENANCE.json`

| Field | Historical value |
|---|---|
| Product version | 0.1.0 |
| Recorded commit | `be3b5ba75d5ff61cc3c84636659d6aaf295e5c4b` |
| Environment | Python 3.12.14 / NumPy 2.3.5 / Pillow 13.0.0 |
| Recorded result | 27 passed, 0 failed, 0 skipped |
| U02-T2 | `BEKLİYOR` |
| Comparison | `NOT_EVALUATED` |

Limitations of the historical record:

- It does not record the exact command, start/end timestamp, duration, stdout,
  or individual test-case list.
- Commit `be3b5ba` is still present as a Git object, but it is not an ancestor
  of current HEAD and no local/remote-tracking branch contains it.
- Its tree `7a942d1c...` appears in the current history at commit `040906d`.
- The old snapshot contained 27 test methods across five test files; current
  discovery is materially larger.

### 6.2 Required separation

The historical `27/27` is a dated record only. It is not upgraded, replaced,
or combined with the new `164 run / 161 pass / 3 skip` result. The current G0
result is tied to HEAD `584486a` and the timestamps in section 5.3.

## 7. K03 evidence baseline

| Evidence | Result |
|---|---|
| Archive SHA-256 | `c9d1f3d69354c38ed6325b73c54450cf3d6042ebfab32b213e94d7dfbb7ba107` - matched |
| `deney.py` SHA-256 | `19b14df3c90556bd7ae404e28803991a100520057593054f3bd478e65c8fab25` - matched |
| Required inputs | 11/11 present and SHA-256 matched |
| Optional IMX477 DNG | Absent, consistent with the prior validation record |
| Recorded result outputs | All five recorded output hashes matched |
| U02-T1 result | 512 x 512 input, 256 x 256 central ROI, 21 planes, both peaks at 0 um |
| Physical focus | Not established |

The current K03 regression pins the four holography input hashes, checks all
21 numerical rows at absolute tolerance `1e-12`, and verifies the 0 um peaks,
input shape and ROI. K03 `hologram.csv` and the later U02 session
`metrics.csv` are not byte-identical; only the explicitly tested numerical
and semantic equivalence is claimed.

K03 does not include the physical hardware evidence needed for U02-T3 and does
not complete U02-T2 reference-image acceptance.

## 8. Baseline drift and blockers

### BLOCKER-01 - Mandatory v2 plan is missing

The requested v2 is absent from both the active tree and the model-report ZIP.
V1 cannot be silently treated as v2. Authoritative G1 requirement baselining
is blocked until v2 is supplied or the owner explicitly approves a
provisional baseline based on this master task plus v1.

### BLOCKER-02 - Workspace control documents are stale

- Workspace `README.md` still describes U02 at 0.2.0 / 61 tests and an older
  delivery head.
- `PROJECT-MANIFEST.json` records U02 HEAD `d76abec`, 38 commits and 137 tests.
- Actual U02 is HEAD `584486a`, 42 commits, with the new G0 run described in
  section 5.3.
- `NEXT-TASKS.md` does not include the new autofocus or MBSE-device work.

These documents are inputs to G1 traceability and must be reconciled, but they
were not edited in read-only G0.

### BLOCKER-03 - Workspace verifier paths and evidence hashes drifted

The Model Raporları files were moved to the 15.11.2026 root, while the
manifest, README and verifier still use the removed directory. The
point-source validation record also pins an older package `__init__.py` hash.

### BLOCKER-04 - Physical and acceptance inputs remain open

- LED datasheet/current limits are not supplied. No physical current boundary
  may be asserted.
- K07/K18 authorized images and the pre-registered U02-T2 similarity threshold
  remain incomplete.
- Real Pi RAW frames and device metadata are absent.

These do not prevent virtual-device development after approval, but they do
prevent physical PASS and U02-T2/U02-T3 acceptance closure.

### BLOCKER-05 - Write authorization has not been granted

This task explicitly requires a new user authorization before code changes and
a separate later authorization before any commit. Neither is inferred from
earlier conversations or documents.

## 9. Collision analysis

The requested delivery filenames do not currently exist, so there is no
physical filename collision if they are placed under a new `docs/mbse/`
namespace. There are important semantic collisions:

1. `session.py` owns session 1.0 and requires selected depth to belong to the
   current scan grid.
2. `schemas/session.schema.json` has top-level `additionalProperties: false`;
   device metadata cannot be added silently at the top level.
3. `opened_session.py` reconciles declared outputs, manifest entries and the
   physical file set. Any new sidecar must be updated and tested across all
   three layers.
4. `DesktopWorkflow` already owns asynchronous `WorkflowState`; device states
   must use a separate enum and composition, not extend this enum casually.
5. `InputSelection` and `ScanRequest` already exist. Device contracts should
   use distinct names such as `DeviceCommand` and `CaptureRequest`.
6. The existing CLI is file-based. Virtual-device support must be opt-in and
   must not alter existing CLI defaults.
7. Current autofocus and point-source modules already have explicit numerical
   claim boundaries; control integration must reuse rather than fork them.
8. Existing session TIFF/JSON/CSV bytes and reopen rules are regression
   contracts.

## 10. Proposed G1-G6 implementation plan

All identifiers below are **provisional** until G1 is authorized and the v2
source gap is resolved.

### G1 - System architecture

Proposed files:

- `docs/mbse/requirements.md`
- `docs/mbse/architecture.md`

Proposed requirement families:

- `U02-SYS-*`: preservation, separation of responsibilities and traceability.
- `U02-LED-*`: LED command/state/safe-off behavior.
- `U02-CAM-*`: capture request, frame metadata and correlation.
- `U02-SES-*`: session provenance and sidecar integrity.
- `U02-IMG-*`: reuse of the existing hologram processing core.
- `U02-SIM-*`: deterministic simulation and explicit `SIMULATED` marking.
- `U02-ACC-*`: claim and acceptance boundaries.

Architecture will separate LED control, camera acquisition, control/session
orchestration and image processing. Mermaid context, component and state
diagrams will be included. No code dependency is proposed in G1.

Exit proposal: architecture review, unique IDs, source references and no
unresolved collision with session 1.0.

### G2 - Interface contracts

Proposed files:

- `docs/mbse/icd.md`
- `schemas/device-command.schema.json`
- `schemas/device-response.schema.json`
- `schemas/capture-record.schema.json`
- `tests/unit/test_device_contracts.py`

The ICD will define request/response envelopes, `request_id`, device type,
command, units, numeric bounds, timeout semantics, ACK/NACK, closed error-code
enums and device states. Command acceptance and measurement validation will be
separate fields/events. LED physical-current limits will remain
`DATASHEET_REQUIRED`; simulation bounds will be labeled as simulation bounds.

No new runtime framework is proposed. Standard-library JSON parsing plus the
same fail-closed validation style already used by `unal_fixture.py` can keep
runtime dependencies at NumPy and Pillow. Any request for a full third-party
JSON Schema validator would be raised separately as a development-only
dependency decision.

Provisional verification IDs: `U02-CT-001` through `U02-CT-0xx`.

### G3 - Virtual devices

Proposed files:

- `src/lensless_holography_workbench/device_adapter.py`
- `src/lensless_holography_workbench/virtual_devices.py`
- `tests/unit/test_virtual_devices.py`

Planned design:

- Standard-library `Protocol`/ABC, dataclasses and closed enums.
- `VirtualLED` with deterministic state, ACK/NACK, timeout/fault injection and
  idempotent safe-off.
- `VirtualCamera` with deterministic frame/capture metadata generation,
  duplicate-request rejection, timeout/fault injection and shutdown.
- Injected clock/ID source so repeated inputs produce repeated records.
- Every virtual measurement and frame marked `SIMULATED`; no hardware or
  physical-validation claim.

Provisional verification IDs: `U02-VD-001` through `U02-VD-0xx`.

### G4 - Control integration

Proposed files:

- `src/lensless_holography_workbench/control_service.py`
- `tests/unit/test_control_service.py`
- `tests/integration/test_virtual_control_pipeline.py`
- optionally a versioned `device-session.json` sidecar contract after detailed
  G2 review

The service will correlate command/capture IDs, virtual timestamps, parameters
and session records, then pass captured arrays to the existing U02
normalization/propagation/session code. It will not duplicate the hologram
core. Real Raspberry Pi adapters will remain interface-only stubs.

To preserve session 1.0, the preferred design is an opt-in, versioned sidecar
declared under `outputs`, included in `sha256.json`, and semantically validated
by reopen logic. Existing runs without the sidecar must remain byte- and
behavior-compatible. This design must be confirmed in G2 before code.

Provisional verification IDs: `U02-INT-001` through `U02-INT-0xx`.

### G5 - Verification

Planned commands/evidence:

- Existing full regression command from section 5.1.
- Focused contract, virtual-device and control-service unittest modules.
- Repeated identical virtual runs with canonical JSON/hash comparison.
- Negative ACK/NACK, invalid-unit/range, timeout, duplicate ID and safe-shutdown
  cases.
- K03 regression unchanged.

Planned deliverables:

- `validation-report.md`
- `requirements-traceability.md`

Each requirement will map to test IDs, commands, evidence files and result.
U02-T2 and U02-T3 will not be set to PASS.

### G6 - Delivery

Planned deliverables:

- `integration-summary.md`
- `open-issues.md`
- `delivery-manifest.json`

The manifest will list every created/modified file, its SHA-256, related
requirement/test IDs, verification status and residual risk. It will explicitly
separate simulated evidence, numerical regression, physical tests not run and
acceptance decisions not evaluated.

No commit will be created during G1-G6 without a separate explicit commit
approval. No push, PR, merge, rebase, reset or history rewrite is planned.

## 11. Proposed change-to-requirement/test mapping

| Proposed change | Provisional requirement IDs | Planned tests/evidence |
|---|---|---|
| Architecture/requirements docs | `U02-SYS-*`, `U02-ACC-*` | Document review and traceability completeness |
| Device command/response schemas | `U02-LED-*`, `U02-CAM-*`, `U02-SIM-*` | `U02-CT-*`, schema/code parity tests |
| `DeviceAdapter` | `U02-SYS-*` | `U02-CT-*`, adapter conformance tests |
| `VirtualLED` | `U02-LED-*`, `U02-SIM-*` | `U02-VD-LED-*` |
| `VirtualCamera` | `U02-CAM-*`, `U02-SIM-*` | `U02-VD-CAM-*` |
| Control service | `U02-SES-*`, `U02-IMG-*` | `U02-INT-*` |
| Optional device sidecar | `U02-SES-*`, `U02-ACC-*` | reopen, hash, tamper and backward-compatibility tests |
| G5/G6 reports | all approved IDs | full regression plus requirements traceability matrix |

## 12. Transition recommendation

G0 evidence collection is complete, but the gate is `BLOCKED` for an
authoritative transition because v2 is missing. Two safe paths exist:

1. Supply the exact v2 document and authorize G1 writing; or
2. Explicitly authorize a provisional G1 baseline using this master task plus
   v1, with a mandatory later v2 reconciliation gate.

After either decision, code work should still wait until the user explicitly
authorizes it. Commit creation requires a further, separate approval.

