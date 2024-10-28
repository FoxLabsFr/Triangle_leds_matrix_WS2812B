# Triangle LED Matrix with 144 WS2812B-B/W LEDs

Documentation and assets for the 133mm triangle LED matrix featuring 144 WS2812B-B/W LEDs arranged in a triangular pattern.

[![Tindie](https://img.shields.io/badge/Tindie-Product%20Page-orange?style=for-the-badge&logo=tindie)](https://www.tindie.com/products/37169/)

<img src="assets/triangle_leds_matrix_pic.jpg" alt="Triangle LED Matrix" width="600">

## 📋 Specifications

- **Size:** 133mm triangle
- **LED Type:** WS2812B-B/W
- **Total LEDs:** 144
- **Operating Voltage:** 5V DC
- **Current Consumption:** ~60mA per LED at full brightness (~8.64A total max)
- **Data Protocol:** Single-wire serial interface (WS2812 protocol)
- **PCB Thickness:** 1.6mm
- **Mounting Holes:** 3x M3 screw holes at the corners of the triangle
- **Connector Type:** 3-pin JST HX connector OR soldering pads, for power and data (IN and OUT)

## 🔌 Pin Configuration & Wiring

### IN Connector

| Pin | Function | Description          |
| --- | -------- | -------------------- |
| IN  | Data     | Data input signal    |
| 5V  | Power    | Power supply (5V DC) |
| GND | Ground   | Ground connection    |

### OUT Connector

| Pin | Function | Description                                  |
| --- | -------- | -------------------------------------------- |
| OUT | Data     | Data output (for chaining multiple matrices) |
| 5V  | Power    | Power supply (5V DC)                         |
| GND | Ground   | Ground connection                            |

### Wiring Diagram

<img src="assets/SchematicNanoTriangle.jpg" alt="Triangle LED Matrix Wiring Diagram" width="600">

## 🔢 LED Ordering

For programming patterns and animations, refer to the diagram below to understand the LED ordering within the matrix.

<img src="assets/triangle_led_matrix_id_order_diagram.jpg" alt="Triangle LED Matrix ID Diagram" width="600">

## 🔄 Conversion Matrix

This matrix is useful for converting 2D images stored in a standard square format to the specific layout of the LED matrix. It maps each LED's position in the matrix to its corresponding image pixel. Entries with a value of `-1` indicate positions that do not correspond to an actual LED and should be ignored.

```cpp
const short convertMat[16][16] = {
  { -1, -1, -1, -1, -1, -1, -1,  0,  1, -1, -1, -1, -1, -1, -1, -1},
  { -1, -1, -1, -1, -1, -1, -1,  2,  3, -1, -1, -1, -1, -1, -1, -1},
  { -1, -1, -1, -1, -1, -1,  4,  5,  6,  7, -1, -1, -1, -1, -1, -1},
  { -1, -1, -1, -1, -1, -1,  8,  9, 10, 11, -1, -1, -1, -1, -1, -1},
  { -1, -1, -1, -1, -1, 12, 13, 14, 15, 16, 17, -1, -1, -1, -1, -1},
  { -1, -1, -1, -1, -1, 18, 19, 20, 21, 22, 23, -1, -1, -1, -1, -1},
  { -1, -1, -1, -1, 24, 25, 26, 27, 28, 29, 30, 31, -1, -1, -1, -1},
  { -1, -1, -1, -1, 32, 33, 34, 35, 36, 37, 38, 39, -1, -1, -1, -1},
  { -1, -1, -1, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, -1, -1, -1},
  { -1, -1, -1, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, -1, -1, -1},
  { -1, -1, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, -1, -1},
  { -1, -1, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, -1, -1},
  { -1, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 98, -1},
  { -1, 99,100,101,102,103,104,105,106,107,108,109,110,111,112, -1},
  {113,114,115,116,117,118,119,120,121,122,123,124,125,126,127,128},
  {129,130,131,132,133,134,135,136,137,138,139,140,141,142,143,144}
};
```

## 💻 Example Code

```cpp
#include <Adafruit_NeoPixel.h>

#define PIN            6  // Data pin connected to DIN of the LED matrix
#define NUMPIXELS      144 // Number of LEDs in the matrix

Adafruit_NeoPixel pixels(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

void setup() {
  pixels.begin(); // Initialize the NeoPixel library.
}

void loop() {
  for (int i = 0; i < NUMPIXELS; i++) {
    pixels.setPixelColor(i, pixels.Color(255, 0, 0)); // Set all LEDs to red
    pixels.show(); // Update the LED matrix
    delay(50);
  }
}
```

## 📁 Assets

- **WS2812B Datasheet:** [View Datasheet](https://cdn-shop.adafruit.com/datasheets/WS2812B.pdf)
- **Footprint:** [DXF file](./assets/triangle_leds_matrix_133mm_WS2812B.DXF) for the PCB layout and screw holes
- **3D Model:** [STEP file](./assets/triangle_leds_matrix_133mm_WS2812B.STEP) for the PCB layout and screw holes

## ⚠️ Important Considerations

- **Power Supply:** Verify that your power supply can support the total current required by the LEDs. The JST HX connectors are rated up to 3A. If you plan to use more (for example, setting the LEDs to full brightness), use the solder pads instead, with appropriately sized AWG wires.
- **LED Protection:** WS2812B require protection against voltage spikes and excessive current. [Protection Module](https://www.tindie.com/products/27407/)
- **Heat Dissipation:** Depending on your usage, active cooling may be necessary to prevent overheating.
- **Data Integrity:** To prevent signal degradation, especially in long LED chains, keep data lines as short as possible.

---

Built with ❤️ by FoxLabs

This README was generated with AI assistance.
