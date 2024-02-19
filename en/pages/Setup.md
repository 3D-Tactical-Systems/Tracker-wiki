# Setup


This section provides a comprehensive overview of the telemetry communication network architecture, detailing the essential settings and programs necessary for its operation. Proper configuration of the telemetry network is crucial to guarantee the success of the boat landing sequence. The network is comprised of three key nodes: the UAV, the antenna tracker, and the mission planner ground station. It's imperative that each node maintains a bidirectional connection with the others to facilitate uninterrupted telemetry data exchange. Subsequent sections will meticulously outline the connection settings required for each device, ensuring a robust and seamless telemetry link.

## UAV Hardware Connections


The UAV is equipped with a singular telemetry connection to the flight controller via Serial 1. This connection interfaces with the S2 Ethernet-to-Serial module, facilitating the broadcast of data across the radio network. Additionally, the TX line from Serial 1 is directly routed to the radio. This second unidirection link does not get used in this new configuration.  The hardware connections of the UAV are illustrated in the figure below.


![alt](uploads/images/UAV_Telem_Com.png)


## Ground Station

Once the telemetry data is recieved by the ground station radio the data is passed though a Mavproxy. Mavproxy acts as a routing and forwarding tool to connect both the antenna tracker and the Mission Planner ground station to the UAV. The diagram below shows the data routing from a IP network perspective. 

![alt](uploads/images/IP%20Connection.png)

Mavproxy acheives the routing by configuration with the following start up instruction.

Mavproxy command

mavproxy --master=udpout:192.168.2.3:20108 --master=udpout:192.168.2.5:23 --out=udpout:192.168.2.5:23 --out=udpout:192.168.2.25:26


```javascript
var hello = function () {
    // say hello
    alert('Hello world!');
}
```





## TrackerX Software

The mavproxy forwarding software can be run via the TrackerX software. Once mavproxy is running in the backrgorund the UAV telemetry will be forwared to the tracker and a connection on Mission Planner and be inisiated. 


