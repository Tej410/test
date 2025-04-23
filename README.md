#AWS Architecture

```mermaid
graph LR
    subgraph AWS Cloud
        subgraph Region (us-east-1)
            direction LR
            subgraph Project VPC
                direction LR
                Internet_Gateway -- Internet Access --> Public_Subnet_1 & Public_Subnet_2
                subgraph Availability_Zone_1
                    Public_Subnet_1 -- NAT Gateway --> Private_Subnet_1
                    Private_Subnet_1 -- Application Servers --> DB_Subnet_1
                    DB_Subnet_1 -- MySQL RDS --> Secrets_Manager
                end
                subgraph Availability_Zone_2
                    Public_Subnet_2 -- NAT Gateway --> Private_Subnet_2
                    Private_Subnet_2 -- Application Servers --> DB_Subnet_2
                    DB_Subnet_2 -- MySQL RDS --> Secrets_Manager
                end
                Application_Load_Balancer -- Traffic Distribution --> Target_Group
                Target_Group -- Application Traffic --> Application_Servers
                Auto_Scaling_Group -- Instance Management --> Application_Servers
                Application_Servers -- Database Queries --> MySQL_RDS
                IAM_Role -- Permissions --> Application_Servers & MySQL_RDS
                NAT_Gateway
            end
        end
        Secrets_Manager
    style Public_Subnet_1 fill:#ccf,stroke:#333,stroke-width:2px
    style Public_Subnet_2 fill:#ccf,stroke:#333,stroke-width:2px
    style Private_Subnet_1 fill:#aaffaa,stroke:#333,stroke-width:2px
    style Private_Subnet_2 fill:#aaffaa,stroke:#333,stroke-width:2px
    style DB_Subnet_1 fill:#aaffff,stroke:#333,stroke-width:2px
    style DB_Subnet_2 fill:#aaffff,stroke:#333,stroke-width:2px
    style Application_Servers fill:#f9f,stroke:#333,stroke-width:2px
    style MySQL_RDS fill:#fdd,stroke:#333,stroke-width:2px
    style Application_Load_Balancer fill:#ddf,stroke:#333,stroke-width:2px
    style Auto_Scaling_Group fill:#ffe,stroke:#333,stroke-width:2px
    style Secrets_Manager fill:#eef,stroke:#333,stroke-width:2px
    style NAT_Gateway fill:#cce,stroke:#333,stroke-width:2px
    style IAM_Role fill:#ada,stroke:#333,stroke-width:2px
    style Target_Group fill:#bbf,stroke:#333,stroke-width:2px
```
