Contributing to Red Plasma

Thank you for your interest in the Red Plasma Kernel! To maintain our "Lego-Style" modularity and ensure performance from 16-bit hardware to modern workstations, all contributors must follow these guidelines.
⚖️ Licensing & Legal

    MPL-2.0 Core: The Kernel is licensed under the Mozilla Public License 2.0.

    Mandatory Headers: Every new source file in the src/ or include/ directory must contain the standard MPL-2.0 notice.

    Plugin Freedom: Contributions to the core Kernel remain open-source, but the architecture explicitly supports closed-source, proprietary plugins in their own sandboxed folders.

🏗️ Architectural Guardrails

    The Kernel is Blind: Never include headers from specific plugins (e.g., Vulkan, Wayland) inside the Kernel core.

    Zip Code Results: All functions must return an RP_Result enum to ensure the system remains self-diagnosing.

    Memory Management: Avoid raw new and delete in the main loop to prevent fragmentation on low-RAM systems; use the provided engine memory management.

📝 Coding Standards

    Naming: Use PascalCase() for functions and camelCase for variables.

    Types: Use only rp_ prefixed types (e.g., rp_u32, rp_fixed) from the SDK to ensure cross-platform portability.

    Physics: Logic must adhere to the fixed Δt "Heartbeat" and support Evolutionary Calibration.
    
⚖️ Error Code Standards ("Zip Codes")

    Kernel Contributions: Use only the -100 to -999 range for internal logic.

    No Hardware Leaks: Do not define any error codes -1000 or below within the Kernel source.

    Pass-through Logic: If your Kernel code interacts with a plugin, it must treat any result ≤−1000 as an opaque "Plugin Implementation" error.

    Documentation: If you create a new Kernel error code (e.g., -105 for a specific Heartbeat sync failure), you must document it in the internal RP_Result registry.

🚀 Submission Process

    Fork and Branch: Create a branch for your feature or fix.

    Self-Diagnose: Ensure your code returns the correct RP_Result "Zip Code" (Kernel range: -100 to -999).

    Documentation: Update Doxygen comments for any new internal functions.

    Pull Request: Submit your PR with a clear description of how it affects the "Heartbeat."
