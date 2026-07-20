\# Herbie 2.0



\*\*Herbie 2.0\*\* is an autonomous RFID-based line following robot developed for a state-level robotics competition in Kerala.



Unlike a conventional line follower, Herbie 2.0 can execute different tasks by reading RFID tags placed beneath the track.



Supported tasks include:



\* FOLLOW

\* STOP

\* BOMB

\* DIR:LEFT

\* DIR:RIGHT

\* REVSTART

\* REVEND

\* TONE:TIME:xx

\* TIME:xx



The project focuses on robust embedded system design using an ESP32 microcontroller, digital line sensing, PD control, RFID navigation, OLED feedback and Bluetooth PID tuning.



\---



\# Hardware.md



\## Microcontroller



\### Final Controller



ESP32 DevKit V1 (ESP-WROOM-32)



Reasons:



\* More GPIOs

\* Bluetooth for live PID tuning

\* Fast dual-core processor

\* Good PWM support

\* Better development ecosystem

\* Easy USB programming



\---



\### Originally Planned Controller



STM32F103C8T6 Blue Pill



Reasons for initial selection:



\* 72 MHz ARM Cortex-M3

\* Professional embedded platform

\* Hardware timers

\* Low cost



Reason for switching:



Two days before the competition the STM32 stopped accepting uploads through ST-Link.



Despite repeated debugging:



\* SWD verified

\* Wiring checked

\* Boot configuration checked

\* Multiple PCs tested



the issue could not be resolved in the available time.



The project was migrated to ESP32 to ensure competition participation.



\---



\## Motor Driver



TB6612FNG



Reasons:



\* Efficient MOSFET H-Bridge

\* Low voltage drop

\* Higher efficiency than L298N

\* Suitable for Li-ion powered robots



Originally a DRV8833 was used.



It was accidentally damaged due to reverse battery polarity and replaced with TB6612FNG.



\---



\## Motors



N20 Metal Gear Motors



Reasons:



\* Compact

\* High RPM

\* Lightweight



Lessons learned:



The 2000 RPM version produced insufficient torque on rough competition tracks.



Future versions should prioritize torque over maximum RPM.



\---



\## Line Sensor



RLS-08



Initially used in Analog Mode.



Reasons:



\* Dedicated line follower sensor

\* Eight sensors

\* Adjustable potentiometer for each sensor

\* Individual indicator LEDs



Competition observations:



Although analog mode provided continuous values, it was highly affected by:



\* Ambient lighting

\* Surface reflectivity

\* Uneven track finish



Switching to Digital Mode resulted in:



\* More stable readings

\* Easier PD tuning

\* Smoother line following

\* Better robustness



Future versions will use Digital Mode.



\---



\## RFID



MFRC522



Purpose:



Execute tasks from RFID tags.



Competition format:



Card Type:



MIFARE Classic 1K



Sector:



1



Block:



0 (Absolute Block 4)



Authentication:



Key A



Default key:



FF FF FF FF FF FF



Supported commands include:



FOLLOW



STOP



BOMB



DIR:LEFT



DIR:RIGHT



TIME:10



REVSTART



REVEND



TONE:TIME:10



\---



\## Display



0.96 inch SSD1306 OLED



Purpose:



\* Robot status

\* Current RFID command

\* Debug messages



\---



\## Communication



Bluetooth



Purpose:



Real-time PID tuning



\* Kp

\* Kd

\* Base Speed



No Wi-Fi required.



\---



\# Software.md



The firmware is organized into independent modules.



\* Motor Control

\* Sensor Processing

\* PD Controller

\* RFID Handler

\* OLED Manager

\* Bluetooth Interface

\* Competition Task State Machine



Programming language:



Arduino C++



\---



\# PinMapping.md



\## ESP32 Pin Mapping



| Function   | GPIO                            |

| ---------- | ------------------------------- |

| Sensor 1   | 36                              |

| Sensor 2   | 39                              |

| Sensor 3   | 34                              |

| Sensor 4   | 35                              |

| Sensor 5   | 32                              |

| Sensor 6   | 33                              |

| Sensor 7   | 25                              |

| Sensor 8   | 26                              |

| Left IN1   | 27                              |

| Left IN2   | 14                              |

| Left PWM   | 13                              |

| Right IN1  | 16                              |

| Right IN2  | 17                              |

| Right PWM  | 4                               |

| OLED SDA   | 21                              |

| OLED SCL   | 22                              |

| RC522 SS   | 5                               |

| RC522 SCK  | 18                              |

| RC522 MISO | 19                              |

| RC522 MOSI | 23                              |

| RC522 RST  | 15                              |

| RGB Red    | 2                               |

| RGB Green  | 12                              |

| RGB Blue   | 0                               |

| Buzzer     | \*(update with your final GPIO)\* |



\---



\# Competition.md



Competition Features



\* RFID-based autonomous tasks

\* White line on black surface

\* Sharp turns

\* Loops

\* Junctions

\* Reverse section

\* Timing tasks

\* Music task



Herbie completed most system integration but encountered:



\* Rough competition surface

\* High front caster clearance

\* Low motor torque

\* Time penalty during debugging

\* Incorrect RFID mapping after rushed modifications



\---



\# LessonsLearned.md



\## Hardware



\* Lower caster improves stability.

\* High torque motors are preferable to very high RPM motors.

\* Test on uneven surfaces before competition.



\## Sensors



The biggest lesson of the project.



Initially Analog Mode was selected because of its higher theoretical precision.



However, competition testing showed that Digital Mode was significantly more robust against varying lighting conditions and track reflectivity.



Digital Mode combined with a properly tuned PD controller produced smoother and more reliable behaviour than Analog Mode.



Future versions will therefore adopt Digital sensing.



\## Firmware



\* Freeze competition firmware before the event.

\* Verify every RFID command after any firmware modification.

\* Keep a complete backup of working firmware.



\---



\# Changelog.md



\## Version 1



Arduino Uno



L298N



Digital Sensors



Winner of State Level Line Follower Competition



\---



\## Version 2



STM32



RFID



OLED



PD Controller



RLS-08



Later migrated to ESP32 due to STM32 programming failure.



Adopted Digital sensor mode after competition observations.



\---

