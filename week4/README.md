# Week 4: reproducibility and evidence integrity（by Wu Has）

## Contribution

This week adds a lightweight audit for the experiment evidence already stored in the repository. It checks the six Week 2 CSV logs (three runs for each booting kernel) and the three Week 3 `mitigations=off` logs. It verifies each log's kernel label, checks that the `kbest` test names and their order agree across runs, checks that the Week 3 boot command line records `mitigations=off`, and confirms that three Week 3 wall-clock records are present.

The audit also calculates a SHA-256 fingerprint for every input CSV and writes `reproducibility_report.md`. This makes it easier to detect accidental changes to the archived evidence before regenerating or discussing results.

## Run

From the repository root, with Python 3.10 or newer:

```bash
python week4/reproducibility_check.py
```

No third-party Python packages are required. A successful run prints the checks and updates `week4/reproducibility_report.md`. A missing file, unexpected kernel label, inconsistent test list, missing `mitigations=off` record, or wrong number of wall-clock records causes a non-zero exit status.

## Scope and limitations

This is an integrity and consistency check, not a new LEBench run. It does not change the original CSV files or previous-week summaries, install or boot kernels, or claim to independently verify the machine configuration. Hashes identify the exact files inspected; they do not prove how the measurements were produced. The Week 2 and Week 3 source notes remain the provenance records for those experiments.

# Week4 Experiment: Ubuntu16.04 VirtualBox VM（by Fan Borui）
## Goal
Reproduce the baseline kernel v4.0.5 and kernel v4.15.0-112 from the paper Figure 1.
- v4.0.5: baseline, without KPTI / Spectre mitigations
- v4.15.0-112: kernel with KPTI + Retpoline security patches

## Environment
- Hypervisor: Oracle VirtualBox
- Guest OS: Ubuntu 16.04
- Benchmark: LEBench / OS_Eval
- Kernel 1: 4.0.5-040005-generic
- Kernel 2: 4.15.0-112-generic

## Status
Boot successfully
OS_Eval completed, CSV output generated


## Run command
```bash
cd ~/LEBench
./OS_Eval
# After run, rename csv to avoid overwrite
cp output.4.0.5-040005-generic.csv raw_csv/output.4.0.5-040005-generic_run1.csv

## Limitations

1. This experiment runs on VirtualBox VM, not the original physical Xeon E5 server from the paper. Virtualization overhead exists.
2. Only two kernel versions are tested, not the full set of 36 kernels in the original paper. This is a reduced-scale reproduction.
