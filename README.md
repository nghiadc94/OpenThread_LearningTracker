# OpenThread Learning Tracker

This repository documents my journey to learn the Thread protocol and OpenThread stack for IoT development.

---

## 🎯 Goals

- Understand Thread protocol architecture
- Learn OpenThread stack internals and development flow
- Build working Thread networks using simulation and real hardware
- Work with IPv6, 6LoWPAN, CoAP, and mesh routing

---

## 🗂️ Learning Modules

### ✅ Module 1: Thread Fundamentals
- [ ] What is Thread and why use it?
- [ ] IEEE 802.15.4 and 6LoWPAN basics
- [ ] Thread network roles (Leader, Router, REED, Child)
- [ ] Mesh topology and self-healing concepts

### ✅ Module 2: OpenThread Stack Architecture
- [ ] OpenThread core layers: MAC, MLE, IP6, etc.
- [ ] NCP vs RCP architecture
- [ ] Build OpenThread from source (POSIX target)
- [ ] Understand Spinel protocol and NCP control

### ✅ Module 3: IPv6, UDP, and CoAP
- [ ] Thread-specific IPv6 address types
- [ ] Mesh-local routing, SLAAC
- [ ] UDP packet structure and behavior
- [ ] CoAP protocol: basics + OpenThread API
- [ ] Send CoAP messages in simulation

### ✅ Module 4: Border Router + Integration
- [ ] Set up OTBR on Raspberry Pi or Linux VM
- [ ] Configure NAT64/DNS64 for Internet access
- [ ] Use `ot-ctl` or `python-commissioner`
- [ ] Commission new Thread devices

---

## 🛠️ Practice Projects

- [ ] Build a 3-node simulated mesh with OpenThread CLI
- [ ] Implement CoAP server/client between nodes
- [ ] Analyze traffic using Wireshark
- [ ] Deploy OTBR with nRF52840 dongle as RCP
- [ ] Commission devices securely via Joiner/Commissioner

---

## 📚 Reference Links

- [OpenThread Docs](https://openthread.io/)
- [Thread Group](https://www.threadgroup.org/)
- [RFC 4944 (6LoWPAN)](https://tools.ietf.org/html/rfc4944)
- [RFC 7252 (CoAP)](https://datatracker.ietf.org/doc/html/rfc7252)

---
