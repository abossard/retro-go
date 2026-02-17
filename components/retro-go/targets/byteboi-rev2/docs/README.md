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

# Images
![device.jpg](device.jpg)
