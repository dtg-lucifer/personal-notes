To connect your VPC to an on-premises data center via **VPN** using Terraform, you'll need to:

1. **Create a Virtual Private Gateway (VGW)** for your VPC.
2. **Create a Customer Gateway (CGW)** to represent your on-premises environment.
3. **Establish a VPN connection** between your VPC and the on-premises network.

Below is a **Terraform** example that configures a VPN between your AWS VPC and an on-premises data center using a **Customer Gateway** (CGW) and a **Virtual Private Gateway** (VGW). 

### Prerequisites:
- A VPC already exists or you can include the VPC setup in this configuration (similar to the earlier example).
- You need a **public IP** from your on-premises data center that will serve as the **Customer Gateway**.
  
### Terraform Code Example for VPN Setup:

```hcl
provider "aws" {
  region = "us-west-2"
}

# Step 1: Create a VPC (if you don't have one)
resource "aws_vpc" "main_vpc" {
  cidr_block = "10.0.0.0/16"
  tags = {
    Name = "main_vpc"
  }
}

# Step 2: Create a Customer Gateway
# Replace with your on-premises network's public IP
resource "aws_customer_gateway" "cgw" {
  bgp_asn    = 65000
  ip_address = "203.0.113.12"  # Replace with your on-premises public IP
  type       = "ipsec.1"

  tags = {
    Name = "on_prem_cgw"
  }
}

# Step 3: Create a Virtual Private Gateway
resource "aws_vpn_gateway" "vgw" {
  vpc_id = aws_vpc.main_vpc.id
  tags = {
    Name = "main_vgw"
  }
}

# Step 4: Attach the Virtual Private Gateway to the VPC
resource "aws_vpn_gateway_attachment" "vpc_attachment" {
  vpc_id             = aws_vpc.main_vpc.id
  vpn_gateway_id     = aws_vpn_gateway.vgw.id
}

# Step 5: Create the VPN Connection
resource "aws_vpn_connection" "vpn_connection" {
  customer_gateway_id = aws_customer_gateway.cgw.id
  vpn_gateway_id      = aws_vpn_gateway.vgw.id
  type                = "ipsec.1"
  
  # Tunnel configurations, optional, customize as needed
  static_routes_only = true  # Static routing example

  tags = {
    Name = "main_vpn_connection"
  }
}

# Step 6: Route Table Update to Use VPN Connection for Specific Traffic
# Create a route for the private subnet to use the VPN for traffic to the on-premises network
resource "aws_route" "private_route" {
  route_table_id         = aws_vpc.main_vpc.main_route_table_id
  destination_cidr_block = "192.168.1.0/24"  # Replace with on-premises network range
  gateway_id             = aws_vpn_gateway.vgw.id
}
```

### Explanation of Key Components:
1. **Customer Gateway (CGW)**:
   - This resource represents the on-premises side of the VPN. You need the **public IP** of your on-premises router/firewall to configure this.
   
2. **Virtual Private Gateway (VGW)**:
   - This acts as the VPN concentrator on the AWS side of the connection.

3. **VPN Connection**:
   - A VPN connection is established between the Customer Gateway and the Virtual Private Gateway.

4. **Routing**:
   - Traffic from the VPC to the on-premises network (defined by the CIDR block `192.168.1.0/24`) is routed through the VPN.

### How to Test:

1. **Replace the placeholders**: Update the `ip_address` in the `aws_customer_gateway` block with your actual on-premises public IP, and the `destination_cidr_block` in the route with your on-premises network’s CIDR.

2. **Run Terraform commands**:
   ```bash
   terraform init
   terraform apply
   ```
   
   This will set up the VPN infrastructure on AWS.

3. **Configure your on-premises firewall/router**: On the on-premises side, you need to configure the corresponding VPN settings to match the tunnel details (like IPsec parameters). AWS will provide these details after the VPN connection is established (you can view them in the AWS console or fetch them via Terraform).

### Further Customizations:
- **Dynamic Routing**: If you want to use dynamic routing (BGP), remove `static_routes_only = true` and configure BGP ASN settings accordingly.
- **Tunnel Options**: AWS VPN connections offer two tunnels for redundancy, and you can customize each tunnel’s parameters (encryption, pre-shared keys, etc.).

This setup will create a VPN connection allowing secure communication between your AWS VPC and your on-premises data center, creating a hybrid cloud environment. Let me know if you need help with any specifics or further customization!