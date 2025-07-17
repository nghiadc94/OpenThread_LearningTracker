# Thread Network Education
## Thread Network Definition
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

## Thread device types and roles
### Device Types
#### Full Thread Device (FTD)
- Radio is constantly enabled
- Always participates in thread network
- Usually are mains powered devices
#### Minimal Thread Device (MTD)
- Not always participates in thread network
- Low power is enabled, such as sleep mode or disable radio
- Usually battery operated devices
