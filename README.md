# JoTech BLE Signal Simulator — bench prototype

## Hardware
Arduino Opta WiFi + one AFX00007; regulated 12 V main power. O1+/- active current output 4–20 mA; O2+/- 0–5 V output; P1+ PWM 0–5000 Hz. For PWM, VPWM is an 8–24 VDC supply and `-` its return. Omniplex sensor pin A to VPWM, pin B to PWM `-`, pin C to P1+ is the user's proposed arrangement, **not validated as electrically compatible**. The Omniplex pin C reading 12 V disconnected suggests a pull-up; do not connect P1+ until active PWM compatibility is confirmed. O1 is an ACTIVE source and cannot simulate a passive two-wire loop without external hardware. Bench test with safe loads before connecting Omniplex.

## Arduino
Install Arduino Mbed OS Opta board support, `ArduinoBLE`, and latest `Arduino_Opta_Blueprint` in Arduino IDE. Open JoTech_Opta_BLE.ino and select Arduino Opta WiFi. Expansion should be the first/only expansion. Serial monitor 115200. This code is not compiled/hardware-verified; verify against your installed library and update expansion firmware before testing. It uses official OA_CH_4/OA_CH_7 channel numbers 4/7 and OA_FIRST_PWM_CH for P1.

## iPhone without Mac
Install Bluefy (https://bluefy.app/). Host `index.html` on an HTTPS site (for example GitHub Pages). In Bluefy, open the HTTPS URL and tap Connect BLE; choose JoTech-Simulator. Safari on iPhone does not provide the necessary Web Bluetooth interface. You can host the single HTML file using a Windows PC and GitHub Pages; no Mac or Xcode required. Once loaded, BLE works locally without an internet connection, but loading the hosted page may need internet unless cached.

## BLE protocol
Service UUID a6c00001-7865-4f45-8e70-1e330f520001; writable command UUID a6c00002-7865-4f45-8e70-1e330f520001. Commands: `I,12.5,1`, `V,2.5,1`, `F,1000,1`, `OFF`, `PING`. All outputs disabled at startup and disconnect, or after 5 seconds without valid commands. 0 mA when O1 disabled is an active-output command and not a passive loop mode. Verify actual output with meters/scope.

## Safety
This is a prototype, not a certified calibrator or hazardous-location device. No BLE authentication; do not use for live critical control. Check grounding, voltage/current ratings and load characteristics before attaching the Omniplex. Prefer testing each output into known safe loads first.
