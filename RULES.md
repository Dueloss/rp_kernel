Red Plasma Engine: The Modular Constitution
1. The Error Mandate (The "Zip Codes")

Every function that performs an operation must return an RP_Result enum. Data is passed via out-pointers. This ensures the engine is self-diagnosing across all hardware.

    0 (SUCCESS): Operation completed normally.

    −1 to −99 (OS/Hardware): Critical system failures (e.g., Memory, File I/O).

    −100 to −999 (Kernel): Engine core logic errors (e.g., Heartbeat sync, Plugin loading).

    −1000 and below (Plugin Implementation): Hardware-specific errors (e.g., Vulkan Swapchain, 16-bit Bus).

        Kernel Blindness: These codes are strictly defined and implemented by the plugins themselves.

        Pass-through: The Kernel must treat this range as a "Black Box" and only report the numeric value without internal knowledge of its meaning.

2. Architecture & Sandboxing

    The Kernel is Blind: The Kernel must never include headers from a specific plugin (e.g., no vulkan.h in the Kernel).

    Plugin Isolation: Each plugin lives in its own folder under build/plugins/.

    The Passport: Every plugin must have a manifest file defining its entry point and version.

    Write Access: Plugins may only write data to their own subfolder.

3. The Learning Heartbeat

    Fixed Physics: Physics and logic must run at a fixed Δt.

    Evolutionary Calibration: The engine must measure its "Slack Time" and average it across sessions.

    Persistence: The calculated optimal Hz must be saved to rp_engine.cfg on exit and loaded on startup.

4. Coding Standard (Lean & Blown)

    Naming: PascalCase() for functions, camelCase for variables.

    Types: Always use the rp_ prefix types from the SDK (e.g., rp_u32, rp_fixed).

    Memory: No raw new/delete in the Kernel loop; use the engine's memory management to prevent fragmentation on low-RAM systems.
