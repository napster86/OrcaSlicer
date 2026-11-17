# Creality K1C 2025 CFS-C compatibility

## Base version

- OrcaSlicer 2.5.1
- Base commit: eef7710cb102fdb51a9bcdbd9efd61047f44774a
- Printer API model: K1C 2025_CFS-C

## Source code fixes

File: src/slic3r/Utils/CrealityPrint.cpp

- Added K1C 2025_CFS-C to stores_gcode_in_usr_data().
- Added K1C 2025_CFS-C to cfs_capable_models().

These changes enable native recognition and CFS synchronization.

## Monocolor printer profile workaround

The original filament change sequence may request Y245,
which exceeds the Y-axis travel limit on this printer.

Observed firmware error:

    CC5000 - Move out of range

Measured firmware limits:

- X: -7 to 229 mm
- Y: -1.5 to 225 mm
- Z: -5 to 255.5 mm

For the tested monocolor profile:

- Use the existing K1C_CFS-C printer profile as a base.
- Create a separate user printer preset.
- Clear the Change Filament G-code field.
- Preserve the original profile.
- Do not modify firmware movement limits.

Profile setting override:

    "change_filament_gcode": ""

This workaround has not been validated for multicolor printing.

## Hardware validation

- Native printer communication: PASS
- CFS synchronization: PASS
- Filament identification: PASS
- Automatic slot mapping: PASS
- Remote print start: PASS
- Automatic filament loading: PASS
- PLA print using slot 4: PASS
- ABS print using slot 1: PASS
- Monocolor workaround: PASS
- Windows build: PASS
- Custom installer: PASS
- Multicolor printing: NOT TESTED

## Notes

No printer firmware modifications were required.

This is an unofficial community modification.
The original project license remains applicable.
