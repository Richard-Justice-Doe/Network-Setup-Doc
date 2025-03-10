# Network-Setup-Doc
# **Network Configuration Guide**

## **Overview**
This documentation provides a detailed guide for configuring a network with subnetted IPs, including routers, switches, and PCs. The network consists of **two subnets** with interconnectivity through a router.

## **Network Topology**
### **Devices in the Network:**
- **Router** (Cisco)
- **Switch 1 (S1)** - VLAN 1 (Connected to Router and PC1)
- **Switch 2 (S2)** - VLAN 1 (Connected to Router and PC2)
- **PC1** (Connected to Switch 1)
- **PC2** (Connected to Switch 2)

## **IP Addressing Scheme**
The network is subnetted from **192.168.1.0/24** into **two /25 subnets**.

| **Device** | **Interface** | **IP Address** | **Subnet Mask** | **Default Gateway** |
|------------|--------------|--------------|-------------|----------------|
| **Router (R1)** | GigabitEthernet0/0 | 192.168.1.126 | 255.255.255.128 | N/A |
| **Router (R1)** | GigabitEthernet0/1 | 192.168.1.254 | 255.255.255.128 | N/A |
| **Switch 1 (S1)** | VLAN 1 | 192.168.1.1 | 255.255.255.128 | 192.168.1.126 |
| **Switch 2 (S2)** | VLAN 1 | 192.168.1.129 | 255.255.255.128 | 192.168.1.254 |
| **PC1** | NIC | 192.168.1.2 | 255.255.255.128 | 192.168.1.126 |
| **PC2** | NIC | 192.168.1.130 | 255.255.255.128 | 192.168.1.254 |

---

## **Step 1: Configuring PCs**
Each PC must be assigned an IP address and default gateway.

### **PC1 Configuration**
```bash
IP Address: 192.168.1.2
Subnet Mask: 255.255.255.128
Default Gateway: 192.168.1.126
```

### **PC2 Configuration**
```bash
IP Address: 192.168.1.130
Subnet Mask: 255.255.255.128
Default Gateway: 192.168.1.254
```

---

## **Step 2: Configuring the Router (R1)**

### **1. Access the Router CLI**
```bash
enable
configure terminal
```

### **2. Configure Interfaces**
#### **Interface G0/0 (Connected to S1)**
```bash
interface GigabitEthernet0/0
ip address 192.168.1.126 255.255.255.128
no shutdown
exit
```

#### **Interface G0/1 (Connected to S2)**
```bash
interface GigabitEthernet0/1
ip address 192.168.1.254 255.255.255.128
no shutdown
exit
```

### **3. Enable Routing**
```bash
ip routing
exit
```

### **4. Save Configuration**
```bash
write memory
```

---

## **Step 3: Configuring Switches**

### **Switch 1 (S1) Configuration**
```bash
enable
configure terminal
interface vlan 1
ip address 192.168.1.1 255.255.255.128
no shutdown
ip default-gateway 192.168.1.126
exit
write memory
```

### **Switch 2 (S2) Configuration**
```bash
enable
configure terminal
interface vlan 1
ip address 192.168.1.129 255.255.255.128
no shutdown
ip default-gateway 192.168.1.254
exit
write memory
```

---

## **Step 4: Verifying Connectivity**
To verify connectivity, use the following ping commands.

### **From PC1 to Router (G0/0)**
```bash
ping 192.168.1.126
```

### **From PC2 to Router (G0/1)**
```bash
ping 192.168.1.254
```

### **From PC1 to PC2**
```bash
ping 192.168.1.130
```

### **Check Router Routing Table**
```bash
show ip route
```

### **Check Interface Status on Router**
```bash
show ip interface brief
```

---

## **Conclusion**
✅ The **network is successfully configured** with **two /25 subnets**.
✅ **All devices can communicate** with each other.
✅ **Use `ping` and `show ip route` to verify connectivity**.

---

## **Next Steps**
- Enable **SSH access** on switches for secure remote management.
- Implement **VLANs** for additional segmentation.
- Add **security configurations** such as **ACLs and port security**.

---

### **Author**
📌 _Published on GitHub_ 🚀
