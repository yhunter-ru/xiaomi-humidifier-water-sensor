# Xiaomi Humidifier water level sensor emulation with Arduino

## Replacing the blue module with Arduino 

1. Disassemble starting from the top cover. You need to get to the power supply where the power cord comes in.
2. Remove the contacts of the water level sensor (just slide out of the case).
3. You have access to the PSU. Remove it and disassemble the black case.
4. Solder the blue module carefully so as not to damage the tracks of the power supply board.
5. Throw the blue module in the trash)
6. Download Arduino IDE. Install. https://www.arduino.cc/en/software
7. Download driver for CH340 if your arduino is Chinese. Install. https://github.com/DecaturMakers/CH340_drivers-Linux-Mac-Windows
8. Download the firmware sketch from the github: https://github.com/yhunter-ru/xiaomi-humidifier-water-sensor
9. Open up the sketch in the Arduino IDE.
10. Connect Arduino to your computer. See in the IDE that a new virtual COM port has appeared in the "Tools -> Port" menu. (If it does not appear, then the CH340 driver is not installed correctly).
11. Choose: "Tools -> Board -> Arduino Nano". "Tools -> Processor -> ATmega328P" (maybe Old Bootloader, you may not have an old one - try it in turn).
12. Choose: "Tools -> Manage Libraries". In the search, enter "CapacitiveSensor". Press "Install".
13. Click the button with the arrow "Download". The board is ready. Can be connected to a humidifier.
14. Solder a 1 MegaOhm resistor between the D2 and D3 pins of the Arduino. Solder the rest of the leads according to the scheme.

![Connection scheme](https://github.com/yhunter-ru/xiaomi-humidifier-water-sensor/raw/master/smartme-humidifier-arduino-connections.png)

**Helpful Hints:** You can cover the power supply board with a glue gun to keep it dry. From the factory, the board is covered with a moisture-proof varnish. Arduino can be packed in a plastic bag and glued inside the humidifier near the drum motor. 

## Sensor calibration (if required)

1. Check the polarity of the sensor connection to the Arduino. The reverse polarity will give higher values.
2. **Important:** Disconnect the Arduino power supply from the humidifier. Do not connect power from the humidifier power supply unit and from USB at the same time - you can burn the board or/and USB. 
3. Keep the sensor connected to the Arduino. Keep the dry sensor in the tank.
4. Line 49 `Serial.write (packet, sizeof (packet));` - comment with two slashes // at the start.
5. Line 50 `Serial.println (readingRaw);` - uncomment at the start.
6. Upload the firmware into Arduino.
7. In Arduino IDE: "Tools -> Port Monitor". Write down average values of the dry sensor.
8. Fill the water tank to the maximum and write down new values.
9. Enter the values of the min and max to lines 9 `MIN_READING` and 10 `MAX_READING`, respectively.
10. Line 49 `Serial.write (packet, sizeof (packet));` - uncomment back.
11. Line 50 `Serial.println (readingRaw);` - comment back.
12. Upload the firmware. Connect the power supply from the PSU. Assemble the humidifier. 

When the water hits certain level it'll short both metal rods making the measurement returns -2. It is expected behaviour.
