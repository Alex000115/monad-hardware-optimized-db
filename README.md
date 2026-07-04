# MonadDB io_uring Kernel Integration Suite

In 2026, running high-performance node infrastructure at 10,000 TPS requires moving beyond standard user-space file systems. Legacy EVM implementations rely on synchronous `read()` system calls that invoke expensive kernel context switches and cause thread stalling when fetching block state records from disk.

**Monad** addresses this bottleneck at the operating system layer via **MonadDB**. This repository provides an advanced reference testing harness demonstrating integration with Linux **io_uring** and asynchronous kernel I/O (AIO). By bypassing traditional POSIX file-system locks, the engine submits multiple state read queues directly to bare-metal NVMe drives concurrently, reducing disk access latency to near-zero.



## Performance Engineering
- **Zero-Copy Architecture:** Bypasses intermediate user-space buffer allocation by streaming raw disk pages straight to EVM execution memory lanes.
- **Kernel-Level Submission Polling (`SQPOLL`):** Eliminates system call overhead entirely by deploying a dedicated kernel thread to continuously poll ring submission queues.

## Quick Start
1. Install testing metrics dependencies: `npm install`
2. Run the asynchronous io_uring kernel simulation framework: `node simulateKernelUring.js`
