graph TB
    subgraph "Internet"
        ISP1[ISP]
        ISP2[ISP]
    end

    subgraph "CloudCoreNetworks"
        subgraph "PublicSubnet"
            LB[Load Balancer]
            FW[Firewall]
        end

        subgraph "AppSubnet"
            WS[Web Server]
            AP[App Server]
            DB[Database]
        end

        subgraph "ManagementSubnet"
            DC1[Domain Controller]
            DC2[Domain Controller]
        end

        NAT[NAT Device]
        RTR[Router]

        LB -- HTTPS --> FW
        FW -- HTTP --> WS
        WS-- "App Traffic" --> AP
        AP --- DB
        DC1 --- DC2

        ISP1 -->|Internet| NAT
        ISP2 -->|Internet| NAT
        NAT --> RTR
        RTR -- "App Subnet" --> AP
        RTR -- "Mgmt Subnet" --> DC1
        RTR -- "Mgmt Subnet" --> DC2

    end
