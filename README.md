# Patient-Support-Platform for Protocol Validation

The assignment is inspired by medical scanning machines developed at Philips Medical
Systems. A novel system at Philips is a Movable Patient Support Platform, MPSP for short,
which is a trolley bed on which a patient can lie inside a scanner.

## Specifications
![](https://github.com/shrutirao94/Patient-Support-Platform/blob/master/images/pss.png)
The MPSP can be either disconnected from the scanner or docked, i.e. connected to the
scanner. There are two motors in the MPSP. Motor M1 controls the vertical and motor M2
controls the horizontal movement. Both motors have brakes that can be turned on and off
separately from the motors. Horizontal movement is only allowed when
the MPSP is docked. When the MPSP is disconnected from the scanner, the bed must
always be in the rightmost position (which is detected by a detector), as otherwise the
MPSP might tumble over. When disconnected from the scanner, the horizontal brake must
always be applied. The vertical brake must always be applied while the vertical motor is
off. When a motor is on, the corresponding brake must not be used, as otherwise the motor
could overheat.


The movements are controlled via a console on the MPSP, which is designed to be as
simple as possible:
![](https://github.com/shrutirao94/Patient-Support-Platform/blob/master/images/console.png)
The stop button puts the MPSP in emergency mode. In emergency mode, the horizontal
brake must be released, to allow medical staff to manually drag the patient outside the
scanner. This may be useful when an emergency occurs (a heart-attack while scanning), or
when a system malfunction happens. The resume button puts the MPSP back to normal
operating mode.The undock button can be used to disconnect the MPSP from the scanning device. When
the undock button is pressed a message is sent to the scanner which will undock the MPSP.
For this a gentle spring mechanism is used that pushes the MPSP away from the scanner.
The undock message should never be sent to the scanner if the bed is not in the rightmost
position, as otherwise the MPSP might tumble over.

The reset button is used for calibration. Every scanner can have a different height,
generally dependent on how it is installed in the hospital. The MPSP can only be moved
inside the scanner if scanner and bed are at the same height, which is called the standard
height. Before use, the MPSP must be calibrated by setting the standard height. This is
done as follows. The MPSP is docked. This is detected via a sensor in the docking unit D.
Then using the up and down buttons the bed is moved to the correct height. By pressing
the reset button once, this height is set to be the standard height. If the reset button is
pressed while the MPSP is not docked, the standard height is forgotten and the MPSP goes
into uncalibrated mode.

When the MPSP is docked and calibrated, the bed will halt when it has reached the
standard height. If the up button is pressed at the standard height, the MPSP moves into
the scanner. In order to avoid unexpected movements it is important that the up button is
released before the inward movement is commenced. This means that releasing the up and
down buttons are important interface actions also.
When the MPSP is docked and calibrated and the down button is pressed, the bed moves
outward, until an outward horizontal detector indicates that the bed is completely outside
the scanner. By releasing and pressing the down button again the bed will subsequently
move downwards. While the MPSP is docked and calibrated, the bed cannot be moved
above the standard height. When the MPSP is disconnected or uncalibrated, the up and
down buttons can only be used to move the bed up and down. The bed is not allowed to
move above some uppermost and below some lowermost position. There are two detectors,
to detect when the bed is in the uppermost or lowermost position.

![](https://github.com/shrutirao94/Patient-Support-Platform/blob/master/images/system-architecture.png)

Three controllers are created: Console, Hardware and Sensor that manage communications between each other. 
