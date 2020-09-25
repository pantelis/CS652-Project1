# Google/Facebook DCN Approaches

Both Google and Facebook found themseves in a position where an ever-expanding datacenter footprint required moving from conventional legacy network architectures to Clos architectures. The main goal both companies aimed for was an easily-extensible newtork fabric allowing for high bandwidth both internally and externally with a 1P+ bisection bandwidth. 

## Designing the Network

Derivations of the fat tree topology are the name of the game, with each compnay taking a different approach to designing the network.

| Company  | Hierarchy | 
|---|---|
| Google  | Server -> ToR -> Middle Block/Aggregation Block -> Spine Block  |  
| Facebook | Server -> ToR -> Server Pod -> Spine Plane  |  

Google's approach involves taking 32 ToR switches and assigning each 2x10G links to 8 so-called "Middle Blocks". These 8 MBs (grouped into an "Aggregation Block") are each supported by 4 switches. The ABs will uplink via 512x40G links to 256 Spine Blocks, each SB supporting up to 64 ABs with 128x40G total downlinks. 
 
## Hardware Considerations

## Software and Control
