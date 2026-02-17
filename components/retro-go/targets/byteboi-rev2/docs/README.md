# CircuitMess ByteBoi Rev. 2
- Status: completed (build verified)
- Ref: https://circuitmess.com/products/byteboi-2-0
- Ref: https://github.com/CircuitMess/ByteBoi-Firmware
- Ref: https://github.com/CircuitMess/ByteBoi-Library

Button mapping:
- Start: Select + A
- Menu: Select + B
- Option: Select + Up

# Hardware info
- ESP32
- 320x240 TFT path (ST7789/ILI9341-compatible driver path in retro-go)
- microSD storage
- Shift-register based button input on rev2 hardware

# Verification links (source of rev2 mapping)
- Device init and revision switch (`v2_0` + `Pins3`):  
  https://github.com/CircuitMess/ByteBoi-Library/blob/master/src/ByteBoi.cpp
- Rev2 pin definitions (`Pins3`):  
  https://github.com/CircuitMess/ByteBoi-Library/blob/master/src/PinDef.cpp
- Rev2 display panel path (`panel3`, ST7789):  
  https://github.com/CircuitMess/ByteBoi-Library/blob/master/src/ByteBoiDisplay.cpp
- Rev2 shift-register input implementation and bit remap:  
  https://github.com/CircuitMess/ByteBoi-Library/blob/master/src/ByteBoi2Input.cpp  
  https://github.com/CircuitMess/ByteBoi-Library/blob/master/src/ByteBoi2Input.h
- Firmware repo (integration context):  
  https://github.com/CircuitMess/ByteBoi-Firmware

# Notes
- This target intentionally maps `BTN_C` from ByteBoi firmware semantics to `Select` in retro-go to preserve the same Start/Menu virtual combos used by rev1.

# Flash capacity and app selection
- This target is currently configured for **4MB flash** (`components/retro-go/targets/byteboi-rev2/sdkconfig`).
- `.fw` images from SD-card are **not** supported for this target (`FW_FORMAT = "none"` in `env.py`), so use `.img` + USB flashing.
- App set selection is controlled by `rg_tool.py` app arguments:
  - Explicit list: `python rg_tool.py --target byteboi-rev2 build-img <apps...>`
  - `all` uses `DEFAULT_APPS` from `components/retro-go/targets/byteboi-rev2/env.py` (it does **not** mean every app in `PROJECT_APPS`).

## Verified size examples
- Fits (default `all` for this target):
  - `python rg_tool.py --target byteboi-rev2 build-img all`
  - Result: **3.875 MB**
- Fits (example **without DOOM**):
  - `python rg_tool.py --target byteboi-rev2 build-img launcher retro-core gwenesis fmsx`
  - Result: **3.688 MB**
- Does not fit a 4MB device:
  - `python rg_tool.py --target byteboi-rev2 build-img launcher retro-core prboom-go gwenesis fmsx`
  - Result: **4.500 MB** (too large for 4MB flash hardware)

## Flashing selected apps (USB)
- Build + install selected set:
  - `python rg_tool.py --target byteboi-rev2 --port <PORT> install launcher retro-core gwenesis fmsx`
- Or flash generated image manually:
  - `esptool.py write_flash --flash_size detect 0x0 retro-go_<version>_byteboi-rev2.img`

# Images
![device.jpg](device.jpg)
