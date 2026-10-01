# Katali-OS

Katali-OS is an experimental standalone x86-64 operating system being developed toward native local-AI operation without requiring Windows or Linux underneath it.

The long-term goal is a general-purpose bare-metal operating system where local AI becomes a native subsystem. The kernel remains responsible for hardware control, memory protection, security, and validated capabilities.

## Current verified project status

The following foundations are working:

- Native x86-64 long-mode boot
- Physical memory manager
- Virtual memory manager
- Kernel heap
- GDT, TSS, IDT, and exception handling
- ACPI hardware discovery
- Multi-core/SMP support
- PCI/PCIe enumeration on physical hardware

SMP has been physically verified on:

| System | Logical CPUs online |
| --- | --- |
| Intel Core i5-10400 desktop | 12/12 |
| Intel Core i5-10300H laptop | 8/8 |

Hardware discovery identifies NVMe devices, GPUs, USB controllers, Ethernet controllers, and other PCI devices. Device enumeration does not imply that drivers for those devices are implemented.

PCI behavior is currently being hardened across different physical machines, with ongoing hardware compatibility testing.

The following capabilities are **not implemented yet**:

- NVMe driver
- Filesystem and model loading
- Native LLM inference

Katali-OS does not currently load or run AI models.

## Roadmap

The roadmap describes the intended development sequence. Planned phases are not claims of existing functionality.

| Phase | Area | Status |
| --- | --- | --- |
| 1 | x86-64 foundation | Working |
| 2 | Memory management | Working |
| 3 | SMP/multicore | Physically verified |
| 4 | PCI/PCIe | Working; hardware compatibility testing ongoing |
| 5 | NVMe read-only storage | Planned |
| 6 | Filesystem and model loading | Planned |
| 7 | Native AI runtime | Planned |
| 8 | BitNet/ternary CPU inference | Planned research |
| 9 | Networking, USB, and broader driver support | Planned |
| 10 | Higher-level Katali-OS environment | Planned |

## AI direction

Katali-OS is ultimately intended to run local models directly on bare metal.

The current preferred research direction is CPU-oriented inference, including BitNet/ternary models, SIMD/AVX2 optimization, multicore execution, and efficient use of system RAM. These are future research and implementation goals; native inference is not currently available.

The AI layer is not intended to have unrestricted ring-0 hardware access. The kernel remains the authority and exposes controlled, validated capabilities to the AI subsystem. Hardware access and security decisions remain under kernel control.

## Portability

Portability across x86-64 machines is an important design goal. Katali-OS should discover hardware and available capabilities rather than rely on assumptions hard-coded for one specific computer.

Testing across physical systems is part of this effort. Current hardware verification does not establish compatibility with every x86-64 machine.

## Public repository scope

This public repository is intentionally README-only for now. Source code, kernel code, binaries, boot images, build files, tools, scripts, model files, internal documentation, test artifacts, and private development files are not published here.

## Experimental status

Katali-OS is experimental research software. It is not currently intended as a replacement for a production desktop operating system.
