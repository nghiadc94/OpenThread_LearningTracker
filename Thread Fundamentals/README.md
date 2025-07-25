# Thread Network Fundamentals

## IEEE 802.15.4 and 6LoWPAN basics
### IEEE 802.15.4
IEEE 802.15.4 is a low-power, low-data-rate wireless communication standard. It defines how devices physically send and receive data (the Physical Layer) and how they share access to the radio channel (the MAC Layer).

**IEEE 802.15.4 Features:**
- Data Rate: Typically 250 kbps (in 2.4 GHz band)
- Frequency Bands: 2.4 GHz (worldwide), 868 MHz (EU), 915 MHz (US)
- Range: ~10–100 meters (extended via mesh)
- Low Power: Designed for long battery life (months to years)
- Topology: Star or Mesh

IEEE 802.15.4 included only the radio link and basic coordination between devices, no IP support and no application layer.

### 6LoWPAN
6LoWPAN stands for **IPv6 over Low-Power Wireless Personal Area Networks**
It is a network layer adaptation protocol that allows IPv6 packets to be sent over IEEE 802.15.4 radios.

**6LoWPAN Functions:**
- Header Compression: IPv6 headers are 40 bytes long — too big for 802.15.4’s 127-byte MTU. 6LoWPAN compresses them.
- Fragmentation: Breaks large packets into smaller ones that fit 802.15.4 frames.
- Mesh Forwarding: Adds optional mesh routing support (Thread uses its own layer 3 routing though).

**Why we use 6LoWPAN?**
- It enables direct IP connectivity from small devices to the internet (via IPv6).
- Devices can talk using standard IP-based protocols like CoAP, MQTT, HTTP, etc., with no proprietary translation needed.

### How They Work Together in Thread
  | Layer       | Protocol      | Purpose                   |
  | ----------- | ------------- | ------------------------- |
  | Application | CoAP / Matter | Device control, messaging |
  | Transport   | UDP           | Lightweight transmission  |
  | Network     | IPv6          | Addressing and routing    |
  | Adaptation  | 6LoWPAN       | Compress IPv6 headers     |
  | MAC + PHY   | IEEE 802.15.4 | Over-the-air transmission |

Thread uses:
- IEEE 802.15.4 for the wireless physical layer.
- 6LoWPAN to make IPv6 usable over that wireless link.

## Thread Network basics
### What is Thread?
- Thread is a wireless mesh networking technology developed by the Thread Group
- Thread using IEEE 802.15.4 radio (at 2.4 GHz) for operation, same radio layer as Zigbee.
- Thread runs full IPv6 using 6LoWPAN compression to reduce overhead for low-power devices.
- Focus on mesh networking, which devices can relay messages for one another, increasing range and reliability.
- Capable of self-healing, which the mesh reroutes automatically if one devices goes down.
- Optimized for battery-powered devices.
- No single point of failure. There's no centralized hub which multiple devices can act as routers.
- AES encryption, device authentication, and network partitioning are built-in.

### Why we use it?
- **Mesh Network**: Better coverage, resilience, and reliability without range extenders.
- **IPv6-native**: Seamless integration with the internet and other IP-based systems.
- **Interoperability**: Devices from different vendors can work together.
- **Low Latency & Power**: Ideal for battery-powered sensors and real-time control.
- **Secure**: Strong security model with network-level and application-level encryption.
- **Future-proof**:Backed by major industry players and used in Matter, the new IoT standard.

### Thread vs Other IoT Protocols
  | Protocol | Transport          | Topology            | IP-based         | Use Case                      |
  | -------- | ------------------ | ------------------- | ---------------- | ----------------------------- |
  | Thread   | 802.15.4 + 6LoWPAN | Mesh                | ✅ Yes          | Smart home, sensors, lighting |
  | Zigbee   | 802.15.4           | Mesh                | ❌ No           | Smart home (non-IP)           |
  | BLE      | 2.4GHz             | Star / limited mesh | ❌ No           | Wearables, proximity          |
  | Wi-Fi    | 802.11             | Star                | ✅ Yes          | High data rate, cameras       |
  | LoRaWAN  | Sub-GHz            | Star                | ✅ With gateway | Long range, low data          |

### Typical OSI model for Thread Network
  | OSI Layer | Name             | Thread / IoT Example                                                                 |
  | --------- | ---------------- | ------------------------------------------------------------------------------------ |
  | 7         | **Application**  | **CoAP** (Constrained Application Protocol), your device logic (e.g. sensor service) |
  | 6         | **Presentation** | Data formats like **CBOR**, optional **TLS/DTLS**, JSON/CBOR serialization           |
  | 5         | **Session**      | CoAP message IDs, **DTLS session management**, or simple transaction tracking        |
  | 4         | **Transport**    | **UDP** (Thread uses UDP for lightweight communication)                              |
  | 3         | **Network**      | **IPv6** + **6LoWPAN** compression (used for efficient IP on low-power networks)     |
  | 2         | **Data Link**    | **IEEE 802.15.4 MAC** (Medium Access Control, uses CSMA/CA, PAN IDs, etc.)           |
  | 1         | **Physical**     | **IEEE 802.15.4 PHY** (2.4 GHz radio waves, modulation like O-QPSK, 250 kbps)        |
  
**Detail Breakdown for every layers**
1. Physical Layer (PHY)
- Standard: IEEE 802.15.4
- Example: Your sensor node transmits raw bits over the 2.4GHz band using O-QPSK modulation.
2. Data Link Layer (MAC)
- Standard: IEEE 802.15.4 MAC
- Example:
  - Device uses CSMA/CA to avoid collisions.
  - Adds MAC headers with source/dest PAN ID and short/extended addresses.
  - Handles ACKs for reliability.
3. Network Layer
- Protocol: IPv6 over 6LoWPAN
- Example:
  - IPv6 addressing allows global addressing.
  - 6LoWPAN compresses IPv6 headers to fit in small 127-byte frames.
4. Transport Layer
- Protocol: UDP
- Example:
  - Your temperature sensor sends updates via CoAP over UDP.
  - No TCP in Thread (too heavy); UDP gives fast, lightweight transport.
  - Thread uses mesh routing with Border Routers for internet connectivity.
5. Session Layer
- Example:
  - CoAP tokens and message IDs maintain request/response correlation.
  - Optional DTLS sessions manage secure channels for end-to-end security.
6. Presentation Layer
- Example:
  - Sensor data is serialized in CBOR or JSON.
  - Optional DTLS handles encryption/decryption.
  - May include compression for data payloads.
7. Application Layer
- Protocol: CoAP
- Example:
  - Your device exposes REST-like resources, e.g., /temperature, /status.
  - It responds to CoAP GET or POST requests from another node or cloud app.

### Thread network roles
#### Full Thread Device (FTD)
- Radio is constantly enabled
- Always participates in thread network
- Usually are mains powered devices

**Sub-roles of FTD:**
- **Router**: Forwards messages, extends network range, participates in mesh routing.
- **Leader**: Manages network operations, assigns addresses, coordinates routing.
- **Border Router**: Connects Thread network to external IP networks (like Wi-Fi or Ethernet), allowing internet access.
- **Router Eligible End Device (REED)**: Is normal end device that connect to a router, but can become a router if needed.
#### Minimal Thread Device (MTD)
- Not always participates in thread network.
- Low power is enabled, such as sleep mode or disable radio.
- Usually battery operated devices.
- Can wake up and join the network when needed.
- Only talks to its parent (a Router or Leader).

**Sub-roles of MTD:**
- **End Device (ED)**: Communicates with routers but does not route messages. It can sleep to save power.
- **Sleepy End Device (SED)**: Similar to ED, but designed for very low power operation. It wakes up periodically to send/receive data and then goes back to sleep.

**Border Router (Special Role)**
- It not a standard core role, but essential.
- A Border Router connects the Thread mesh to other IP networks (e.g., Wi-Fi or Ethernet).
- It routes IPv6 traffic between the Thread network and external internet or LAN.
- Devices like the Google Nest Hub, Apple HomePod mini, Silicon Labs dev boards or ESP32 Border Dev Kit can act as Border Routers.
- A Border Router is always a Full Thread Device but not necessarily the Leader.

### Thread Network Topology
Thread uses a mesh topology, which means devices can communicate with each other directly or through intermediate nodes. This allows for:
- **Extended Range**: Devices can relay messages, increasing coverage.
- **Self-Healing**: If one device fails, messages can be rerouted through other devices.
- **Scalability**: New devices can join the network without disrupting existing ones.

### Thread Network Formation
1. **Leader Election**: When a Thread network starts, devices elect a Leader to manage the network.
2. **Address Assignment**: The Leader assigns unique IPv6 addresses to each device.
3. **Routing Table Creation**: Devices build routing tables based on their neighbors and the Leader.
4. **Network Partitioning**: If devices lose connection, they can form new partitions and rejoin the main network when connectivity is restored.
5. **Security**: Devices authenticate each other and establish secure communication channels using AES encryption. 

Devices join the network securely and are assigned a role based on their capabilities.

**Thread Network Self-Healing Concept**
- If the Leader fails, a new one is elected.
- If more routing capacity is needed, a REED can promote itself to a Router.
- If a Router is no longer needed, it can demote itself to save power.