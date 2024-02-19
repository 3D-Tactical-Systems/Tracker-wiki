# Setup

It is important to configure the telemetry network correctly to ensure the boat landing sequencey is successfull. The telelemetry network consists of 3 nodes, the UAV, the antenna tracker and mission planner ground station. Each node needs a bidirectional connection to each other node. The following sections document the connneciton settings required on each device to ensure a seamless telemetry link. 

## UAV Hardware Connections

The UAV only has one telemetry connection to the flight contrioller on serial 1. This is connected to the S2 ethernet to serial module and then broadcast across the radio network. The TX line of serial 1 is also routed streight to the radio. The UAV hardware connections are shown the figure below. 


Mavproxy is used as a telemetry forwarding tool to ensure each of the 3 nodes are able to communicate with each other. The image below shows the IP conneciton map. 

This is the mavproxy command:

mavproxy --master=udpout:192.168.2.3:20108 --master=udpout:192.168.2.5:23 --out=udpout:192.168.2.5:23 --out=udpout:192.168.2.25:26








## TrackerX Software

The mavproxy forwarding software can be run via the TrackerX software. Once mavproxy is running in the backrgorund the UAV telemetry will be forwared to the tracker and a connection on Mission Planner and be inisiated. 


