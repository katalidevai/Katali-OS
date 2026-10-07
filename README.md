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
- Experimental native CPU inference with Qwen3 0.6B in GGUF Q8_0 format, including basic prompt/response interaction.

### Limited or not implemented

- Storage access is read-only; Katali-OS does not write to the detected disks.
- Model support is limited to the tested configuration. A general model installer, model manager, or broad compatibility with arbitrary model formats is not available.
- Session chat/context handling is under development and has not yet been re-verified on physical hardware in its latest form.
- Production-grade NVMe support, general filesystem support, and model loading across different hardware remain incomplete.
- Networking, USB device support, and a higher-level desktop-like environment are not implemented.

The inference result is an early technical demonstration, not a claim of production-quality model output, performance, or compatibility.

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
7. **Native AI runtime** — initial Qwen3 0.6B CPU inference demonstrated; experimental.
8. **BitNet/ternary CPU inference** — planned research.
9. **Networking, USB, and broader drivers** — planned.
10. **Higher-level Katali-OS environment** — planned.

## Disclaimer

Katali-OS is experimental research software. It is not currently intended to replace a production desktop operating system.
