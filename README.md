# Katali-OS

Katali-OS is an experimental standalone x86-64 operating system being developed toward native local-AI operation without requiring Windows or Linux underneath it.

The long-term goal is a general-purpose bare-metal OS where local AI can be a native subsystem. The kernel remains responsible for hardware control, memory protection, security, and validated capabilities. Models do not receive unrestricted ring-0 access.

## Current status

The project has progressed from a bootable kernel to an early bare-metal model-inference demonstration. The status below separates hardware-verified foundations from experimental features and planned work.

### Working and verified

- Native x86-64 long-mode boot.
- Physical and virtual memory managers, plus a kernel heap.
- GDT, TSS, IDT, and exception handling.
- ACPI hardware discovery and SMP startup.
- SMP physically verified with all logical CPUs online on two systems:
  - Intel Core i5-10400 desktop: 12/12 logical CPUs.
  - Intel Core i5-10300H laptop: 8/8 logical CPUs.
- PCI/PCIe enumeration on physical hardware, including discovery of NVMe, graphics, USB-controller, Ethernet, and other PCI devices. Compatibility is still being tested across machines.
- Read-only NVMe access and NTFS path lookup on tested hardware.
- Native CPU inference demonstrated on physical hardware with Qwen3-4B Q4_K_M, loaded from NVMe through the read-only storage path and used for interactive prompts.
- A Qwen chat session can retain recent turns until reboot and can be cleared by the user. The current interactive response limit is 128 generated tokens; this latest limit has passed the build and emulator boot checks and still needs a physical retest.

### Limited or not implemented

- Storage access is read-only; Katali-OS does not write to the detected disks.
- Model support is limited to the tested Qwen3 GGUF configurations. A general model installer, model manager, or broad compatibility with arbitrary model formats is not available.
- CPU inference is slow on current hardware, and response quality, length, and performance are still being evaluated. GPU inference is not implemented.
- Production-grade NVMe support, general filesystem support, and model loading across different hardware remain incomplete.
- Networking, USB device support, and a higher-level desktop-like environment are not implemented.

The Qwen3-4B result confirms that a multi-billion-parameter quantized model can be loaded and run directly on bare metal in the tested configuration. It is an early technical demonstration, not a claim of production-quality output, performance, or broad model compatibility.

## AI direction

The current research direction is CPU-oriented inference using SIMD/AVX2 where available, multicore execution, and system RAM. BitNet and ternary-model inference are future research areas. Hardware capabilities should be discovered at runtime so the OS can adapt across machines instead of being built for one computer.

The AI layer will use controlled, validated kernel capabilities. The kernel remains the authority for hardware access, memory protection, and security.

## Roadmap

1. **x86-64 foundation** — working.
2. **Memory management** — working.
3. **SMP and multicore** — physically verified on two systems.
4. **PCI/PCIe enumeration** — working; hardware compatibility testing continues.
5. **NVMe storage** — read-only access demonstrated; robust driver support remains in progress.
6. **Filesystem and model loading** — read-only NTFS path lookup and tested model loading demonstrated; broader support remains in progress.
7. **Native AI runtime** — Qwen3-4B Q4_K_M CPU inference demonstrated on physical hardware; interactive chat is experimental and performance/output are being improved.
8. **BitNet/ternary CPU inference** — planned research.
9. **Networking, USB, and broader drivers** — planned.
10. **Higher-level Katali-OS environment** — planned.

## Disclaimer

Katali-OS is experimental research software. It is not currently intended to replace a production desktop operating system.
