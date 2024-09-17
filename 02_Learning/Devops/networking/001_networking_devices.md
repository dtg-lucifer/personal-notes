---
share_link: https://share.note.sx/ah1vjazq#A75igVehU77MVcuI83TqAw29GgNxeu+DQmH3jK5HD/Y
share_updated: 2024-09-17T13:52:38+05:30
---
# Modem
A modem is a electrical device which converts **digital signal to analog signal and analog signal to digital signal** vise versa. It is used to send the digital data produced by the computer to the internet via any type of transportation such as telephone lines to the receiving modem which will therefore convert the analog signal to another digitala singal which can be read by the other computer.
So basically by modem computers can communicate with each other via **wired or guided** forms of communication.
# Repeater
- Operates at the **physical layer** (Layer 1) of the OSI model.
- Its primary function is to **regenerate** and amplify signals.
- Repeats incoming signals to extend their transmission distance within the same network segment.
- Commonly used in older Ethernet networks.
- **Drawback**: Doesn’t filter or process data; simply repeats it.
# Hub
- Also operates at the **physical layer** (Layer 1).
- A **multi-port repeater** that connects multiple devices in a network.
- Like a hub in a wheel, it distributes data to all connected devices.
- **Drawback**: Broadcasts data to all devices, leading to network congestion and inefficiency.

**Active Hub**: These are hubs which have their own poer suppply and can clean, boost and relay the signal along the network. It serves as a repeater as well as wriring cneter. These are used to extend maximum distance between nodes.

**Passive Hub:** These are the hubs which collect wiring from nodes and power supply from active hub. These hubs relay onto the network without cleaning and boosting them and can't be used to extend distance between nodes.
# Bridge
- Operates at the **data link layer** (Layer 2).
- Connects two LANs (Local Area Networks) using the same protocol (e.g., Ethernet).
- Filters data based on **MAC addresses**.
- Helps segment networks and reduce collision domains.
- **Drawback**: Limited to connecting LANs of the same type.
# Gateway
- Acts as a **protocol converter** between different types of networks.
- Connects LANs to WANs (Wide Area Networks) or different network technologies.
- Examples: LAN to Internet gateway, LAN to cellular network gateway.
# Router
This is a device which reoutes the data packets to other networks or devices based on theri desired op packets. It binds the packets with the ip address and sends those to the network which can be therefore received by devices with those particular ip.
**A router serves as a bridge for one network to communicate with an outside network/device.**
- Operates at the **network layer** (Layer 3).
- Routes data between different networks based on **IP addresses**.
- Determines the best path for data to reach its destination.
- Essential for connecting LANs to the Internet.
# Switch
A network bridging device that uses destination addresses to forward packets of data. A switch will have the MAC address of all the devices connected to its ports and forwads the given packet to the port of the matching destination address.
- A **multiport bridge** that operates at the **data link layer** (Layer 2).
- Intelligently forwards data only to the relevant device based on its MAC address.
- Efficiently manages network traffic by creating separate collision domains for each port.
- Replaced hubs in modern networks due to better performance.

# NIC (Network interface card)
- A hardware component that allows devices (e.g., computers, servers) to connect to a network.
- Contains a unique MAC address.
- Provides the physical interface (wired or wireless) for data transmission.