# OSI Model 
OSI model is a conceptual model that characterizes and standardizes how different software and hardware components involved in a network communication should divide labor and interact with one another. It has seven layers.

![Alt Text](/images/osi-model.jpg)

![Alt Text](/images/layer-protocols.jpg)

### Glossary
* Datagram - If the transport protocol is UDP, the unit of data sent from UDP to network layer is called Datagram. [UDP + Data]
* Segment - If the transport protocol is TCP, the unit of data sent from TCP to network layer is called Segment. [TCP + Data]
* Packet - Data sent over a network is divided into smaller segments called packets. [IP address + Segment/Datagram]
* Frame - Consists of a link layer header followed by a packet. [MAC + Packet + FCS] (Media Access Control, Frame Check Sequence)
    * Frame check sequence (FCS) refers to the extra bits and characters added to data packets for error detection and control.
* Bits - represented using electrical signals and pulses of light transferred through a computer network. A bit has a single binary value, either 0 or 1.

![alt text](/images/frame-packet-segment.jpg)

**Layer 7: Application Layer** - application user interface like IE / Outlook, protocols like http, ftp work on this layer

The application layer of OSI model interacts directly with software applications to provide communication functions as required, and it is the closest to end users. Functions of application layer typically include verifying the availability of communication partners and resources to support any data transfer. This layer also defines protocols for end applications, such as domain name system (DNS), file transfer protocol (FTP), hypertext transfer protocol (HTTP), Internet massage access protocol (IMAP), post office protocol (POP), simple mail transfer protocol (SMTP), Simple Network Management Protocol (SNMP), and Telnet (a terminal emulation).

**Layer 6: Presentation Layer** - converts data into standard format like XML, responsible for encryption

The presentation layer checks the data to ensure it is compatible with the communications resources. It translates the data into the form that the application level and lower levels accept. Any needed data formatting or code conversion is also handled by the sixth layer, such as converting an Extended Binary Coded Decimal Interchange Code (EBCDIC) coded text file to an American Standard Code for Information Interchange (ASCII) coded text file. It functions for data compression and encryption as well. For example, video calls will be compressed during the transmission so that it can be transmitted faster, and the data will be recovered at the receiving side. For the data that has high security requirements, such as a text message containing your password, it will be encrypted at this layer.

**Layer 5: Session Layer** - establishes, manages, and terminates sessions between Peer to Peer

The session layer controls the dialogues (connections) between computers. It establishes, manages, maintains and ultimately terminates the connections between the local and remote application. Layer 5 software also handles authentication and authorization functions. It verifies the data is delivered as well. The session layer is commonly implemented explicitly in application environments that use remote procedure calls.

**Layer 4: Transport Layer** - data gets converted to segments, TCP/UDP header is added here

The transport layer provides the functions and means of transferring data sequences from a source to a destination host via one or more networks, while maintaining the quality of service (QoS) functions and ensure the complete delivery of the data. The integrity of the data can be guaranteed via error correction and similar functions. It can also provide explicit flow control function. Though not strictly conforming to the OSI model, the TCP and User Datagram Protocols (UDP) are essential protocols in layer 4.

**Layer 3: Network Layer** - data gets converted to packets, Router works on this layer

The network layer handles packet routing via logical addressing and switching functions. A network is a medium to which many nodes can be connected. Every node has an address. When a node needs to transfer message to other nodes, it can merely provide the content of the massage and the address of the destination node, then the network will find the way to deliver the message to the destination node, possibly routing through other nodes. If the message is too long, the network may split it into several segments at one node, sending them separately and reassembling the fragments at another node.

**Layer 2: Data Link Layer** - data gets converted to frames, Switch works on this layer

The data link layer provides node-to-node transfer — a link between two directly connected nodes. It handles packaging and unpacking the data in frames. It defines the protocol to establish and terminate a connection between two physically connected devices, such as Point-to-Point Protocol (PPP). The data link layer is generally divided into two sub-layers: 
1. Media Access Control (MAC) layer - MAC layer is responsible for controlling how devices in a network gain access to a media and permission to transmit data. 
2. Logical Link Control (LLC) layer- LLC layer is responsible for identifying and encapsulating network layer protocols, and controls error checking and frame synchronization.

![alt txt](/images/data-link-layer.png)

**Layer 1: Physical Layer** - data travel in the form of Bits (0’s and 1’s) using devices like Hubs, Fibre Optics

The physical layer defines the electrical and physical specifications of the data connection. For example, the layout of pins of the connector, the operation voltages of an electrical cable, optical fiber cable specifications, and the frequency for wireless devices. It is responsible for transmission and reception of unstructured raw data in a physical medium. Bit rate control is done at the physical layer. It is the layer of low-level networking equipment and is never concerned with protocols or other higher-layer items.

![Alt Text](/images/signal-to-bits.png)

## Difference between networking devices - Hub, Switch & Router

Explained simply in this video - https://www.youtube.com/watch?v=ZvWn5xBflUs

![Alt Text](/images/hub-switch-router.jpg)

## Data processing during transmission
When a user requests to browse a website on the computer, the remote server software firstly gives the requested data to the application layer, where it is processed from layer to layer down with each layer performing its designated functions. The data is then transmitted over the physical layer of the network until the destination server or another device receives it. At this point the data is passed up through the layers again, each layer performing its assigned operations until the data is used by the receiving software.

![Alt Text](/images/data-processing-in-OSI.jpg)

During the transmission, each layer adds a header, or footer, or both to the PDU coming from the upper layer, which directs and identifies the packet. This process is called encapsulation. The header (and footer) and the data together form the PDU for the next layer. The process continues until reaching the lowest-level layer (physical layer or network access layer), from which the data is transmitted to the receiving device. The receiving device reverses the process, de-encapsulating the data at each layer with the header and footer information directing the operations. Then the application finally uses the data. The process is continued until all data is transmitted and received.
