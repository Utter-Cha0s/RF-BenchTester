Utter-Cha0s read me edit THANK YOU

# <center>📡 Duggie China Stuff Dual-Band RF Diagnostic Testing Tool 📡</center>
## <center> Overview </center>

The Duggie China Stuff Dual-Band RF Diagnostic Testing Tool is a portable RF diagnostic tool built on the ESP32 platform.
It allows you to test and analyze cheap and mass production NRF24L01 (2.4 GHz) and CC1101 (300-928 MHz) modules.

🎯 Designed to perform:
- SPI verification
- RF spectrum activity scans
- TX validation
- Keyfob/Remote detection mode
- Live bar-graph visualization of signal activity

🧪 Intended Use Cases:
- Verifying questionable AliExpress modules
- Checking if a radio is truly functional
- Detecting keyfob transmitters
- Quick RF environment inspection
- Bench testing before final integration

## <center>🖥️ Parts List </center>
- Breadboard or a Blank PCB
- ESP32-32U
- 3 Momentary Buttons (NRF24L01 | Reset | CC1101) 
- 2 2x4 Female Headers
- SSD1306 - 0.96" 128x64 OLED Screen

## <center>📌 Primary Pinout Tables </center>
#### Shared Pins
|  SPI  |  Pin  |
| :---: | :---: |
|  SCK  |   18  |
| MISO  |   19  |
| MOSI  |   23  |

#### OLED Screen
|  LCD  |  Pin  |
| :---: | :---: |
|  SCK  |   22  |
|  SDA  |   21  |
|  VCC  |  3.3  |
|  GND  |  GND  |

#### Momentary Buttons
| Function |  Button  |  Pin  |
| :---:    |  :---:   | :---: |
| NRF24L01 |  BTN_NRF |	  32  |
|  CC1101  |  BTN_CC  |	  33  |
|  Reset   |  BTN_RST |	  25  |

## <center>🖥 Hardware Overview </center>
📺 **OLED Display (128x64 I2C)**
- Resolution: 128x64
- Interface: I2C (0x3C)
- Displays:
    - Boot logo
    - Scan graphs
    - Test results
    - Detection notifications

|  SPI  |  Pin  |
| :---: | :---: |
|  SDA  |   21  |
|  SLC  |   22  |

📡 **NRF24L01 (2.4GHz Module)**
- Capabilities:
    - SPI verification
    - Register R/W validation
    - Full 126-channel 2.4GHz sweep
    - RPD (Received Power Detector) sampling
    - Activity graph rendering
    - TX payload test

|  SPI  |  Pin  |
| :---: | :---: |
|  CE   |   4   |
|  CNS  |   5   |
|  SCK  |   18  |
|  MISO |   19  |
|  MOSI |   23  |

📻 **CC1101 (Sub-GHz Module)**
- Scannable Bands:
    - 300–350 MHz
    - 390–500 MHz
    - 850–928 MHz

- Capabilities:
    - RSSI sampling
    - Noise floor comparison
    - Peak frequency detection
    - Bar graph visualization
    - Keyfob detection mode (315 MHz / 433.92 MHz)

|  SPI  |  Pin  |
| :---: | :---: |
|  CS   |   17  |
|  SCK  |   18  |
|  MISO |   19  |
|  MOSI |   23  |

## <center>⚡ Functionality </center>

***<center>All buttons use INPUT_PULLUP (active LOW).</center>***

📡 **NRF24 Test Process**
- Stage 1 – SPI & Register Validation
    - radio.begin() check
    - isChipConnected() verification
    - Channel write/read validation
- Stage 2 – 2.4GHz Spectrum Sweep
    - Scans all 126 channels
    - 50 sweep cycles
    - Uses testRPD() for activity detection
    - Counts active channels
    - Displays peak channel + activity graph
    - Bar graph visualizes RF density across channels.
- Stage 3 – TX Test
    - Sends test payload DE AD BE EF 42
    - Validates write attempt
    - Reports PASS / FAIL
    - Final Result Screen
>== NRF24 RESULT ==<br>
>   SPI: PASS<br>
>   RX: PASS / WEAK<br>
>   TX: PASS / FAIL

📻 **CC1101 Test Process**
- Stage 1 – SPI Validation
    - getCC1101() check
    - Version register validation
- Stage 2 – Sub-GHz Spectrum Scan
    - Iterates through predefined frequency list
    - Captures peak RSSI per frequency
    - Calculates noise floor
    - Displays bar graph across spectrum
>= Example Output =<br>
>Pk:433.92MHz -51dBm
- Stage 3 – Keyfob Detection Mode
    - Listens specifically on:
        - 315.00 MHz
        - 433.92 MHz
    - Procedure:
        - Establish baseline RSSI
        - Monitor for spike > +15dB above baseline
        - Trigger detection if RSSI > -60 dBm
> = Detection Output =<br>
>KEYFOB DETECTED!<br>
>433.92MHz -48dBm


<br><br>
**Testing Timeout:** 10 seconds


## <center>Credits and Contributions</center>
Duggie - Original designer<br><br>
Utter-Cha0s - Page editor and schematic contributor

*Based on the absoute need to check Aliexpress stuff before you spend an Hour soldering it.*

**GitHub: https://github.com/duggie162-cpu?tab=following**
