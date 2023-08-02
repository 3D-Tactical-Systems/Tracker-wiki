# Boat Landing

The 3D Tactical System tracker is designed to be used in harsh and demanding enviroments. Besides its rugged build it has functionality that allows it to be used on a moving or floating platforms. There are two challanges that need need to adress when conducting a flight mission from a moving plaftom:

* The home(RTL location) needs to be updated according to the position of the ground control station or platfrom. This will ensure the UAV is alway able to return home and land succesfull without any pilot aid. 
* The UAV needs to be able take off, approach and land on a platfrom with very limited space, superstructure and other obsticals. 

> **Note** 
The Boat Landing functionality is suported for Quad-Plane UAV's only

# Equipment Setup

In adition to the standard [Setup](https://) the following should be considered:

* The base of the antenna tracker should point towards the front of the moving platform. Carefull note of the orentation and position should be taken before flight. Image 
* The *Home Locaiton* is fixed relative to the position and orentation of the antenna tracker. This means that if the antenna tracker is rotated by 15 deg the *Home location* will move in proportion.
* If the base of the antenna tracker is disturbed during a flight it should be returned to its original position and orientation before an RTL mode is activated.
* the orentation of the antenna tracker does not effect its tracking accuracy.


![alt](uploads/images/Tracker_Side_front.png) 
![alt](uploads/images/truck.jpeg  "Truck")

## Enabling Scipting on the Flight Controller

An additional script will need to be added to the flight controller to enable the boat landing functionality. By default the flight controler has scripting disabled. The following parameters will need to be changed:



|    Parameter       | Value            | Description                                           |
| -------------      |:-------------    | :-----                                                |
| SCR_ENABLE         | 1                | Enable Lua sripting on the flight controller          |
| SCR_HEAP_SIZE      | 100000           | Provide enough memory to allow the script to run      |


Ensure the parameters are saved and writen to the flight controller

![alt](uploads/images/SCR_Params.png "SCR_Params")

Dowload the ship landing script from [here](uploads/documents/plane_ship_landing.lua) and upload it to the scripts file on the SD card of the flight controller. The MAVFtp for the file transfer. The flight controller. The flight controller will need a reboot to run the script. 

![Alt text](uploads/images/MAVfp.png "MAVftp")






To ensure the script is active check the *messages* tab for the following messages:

|    Message       | Description                                                         |
| -------------      | :-----                                                            |
|    PreArm: Ship: no beacon    |  The UAV has lost connection with the antenna tracker. The UAV will not arm.  |
| Have beacon     |  Esstablished connection to the antenna tracker      |



# Ship Landing Function

The Ship landing script only effects the *AUTO*, *RTL* and *Q_RTL* flight modes. There is no behaviour change applied to *QLOITER*, *QHOVER*, *FBWA*, *FBWB*, *CRUISE* ex.

## Take-Off
During an *Auto* take-off, while in Quadmode, the  UAV will match the velocity of the moving base until the transition altitude.


> **Note** the transition altitude is set using **Q_RTL_ALT**

This feature provides the following functionality and advantages:
•	The home location is fixed relative the moving platform (antenna tracker). This means that when the location of the moving platform moves the home location will be updated. 
•	The position of the home location relative to the antenna tracker can be set automatically. 
•	During an “Auto” V-TOL take off the UAV will maintain a forward velocity matching the velocity of the moving platform (ship) until the transition altitude. This is to ensure a clear assent path of the UAV until it is well away from any obstacles or platform superstructure. 
•	When RTL is activated, the UAV will begin its return to the location of the GCS not to the location of its initial take off position.
•	Upon approach to the moving platform in RTL mode the UAV will navigate its auto landing following a three- phase behaviour.
The three-phase approach is described below:

o	Hold off Position – After RTL is initiated the UAV will return to the home location. On approach. The UAV will loiter in close proximity to the moving platform at an altitude set by  ALT_HOLD_RTL. If an RC connection is established. It will maintain its proximity to the moving platform until the pilot initiates the start of the landing procedure. Otherwise, it will automatically transition to the Platform approach phase. The distance the UAV loiters around the ship is dependent on the RTL_RADIUS parameter. 

o	Platform Approach –The UAV will loiter decent to the Q_RTL_ALT altitude. It will approach the moving platform from the SHIP_LAND_ANGLE. 


o	 Q-Land -  Once the UAV has reached the Q_RTL_ALT it will transition to Q-RTL and begin the final decent. It will match the forward velocity of the moving platform and land at the home location. 



Integer posuere erat a ante venenatis dapibus posuere velit aliquet. Vestibulum id ligula porta felis euismod semper. Integer posuere erat a ante venenatis dapibus posuere velit aliquet. Nullam quis risus eget urna mollis ornare vel eu leo. Donec sed odio dui.

Cras justo odio, dapibus ac facilisis in, egestas eget quam. Nullam id dolor id nibh ultricies vehicula ut id elit. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Nulla vitae elit libero, a pharetra augue. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras justo odio, dapibus ac facilisis in, egestas eget quam.


# Flight Plan 

Bellow shows an example of a test flight mission

![alt](uploads/images/Mission_Plan.png)