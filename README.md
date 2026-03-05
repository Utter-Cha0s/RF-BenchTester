📡 Duggie China Stuff Tester
Dual-Band RF Diagnostic Tool (NRF24L01 + CC1101)
🧠 Overview

The Duggie China Stuff Tester is a portable RF diagnostic tool built on an ESP32 platform.
It allows you to test and analyze:

PARTS LIST
esp32 U
3 buttons 
some headers and some wire 

🔹 2.4GHz band using an nRF24L01
🔹 Sub-GHz bands (300–928 MHz) using a CC1101
🔹 Visual output via a 128x64 OLED powered by SSD1306

This tool performs:
SPI verification
RF spectrum activity scans
TX validation
Keyfob / remote detection mode
Live bar-graph visualization of signal activity

  SPI PINS
SCK  = 18
MISO = 19
MOSI = 23
  LCD PINS
SCK = 22
SDA = 21
VCC = 3.3
GND = GND
  BUTTON PINS
BTN_NRF	32
BTN_CC	33
BTN_RST	25

🖥 Hardware Overview
📺 OLED Display (128x64 I2C)
  Resolution: 128x64
  Interface: I2C (0x3C)
  SDA: GPIO 21
  SCL: GPIO 22
  Displays:
  Boot logo
  Scan graphs
  Test results
  Detection notifications

📡 NRF24L01 (2.4GHz Module)
  CE → GPIO 4
  CSN → GPIO 5
  SCK → GPIO 18
  MISO → GPIO 19
  MOSI → GPIO 23

Capabilities:
  SPI verification
  Register R/W validation
  Full 126-channel 2.4GHz sweep
  RPD (Received Power Detector) sampling
  Activity graph rendering
  TX payload test

📻 CC1101 (Sub-GHz Module)
  CS → GPIO 17
  SCK → GPIO 18
  MISO → GPIO 19
  MOSI → GPIO 23

Scan Bands Include:
  300–350 MHz
  390–500 MHz
  850–928 MHz

Includes:
  RSSI sampling
  Noise floor comparison
  Peak frequency detection
  Bar graph visualization
  Keyfob detection mode (315 MHz / 433.92 MHz)

🎛 Button Controls
  Button	GPIO	Function
  BTN_NRF	32	Run NRF24 Test
  BTN_CC	33	Run CC1101 Test
  BTN_RST	25	Restart ESP32

All buttons use INPUT_PULLUP (active LOW).

🔬 NRF24 TEST PROCESS
Stage 1 – SPI & Register Validation
  radio.begin() check
  isChipConnected() verification
  Channel write/read validation
Stage 2 – 2.4GHz Spectrum Sweep
  Scans all 126 channels
  50 sweep cycles
  Uses testRPD() for activity detection
  Counts active channels
  Displays peak channel + activity graph
  Bar graph visualizes RF density across channels.
Stage 3 – TX Test
  Sends test payload DE AD BE EF 42
  Validates write attempt
  Reports PASS / FAIL
  Final Result Screen
              == NRF24 RESULT ==
                  SPI: PASS
              RX: PASS / WEAK
              TX: PASS / FAIL

📡 CC1101 TEST PROCESS
Stage 1 – SPI Validation
  getCC1101() check
  Version register validation
Stage 2 – Sub-GHz Spectrum Scan
  Iterates through predefined frequency list
  Captures peak RSSI per frequency
  Calculates noise floor
  Displays bar graph across spectrum
             = Example Output =
            Pk:433.92MHz -51dBm
Stage 3 – Keyfob Detection Mode
  Listens specifically on:
  315.00 MHz
  433.92 MHz
  Procedure:
  Establish baseline RSSI
  Monitor for spike > +15dB above baseline
  Trigger detection if RSSI > -60 dBm
               = Detection Output =
                KEYFOB DETECTED!
                433.92MHz -48dBm

Timeout: 10 seconds


🧪 Intended Use Cases
Verifying questionable AliExpress modules
Checking if a radio is truly functional
Detecting keyfob transmitters
Quick RF environment inspection
Bench testing before final integration

Duggie Tech

Credits
Duggie 
Based on the absoute need to check Aliexpress stuff before you spend an Hour soldering it im
GitHub: https://github.com/duggie162-cpu?tab=following


