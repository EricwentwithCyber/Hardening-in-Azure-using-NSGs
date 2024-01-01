# Hardening-in-Azure-using-NSGs
This guide provides a step-by-step approach to setting up and securing a network within Azure.

# Azure Network Setup and Security Guide

This guide provides a step-by-step approach to setting up and securing a network within Azure.

---

## 1. Set Up a Virtual Network (VNet) and Subnets

### Create a Virtual Network:

- **Log in to Azure Portal.**
- Navigate to **Virtual Networks** and click **Create**.
- Enter basic information:
  - Name: Choose a name for your VNet.
  - Region: Select the Azure region.
- Specify the address space, e.g., `10.1.0.0/16`.
- Click **Next: Subnets**.

### Create Subnets:

- Add a Subnet:
  - Name: `Frontend`.
  - Address range: Specify a range, e.g., `10.1.0.0/24`.
- Add another Subnet:
  - Name: `Backend`.
  - Address range: Choose a different range, e.g., `10.1.1.0/24`.
- Click **Review and create** and then **Create**.

---

## 2. Deploy Virtual Machines (VMs)

### Deploy VMs:

- Navigate to **Virtual Machines** and click **Create**.
- Fill out the basics (name, region, image, size).
- Under **Networking**, select your VNet and choose the `Frontend` subnet for the first VM.
- Repeat the process for the second VM but select the `Backend` subnet.
- Ensure that necessary ports are open (SSH port 22 for Linux or RDP port 3389 for Windows).
- Review and create the VMs.

---

## 3. Initial Network Security Group (NSG) Setup

### Create NSGs for VMs:

- Navigate to **Network Security Groups** and click **Create**.
- Provide the necessary details (name, region).
- Once created, go to the NSG and under **Settings**, select **Subnets**.
- Associate each NSG with the corresponding VM's subnet.

---

## 4. Configuring NSG Rules for VMs

### Define Rules:

- In each NSG, go to **Inbound security rules** and click **Add**.
- Create rules such as:
  - Allow SSH/RDP: Source: Your IP, Destination: Any, Port: 22 (SSH) or 3389 (RDP), Action: Allow.
  - Deny all other inbound traffic: Source: Any, Destination: Any, Port: Any, Action: Deny.

---

## 5. Create NSGs for Subnets

### Create Subnet NSGs:

- Repeat the NSG creation process, but these NSGs will be for subnets.
- Associate each NSG with the respective subnet (Frontend and Backend).

---

## 6. Configuring NSG Rules for Subnets

### Define Subnet Rules:

- For the `Frontend` subnet NSG, allow HTTP/HTTPS traffic:
  - HTTP Rule: Source: Any, Destination: Any, Port: 80, Action: Allow.
  - HTTPS Rule: Source: Any, Destination: Any, Port: 443, Action: Allow.
- For the `Backend` subnet NSG, restrict traffic as needed:
  - Allow specific traffic from the `Frontend` subnet and deny all other traffic.

---

**Note:** Each step involves a number of configurations and choices. Be sure to understand the implications of each setting, especially the network and security configurations, as they are crucial for the overall security and functionality of your Azure environment.

**Documentation Author:** Eric Noga
**Date:** 1/1/2024
