# CarMonitor
An Arduino project for logging pre-OBD car vitals (timestamp, batt voltage, air temp, coolant temp, &amp; HAL sensor for RPM) to an SD card for review later on PC. Can also be used for realtime monitoring. Tested with Arduino Duemilanove and Uno.

<img src="https://github.com/neogeek83/CarMonitor/blob/master/docs/wiring%20harness/20161107_201841_HDR.jpg?raw=true" />

##Dependencies
### Hardware
  * Arduino Duemilanove or Uno (others probably work, but have tested these 2)
  * SDCard /w RTC shield
  * Sensors (various supported, most car sensors are resistive, will just need to re-calebrate if different from ones listed below and in docs/)
### Software
  * Arduino Libraries
    * RTCLib
    * SD (built-in now I think)
    * Wire (built-in now I think)

##Project Sketches
 * CarMonitor - Brings all the below projects together
   
##Supporting Sketches
 * ImpedanceTester - Code specific to create an Ohm Meter
 * SDWriter - Project for bringing up the SDCard writer. This expects an SDcard writter /w RTC (set the clock using the below project prior to using this one)
 * SetSDCardRTCTime - Set the time for the SDCard writer uses SDcard read/write shield /w RTC (something like these: http://www.ebay.com/sch/i.html?_from=R40&_trksid=p2055845.m570.l1313.TR0.TRC0.H0.Xsdcard+arduino+rtc.TRS0&_nkw=sdcard+arduino+rtc&_sacat=0)

###Sensors( see also docs/Sensor Readings.xlsx)

  * new HAL sensor details: 
  ** On device 3144 601
  ** Specs: http://www.elecrow.com/download/A3141-2-3-4-Datasheet.pdf
  ** PINs: (1 is left when looking at printed letters). Pin 1 = Vcc, 2 = GND, 3=output

Diesel Truck Coolant sensor - FZAF-12A648-A4
 * ~65 degrees => 31 K Ohms
 * finger warming, ~85-90degrees =>28kOhms

BMW External Air Temperature Sensor  - Yellow base - (part #1 383 204)
 * 3.5kohms ~65degrees 

BMW External black air sensor
 3066.1 @ 98.5f
 7355.93 @ 61.5f
 5260 @ 75f

###WIRING
  * https://goo.gl/photos/Le24ZwGX4rxnEHM88 
  * Harness #1 (Pin 1 on breadboard is closest to Arduino):
    *  1 blue - intake temperature
	*  2 b /w - intake temp (-)
	*  3 orange - coil voltage
	*  4 o /w   - coil voltage (-)
	*  5 brown - 12V system
	*  6 b / w - 12V system (-)
	*  7 green - coolant temperature sensor
	*  8 g / w - coolant temperature sensor (-)

  * Harness #2 (Pin 1 on breadboard is FARTHEST to Arduino --thk we fixed, need to confirm):
    *  1 blue - not in use
	*  2 b /w - not in use
	*  3 orange - not in use
	*  4 o /w   - not in use
	*  5 brown - HALL GND 
	*  6 b / w - HALL 5Vcc
	*  7 green - HALL Sensor (pulls to GND when magnet S pole is detected)
	*  8 g / w - not in use
	
  * Arduino Pins:
    * A0 - Air Sensor (Black) (10k)
	* A1 - ~ (10.3k)
	* A2 - ~ (10.1k)
	* A3 - Voltmeter (32.7k)
	* A4 - Air Sensor (Yellow) (10.02k)
	* A5 - Water Sensor (10k)
	* D2 - hall effect sensor

###TODO

  * Recalibrate Intake Air Temp(pin 1 and 2) 
  * pretty up arduino code
  * take pictures of setup and add to this readme
  * Create 'event' button to board and in software
  * Add H20 temp sensor(current one isn't going to work due to 12v power being sent to it)
  * Calibrate water sensor
  * Add a MAP sensor to system
  * Add Coil Voltage Sensor
