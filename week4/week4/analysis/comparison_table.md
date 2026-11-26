# Comparison: v4.0.5 vs v4.15.0-112 (kbest latency)
| test | v4.0.5 kbest (s) | v4.15 kbest (s) | ratio (v4.15 / v4.0) |
| ---- | ---- | ---- | ---- |
| ref | 0.000000120 | 0.000000050 | 0.417 |
| cpu | 0.004292636 | 0.004284857 | 0.998 |
| getpid | 0.000000170 | 0.000000120 | 0.706 |
| context switch | 0.000002004 | 0.000002989 | 1.492 |
| send | 0.000002690 | 0.000002500 | 0.929 |
| recv | 0.000002410 | 0.000003200 | 1.328 |
| big send | 0.000005501 | 0.000005342 | 0.971 |
| big recv | 0.000004258 | 0.000004590 | 1.078 |
| fork | 0.000029205 | 0.000045183 | 1.547 |
| thr create | 0.000022740 | 0.000011833 | 0.520 |
| big fork | 0.000483440 | 0.000613354 | 1.269 |
| huge fork | 0.001202813 | 0.001641392 | 1.365 |

> Note: "context siwtch" in raw log is typo for context switch.

We observe higher latency for fork-family operations in Linux 4.15, likely caused by additional security mechanisms.
Thread creation is optimized and faster in 4.15. Simple lightweight syscalls such as getpid also gain minor speedups.
