```mermaid
flowchart TD
    subgraph User
        U[👤 Viewer / Admin]
    end

    subgraph AWS
        CF[🌐 CloudFront]
        EC2[💻 EC2 Backend]
        S3[(🗂 S3 Bucket)]
        L[⚡ Lambda Function]
        IAM[(🔑 IAM Roles)]
        VPC[🔒 VPC]
    end

    U -->|Access via Browser| CF
    CF -->|Delivers Content| U

    U -->|Upload Request| EC2
    EC2 -->|Store Media| S3
    S3 -->|Trigger| L
    L -->|AI Auto-Tagging| S3
    CF -->|Fetch Media| S3

    IAM -.-> U
    IAM -.-> EC2
    IAM -.-> S3

    EC2 --> VPC
    S3 --> VPC
    L --> VPC
