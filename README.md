led-sensor-display


Display the data output of the sensor block or pulse block on a seven-segment LED display, as seen on the balena IoT Happy Hour #47

![image](https://github.com/user-attachments/assets/cf582cfe-bf0e-42c1-8c3e-007f135c41c7)


Overview
This project uses an I2C four digit LED display such as this one from Adafruit. (They are available in other colors as well!) Our example uses the Raspberry Pi 3A but any Pi should work. You can add a button to GPIO16 (pin 36) to toggle through the data fields being displayed. You can also set the device variable DISPLAY_INDEX to the index of the data field (starting with 0) you want as a default value displayed on startup. (This is useful if you don't add a button and don't want the first value displayed.) In our example, we also wired a button to GPIO20 to reset the counter in the pulse block.

Usage
Connect the display to the pi as outlined here. Then include this repo in your project and add this to your existing docker-compose file:

  counter:
    build: ./counter
    restart: always
    privileged: true
(Assuming you placed these files in a folder named "counter".)

The Display
Every time you click the display button, the two leftmost digits will temporarily display the index number of the data along with a colon. It will then display that data. It can display alphabetical characters a - f (the hex letters) but any others will show as blank. If a value exceeds the display capacity of 9999, it will switch to displaying the number in thousands. In that case, an "E" will be displayed for the first digit. For example, the value 147,616 will be displayed as "E147" and the value 12,611 would be displayed "E12.6".
