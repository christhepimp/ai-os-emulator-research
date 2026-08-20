# Rooted Android Emulator Notes

## Key Tools

### AERoot (Recommended for Google Play AVDs)
- Repo: https://github.com/quarkslab/AERoot
- Allows on-the-fly root privileges to any process on Google Play flavor AVDs.
- Uses GDB attached to QEMU stub (`emulator ... -qemu -s`).
- Supports recent Android versions (API > 27) and multiple kernels.
- Modes: pid, name, daemon (root adbd so all new shells are root).

Installation:
```bash
pip install aeroot
# or from source
git clone https://github.com/quarkslab/AERoot.git
cd AERoot && python3 setup.py install --user
```

Usage outline:
1. Start emulator with GDB stub: `emulator @Your_AVD -qemu -s`
2. Run aeroot in desired mode.

### Magisk-based rooting (rootAVD and similar)
- More permanent root for development AVDs.
- Allows Magisk modules, Zygisk, etc.
- Common for security research and custom ROMs on emulator.

### android_emuroot (older, related to AERoot)
- https://github.com/airbus-seclab/android_emuroot
- Predecessor concepts.

## Custom Kernels

Android emulator uses the Goldfish / Ranchu virtual hardware + Android common kernel.

Sources:
- https://android.googlesource.com/kernel/common
- https://android.googlesource.com/kernel/goldfish (older)

Building custom kernels for the emulator is supported and useful for instrumentation, new syscalls, or experimental features.

## Practical First Experiment Ideas

1. Fully automated script that launches a rooted AVD and drops into a root shell.
2. From root, inspect kernel version, modules, process list, and memory layout.
3. Run a simple Python/Go agent with root privileges that monitors system state and makes basic decisions (e.g. kill high-CPU processes based on a policy).
4. Later: feed system telemetry to a local LLM and have it propose actions.
