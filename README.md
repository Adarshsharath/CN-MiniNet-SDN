# 🌐 Static Routing using SDN Controller in Mininet

> **Course:** Computer Networks
> **Name:** Adarsh Prakash | **SRN:** PES2UG24CS027 | **Sec:** A

---

## 📌 Problem Statement

This project implements **static routing** using a **Software Defined Networking (SDN)** controller in a simulated network environment.

Key demonstrations:
- Controller–switch interaction via OpenFlow
- Flow rule (match–action) design
- Controlled and predictable network behavior
- Static path enforcement without dynamic routing

> Unlike traditional networks, routing decisions are made **centrally by the controller** rather than by distributed routers.

---

## 🎯 Objectives

- Design a custom network topology using **Mininet**
- Implement an SDN controller using **Ryu**
- Manually define routing paths using **flow rules**
- Analyze network behavior under **normal and failure conditions**

---

## 🛠️ Tools & Technologies

| Tool | Description |
|------|-------------|
| **Mininet** | Network emulator for creating virtual topologies |
| **Ryu** | Python-based SDN controller framework |
| **Open vSwitch (OVS)** | Software-based OpenFlow-capable switch |
| **Ubuntu / Linux** | Host operating system |
| **OpenFlow 1.3** | Protocol for controller-switch communication |

---

## 🗂️ Project Structure

```
.
├── controller.py       # Ryu SDN controller with static routing logic
├── topo.py             # Custom Mininet topology definition
└── README.md           # Project documentation
```

---

## 🚀 Execution & Setup

### Prerequisites

```bash
# Install Mininet
sudo apt-get install mininet

# Install Ryu
pip install ryu
```

### Step 1: Start the Controller

```bash
ryu-manager controller.py
```

### Step 2: Start Mininet with Custom Topology

```bash
sudo mn --custom topo.py --topo demo --controller=remote
```

### Step 3: View the Network Topology

```
mininet> net
```

---

## 🖧 Network Topology

```
         h1
          |
         s1
        /   \
       s2    s3
        \   /
         s4
          |
         h3
      (h2 on s2)
```

### Components

| Component | Description |
|-----------|-------------|
| `h1`, `h2`, `h3` | End hosts |
| `s1`, `s2`, `s3`, `s4` | OpenFlow switches |

### Key Points

- Multiple physical paths exist between hosts
- The controller enforces a **single static path**
- **No dynamic routing** — paths do not adapt to failures

### ✅ Static Path Enforced

```
h1 → s1 → s3 → s4 → h3
```

---

## ⚙️ Implementation Details

### Controller Logic (`controller.py`)

- Handles **`packet_in`** events from switches
- **Installs flow rules** dynamically upon first packet arrival
- Uses **match–action** forwarding based on source/destination

### Behavior

| Scenario | Result |
|----------|--------|
| Packet on static path | ✅ Forwarded correctly |
| Packet on alternate path | ❌ Dropped / not routed |

---

## 📊 Results & Observations

### ✅ 7.1 — Successful Routing (`h1 → h3`)

```bash
mininet> h1 ping h3
```

- ✔ Packets successfully delivered
- ✔ Static routing path `h1 → s1 → s3 → s4 → h3` followed

---

### ❌ 7.2 — Unused Path (`h1 → h2`)

```bash
mininet> h1 ping h2
```

- ❌ Communication not properly established
- ✔ Confirms alternate path (`s2`) is intentionally unused

---

### 📋 7.3 — Flow Table Verification

```bash
mininet> sh ovs-ofctl -O OpenFlow13 dump-flows s1
```

- ✔ Shows match-action flow rules installed by the controller
- ✔ Confirms correct controller-driven forwarding behavior

---

### ❌ 7.4 — Failure Scenario

```bash
mininet> link s3 s4 down
mininet> h1 ping h3
```

- ❌ Communication fails after link is brought down
- ✔ Demonstrates that **no automatic rerouting** occurs with static routing

---

## 🔍 Analysis

| Aspect | Observation |
|--------|-------------|
| **Path Predictability** | Static routing ensures deterministic, fixed paths |
| **Centralized Control** | All decisions made at the controller level |
| **Fault Tolerance** | No automatic failover — static paths fail hard |
| **Flow Validation** | Flow tables confirm correct rule installation |

---

## 📝 Conclusion

This project successfully demonstrates:

- ✅ SDN-based static routing in a simulated environment
- ✅ Controller-driven flow rule installation using Ryu
- ✅ Fixed path enforcement via OpenFlow match-action rules
- ✅ Predictable failure behavior confirming no dynamic rerouting

---

## 📚 Learning Outcomes

1. Understood **SDN architecture** and controller-data plane separation
2. Learned the **OpenFlow match-action model**
3. Implemented a functional **Ryu controller**
4. Analyzed network behavior using **Mininet**

---

## 🔗 References

- [Mininet Documentation](http://mininet.org/walkthrough/)
- [Ryu Controller Documentation](https://ryu.readthedocs.io/)
- [OpenFlow Specification](https://opennetworking.org/sdn-resources/openflow/)
- Course Notes — Computer Networks
