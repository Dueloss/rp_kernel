Red Plasma Kernel (RP_Kernel)

Red Plasma is a 100% modular, high-performance game engine designed to scale from 16-bit homebrew hardware to modern Fedora/Linux workstations. The Kernel serves as the hardware-agnostic "Heartbeat" of the system.
🏗️ Architectural Philosophy

The Kernel follows a strict "Lego-Style" modularity. It contains no graphics, sound, or input code. Instead, it manages the lifecycle of independent plugins through a standardized SDK contract.

    Sandboxed Plugins: Each plugin resides in its own dedicated folder with a manifest file.

    Evolutionary Calibration: The engine measures system performance across sessions to "learn" and optimize its fixed physics frequency (Hz).

    Tiered Error System: Every function returns a standardized RP_Result with specific "Zip Code" ranges for instant hardware/software diagnostics.

📂 Project Structure
Plaintext

rp_kernel/
├── src/                # Kernel Heartbeat & Plugin Loader
├── include/            # Internal Kernel headers
├── build/              # Output directory (Out-of-source build)
│   └── plugins/        # The Plugin Sandbox
├── RULES.md            # The Engine Constitution
└── LICENSE             # Mozilla Public License 2.0

🛠️ Build Requirements (Fedora)

To prepare your environment for the Red Plasma toolchain:
Bash

sudo dnf install gcc-c++ cmake ninja-build wayland-devel vulkan-loader-devel glslang

🚀 Getting Started

    Configure: cmake -S . -B build

    Compile: cmake --build build

    Run: ./build/RedPlasmaKernel

⚖️ License

This project is licensed under the Mozilla Public License 2.0 (MPL-2.0). This allows for closed-source plugins while ensuring the Core Kernel remains open and improved by the community.
