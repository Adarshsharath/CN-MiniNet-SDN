🟦 Static Routing using SDN Controller in Mininet
📌 Title

Static Routing using SDN Controller in Mininet

📚 Course

Computer Networks

👤 Details
Name: (Your Name)
USN: (Your ID)
Date: (Submission Date)
🟦 1. Problem Statement

The objective of this project is to implement static routing using a Software Defined Networking (SDN) controller.

This project demonstrates:

Controller–switch interaction
Flow rule (match–action) design
Controlled network behavior using OpenFlow
Static path enforcement

Unlike traditional networks, routing decisions are made centrally by the controller instead of distributed routers.

🟦 2. Objective
Design a custom network topology using Mininet
Implement an SDN controller using Ryu
Manually define routing paths using flow rules
Analyze network behavior under normal and failure conditions
🟦 3. Tools & Technologies Used
Mininet
Ryu
Open vSwitch
Ubuntu/Linux Environment
🟦 4. Execution & Setup
🔹 Step 1: Start Controller
ryu-manager controller.py
🔹 Step 2: Start Mininet
sudo mn --custom topo.py --topo demo --controller=remote
🔹 Step 3: View Network Topology
net
🟦 5. Network Topology Description
🔹 Components
Hosts: h1, h2, h3
Switches: s1, s2, s3, s4
📌 Key Points
Multiple paths exist
Controller enforces a fixed static path
No dynamic routing
🔹 Static Path Used
h1 → s1 → s3 → s4 → h3
🟦 6. Implementation Details
🔹 Controller Logic
Handles packet_in events
Installs flow rules dynamically
Uses match–action forwarding
🔹 Behavior
Only one path is allowed
Alternate paths are ignored
🟦 7. Results & Observations
✅ 7.1 Successful Routing (h1 → h3)
h1 ping h3

✔ Packets successfully delivered
✔ Static routing path followed

❌ 7.2 Unused Path (h1 → h2)
h1 ping h2

❌ Communication not properly established
✔ Shows alternate path is not used

📊 7.3 Flow Table Verification
sh ovs-ofctl -O OpenFlow13 dump-flows s1

✔ Shows match-action flow rules
✔ Confirms controller behavior

❌ 7.4 Failure Scenario
link s3 s4 down
h1 ping h3

❌ Communication fails
✔ No alternate routing available

🟦 8. Analysis
Static routing ensures predictable paths
Controller provides centralized control
No automatic rerouting in case of failure
Flow tables validate implementation
🟦 9. Conclusion

This project successfully demonstrates:

SDN-based static routing
Controller-driven flow rule installation
Fixed path enforcement
Behavior under failure conditions
🟦 10. Learning Outcomes
Understood SDN architecture
Learned OpenFlow match-action model
Implemented Ryu controller
Analyzed network behavior using Mininet
🟦 11. References
Mininet Documentation
Ryu Controller Documentation
Course Notes
