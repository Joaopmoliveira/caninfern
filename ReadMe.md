## Caninfern

Caninfern is the culmination of a project I started during my Ph.D. at IST back in Portugal. 
At some point, after a ton of meetings discussing how to write a control loop that guarantees a specific sample time, 
I went back into hibernation and came up with the Caninfern architecture. 
The software itself is fairly simple, you have three distinct processes, namely: 
a sensor reader; a watchdog; a controller. For the more observant, caninfern derives from "canine inferno", 
which roughly translates to dog from hell, the mitological Cerberus with three heads, 
similar to the proposed architecture. 

The watchdog is like a maestro, 
it keeps the entire thing running. 
It first sends control commands obtained from a previous session, 
then it starts a timer and it tells the sensor reader to grab observations, 
which then warns the watchdog once its finished.
Afterwards the watchdog tells the controller to compute the control law. 
The controllers sends the control command back to the watchdog which stores it. 
The loop will only repeat once the timer expires.
If, at any point, the timer expires, 
and the controller still has not send the control command, 
then the system triggers a safety stop. 

To reduce latency between these three heads, a shared memory region is allocated
and all readings a copied from the sensor thread, directly to the controller thread. 
By isolating the watchdog in a single core, and forbiding the kernel from putting any task there, 
it is possible to achieve a hard real time system so long as no blocking calls are made to the kernel, 
which is the case inside the watchdog.


