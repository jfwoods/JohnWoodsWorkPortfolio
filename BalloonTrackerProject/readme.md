# Balloon Tracking Research Project

## The Basics
This project began back in April 2023, when I was a student in Dr. Ridley's Engineering 100 - Weather Balloons class at UMich. We spent the semester designing and building custom circuit boards to act as a weather balloon payload with various sensors, a microcontroller, GPS, and SD card module to record the data.

Come launch time, and the balloons launch! Only to lose communication with the tracking system. The next couple days were a little hectic, as we had no idea where our payloads had gone. We knew this was a possibility, but it saddened the class nontheless. Fortuneately, both balloons launched had crashed into fields in southeast Michigan, and were recovered by the landowners and returned to us. This was when work on the next-gen tracking system began.

(Skip ahead to the [design page](./design+photos.md) for design pictures and thoughts, otherwise keep reading for high-level requirements & system architecture.)

---

## Design Goals
When we first sat down to begin planning, we came up with these goals:
- Custom design with documentation
- Use redundant methods of communication
- Use a microcontroller board (i.e. Arduino, Teensy, RP2040, etc.) as the brains
- 3+ hour battery life in cold conditions
- Ideally record all GPS data for post-flight analysis
- Light, reliable, and rugged (all simple requirements for a project like this)

---

## System Architecture
With those goals in mind, we came up with this plan:
1. Use an Arduino Nano Every as the main 'brains' of the project. These are easily accessible SBCs [^1] that would make maintence and replication of this project much simpler. We thought about soldering a processor to each tracker, like an ATmega 2560 or ATmega 328p, but decided against it for the reasons I listed.
2. Use the DRA818V HAM radio module as the primary communication device. I would design a board around this module, and Eric would write the software to make it do what we needed. 
3. Use an Iridium satellite modem as the secondary communication method. We liked the RockBlock 9603, and the university had a couple of them for us to test with. Great little devices. 
4. Instead of using a [GPS breakout board](https://www.adafruit.com/product/746?gclid=Cj0KCQjwgNanBhDUARIsAAeIcAtAeNtzSEiQcC9UHOvohR2_PsaDv65w-8E68LjxnSKLT4-7cJbT-toaAkXZEALw_wcB) like the students in the class did on their payloads, we were going to integrate a GPS IC onto the board. We chose the uBlox MAX-M10-S, a great high-performance GPS chip with fantastic documentation. 
5. Include a temperature sensor and battery voltage measurement to transmit along with the location data. Useful for making sure the battery is okay and the board isn't going to freeze. 
6. Include LoRa functionality with this [breakout board](https://www.adafruit.com/product/3072) so that potential communication with student payloads is possible, if the students include one of these modules on their board as well. 

---

## Design

With that out of the way, it was time to start drawing schematics and laying traces! Head to the [design page](./design+photos.md) for more on that.

[^1]: Single Board Computer
