requirements: 
- needs to have a state machine:
	- on-state change (both entry and exit) behavior handling
	- during-state running
- needs to handle communication
	- MVP over CAN
- importable as a platform.io library
- CAN dbc wrapping / code gen built in 
- smart logging
	- easy logging enable / disable 
	- print line logging 
	- CAN logging
	- storage logging (eg: SD card logging)
- also contains generic system design 
	- such as every system can have actuators / a drivetrain that carry out those inputs
	- every system can have control inputs / controllers
	- every system can have stuff that doesnt fit either of those categories
- needs a way to structure muxing of different inputs

current idea:
- we could have a library that works around using lambda functions that get registered as callbacks that get used 
	- we would need to have different types of functions, ones that can change the state and ones that get run during specific states
- use abstract classes for the generic system components
	- certain callbacks can be marked as handling inputs / actuators

