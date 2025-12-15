
# 🌍 **Terraform Basics**

A clean and simple guide to understanding **IaC** and **Terraform** for beginners.
![Terraform GIF](terraform.gif)

---
| 📚 **Table of Contents** |
|--------------------------|
| [Terraform Basics](#-terraform-basics) |
| [What is IaC?](#1-what-is-iac-infrastructure-as-code) |
| [Popular IaC Tools](#3-popular-iac-tools) |
| [What is Terraform?](#4-what-is-terraform) |
| [Terraform Blocks](#-terraform-blocks) |
| [EC2 Lab](#-terraform-lab--create-a-simple-ec2-instance) |
| [Alias Provider Lab](#-terraform-alias--multi-region-s3-bucket-example) |
| [Resource Behaviors](#-terraform-resource-behaviors) |
| [VPC + Subnets Lab](#lab-create-a-vpc-and-add-subnets-using-terraform) |
| [Full VPC + EC2 Lab](#lab-terraform-lab-vpc-subnets-igw-route-tables--ec2-with-explanation) |
| [Create AWS Key Pair and EC2](#create-aws-key-pair-and-ec2) |

---

## 📘 **1. What is IaC (Infrastructure as Code)?**

**Infrastructure as Code (IaC)** means **creating and managing infrastructure using code**, not manual clicks.

Instead of using cloud consoles (AWS, Azure, GCP), you write code like:

```
main.tf
variables.tf
provider.tf
```

Terraform reads this code and automatically builds your infrastructure.

### 🔹 **In simple words:**

➡️ *IaC = Automating infrastructure using code.*

---

## 🚀 **2. Advantages of IaC**

| Benefit               | Explanation                              |
| --------------------- | ---------------------------------------- |
| ⚡ Fast Deployment     | Create servers/networks quickly.         |
| 🔁 Repeatable         | Same code = same result every time.      |
| ❌ Fewer Errors        | Removes manual mistakes.                 |
| 📦 Version Controlled | Code can be tracked using Git.           |
| 📈 Scalable           | Easily create or destroy many resources. |
| 💰 Cost Efficient     | Remove unused resources instantly.       |

---

## 🛠️ **3. Popular IaC Tools**

Here are the most commonly used IaC tools:

* **Terraform** (Multi-cloud)
* **AWS CloudFormation** (AWS only)
* **Ansible**
* **Chef**
* **Puppet**
* **SaltStack**

---

## 🌐 **4. What is Terraform?**

Terraform is an **open-source IaC tool** created by **HashiCorp**.

You use Terraform to:

* Create infrastructure
* Modify infrastructure
* Delete infrastructure
* Automate cloud resources

Terraform supports **multiple cloud providers** like:

* AWS
* Azure
* Google Cloud
* DigitalOcean
* Oracle
* Kubernetes
* And many more…

### 🔹 **Terraform uses HCL (HashiCorp Configuration Language)**

HCL files end with `.tf`.

---

## 🎯 **5. Advantages of Terraform**

| Feature                | Why It’s Useful                                  |
| ---------------------- | ------------------------------------------------ |
| 🌏 Multi-Cloud Support | Same tool works on AWS, Azure, GCP.              |
| 📝 Declarative Syntax  | Easy to write and read.                          |
| 📍 State Management    | Tracks all created resources.                    |
| 🧪 Plan Before Apply   | `terraform plan` shows changes before execution. |
| 📦 Reusable Modules    | Organised and clean code.                        |
| 🤖 Automation Ready    | Works well in CI/CD pipelines.                   |
| 🔁 Idempotent          | Running the same code gives the same result.     |

---

## 💡 **Summary (Very Simple)**

* IaC = Managing infrastructure using code
* Terraform = Most popular IaC tool
* Terraform uses `.tf` files
* It supports multi-cloud
* It reduces errors, saves time, and automates everything

---

# 📘 Terraform Blocks 

Terraform uses different blocks to define, manage, and organize infrastructure.
Each block has a specific purpose.
Below are the most important ones with short, clear explanations.

---

## 1️⃣ **terraform block**

The **terraform block** is used for Terraform’s own settings.
It defines:

* Required Terraform version
* Required providers
* Backend (where state file is stored)

```hcl
terraform {
  required_version = ">= 1.5.0"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}
```

📌 *Think of this as Terraform’s global configuration.*

---

## 2️⃣ **provider block**

The **provider block** tells Terraform which cloud or platform you want to use.
Examples: AWS, Azure, GCP, Kubernetes.

```hcl
provider "aws" {
  region = "us-east-1"
}
```

📌 *Providers are like plugins that allow Terraform to talk to the cloud.*

---

## 3️⃣ **resource block**

The **resource block** creates actual infrastructure such as EC2, S3, VPC, etc.
This is the most important block in Terraform.

```hcl
resource "aws_instance" "server" {
  ami           = "ami-12345"
  instance_type = "t2.micro"
}
```

📌 *Every cloud resource you create is defined inside a resource block.*

---

## 4️⃣ **variable block**

The **variable block** is used to take input values.
It helps you make your configuration dynamic and reusable.

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

📌 *Instead of hardcoding values, you store them in variables.*

---

## 5️⃣ **output block**

The **output block** displays useful values after Terraform finishes creating resources.
Example: IP address, URL, instance ID.

```hcl
output "public_ip" {
  value = aws_instance.server.public_ip
}
```

📌 *Outputs help you quickly find important details without searching manually.*

---

## 6️⃣ **locals block**

The **locals block** defines local variables that are used only inside the Terraform files.
Useful for common names, tags, or repeated values.

```hcl
locals {
  app_name = "myapp"
}
```

📌 *Locals reduce duplication by storing reusable values.*

---

## 7️⃣ **data block (Data Source)**

The **data block** reads information about existing resources.
It does *not* create anything new.

```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
}
```

📌 *Used when you want Terraform to fetch an existing AMI, VPC, Subnet, etc.*

---

## 8️⃣ **module block**

The **module block** is used to reuse Terraform code.
You can import code from:

* Local folders
* Terraform Registry
* GitHub

```hcl
module "vpc" {
  source = "./modules/vpc"
}
```

📌 *Modules make Terraform scalable and organized.*

---

## 9️⃣ **backend block**

Defines where Terraform stores the **state file**.
Usually used in team environments for shared state.

```hcl
terraform {
  backend "s3" {
    bucket = "tf-state"
    key    = "prod/terraform.tfstate"
    region = "us-east-1"
  }
}
```

📌 *Backend ensures your state is safe and accessible for collaboration.*

---

## 🔟 **provisioner block**

Runs scripts or commands during resource creation.
Common types:

* `local-exec` (runs on your machine)
* `remote-exec` (runs on the instance)

```hcl
provisioner "local-exec" {
  command = "echo Deployment Done"
}
```

📌 *Provisioners should be used only when necessary, not as the main automation tool.*

# 📜 Basic Terraform Commands

| Command              | Description                                                         |
| -------------------- | ------------------------------------------------------------------- |
| `terraform init`     | Initializes working directory and downloads required providers.     |
| `terraform plan`     | Shows what actions Terraform will take without applying them.       |
| `terraform apply`    | Applies the configuration and creates the infrastructure.           |
| `terraform destroy`  | Destroys all resources defined in the configuration.                |
| `terraform validate` | Validates Terraform file syntax.                                    |
| `terraform fmt`      | Formats Terraform code.                                             |
| `terraform state`    | Interacts with the Terraform state file (list, show, rm, mv, etc.). |

---


# 🚀 Terraform Lab – Create a Simple EC2 Instance

This lab demonstrates how to create a **single EC2 instance** using **only Terraform provider and resource blocks**.
No variables, no modules, no backend, no extra configuration — perfect for beginners.

![TerraForm GIF](https://github.com/shyamdevk/Terraform-Basic-to-Advanced/blob/image/blockec2.gif)

---

## 📁 Folder Setup

Create a new folder for Terraform and open it in VS Code:

```bash
code .
```

---

## 📌 1. Create `main.tf`

Paste the following minimal Terraform configuration:

```hcl
# Provider Block
provider "aws" {
  region = "us-east-1"
}

# Resource Block - EC2 Instance
resource "aws_instance" "demo" {
  ami           = "ami-0c02fb55956c7d316" # Amazon Linux 2 (us-east-1)
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-EC2"
  }
}
```

### ✔ What this does:

* Uses AWS provider
* Launches **one EC2 instance**
* Uses a standard Amazon Linux 2 AMI
* Creates a free-tier eligible `t2.micro` instance
* Adds a simple tag `Name = Terraform-EC2`

---

## 📌 2. Configure AWS Credentials

Run:

```bash
aws configure
```

Enter:

* AWS Access Key
* AWS Secret Key
* Default region: `us-east-1`
* Output: `json`

---

## 📌 3. Initialize Terraform

```bash
terraform init
```

This downloads the AWS provider plugin.

---

## 📌 4. View the Execution Plan

```bash
terraform plan
```

Terraform will show that **1 EC2 instance** will be created.

---

## 📌 5. Deploy the EC2 Instance

```bash
terraform apply -auto-approve
```

Terraform will create the instance in ~30 seconds.

---

## 📌 6. Verify in AWS Console

Go to:

**AWS Console → EC2 → Instances**

You will see:

```
Terraform-EC2
```

---

## 📌 7. Delete the EC2 Instance (Cleanup)

```bash
terraform destroy -auto-approve
```

---

# 🎉 Lab Completed!

This is the most **simple and clean Terraform EC2 lab**, perfect for beginners learning:

* Provider block
* Resource block
* Terraform commands

---

# **Terraform Alias – Multi-Region S3 Bucket Example**

## 📌 **What is `alias` in Terraform?**

`alias` is used to create **multiple provider configurations** of the same provider.

### ✔️ Why use alias?

* Deploy resources **in multiple regions**
* Use **multiple AWS accounts**
* Apply **different provider settings** for different resources

Without alias → Terraform can use **only one provider**.
With alias → You can create **many providers** and assign them to resources.

---

## 📘 **Example: Create S3 Buckets in Multiple Regions**

### ### **1️⃣ Default Provider (us-east-1)**

```hcl
provider "aws" {
  region = "us-east-1"
}
```

### **2️⃣ Provider With Alias (ap-south-1)**

```hcl
provider "aws" {
  alias  = "mumbai"
  region = "ap-south-1"
}
```

---

## 🪣 **Create S3 Buckets**

### **➡️ S3 Bucket in `us-east-1` (Default provider)**

```hcl
resource "aws_s3_bucket" "bucket_us" {
  bucket = "my-bucket-us-east-1-demo123"
}
```

### **➡️ S3 Bucket in `ap-south-1` (Using alias provider)**

```hcl
resource "aws_s3_bucket" "bucket_mumbai" {
  provider = aws.mumbai
  bucket   = "my-bucket-mumbai-demo123"
}
```

---

## 📄 **Full Working Example**

```hcl
# Default provider (us-east-1)
provider "aws" {
  region = "us-east-1"
}

# Provider with alias (ap-south-1)
provider "aws" {
  alias  = "mumbai"
  region = "ap-south-1"
}

# S3 Bucket in US East (default provider)
resource "aws_s3_bucket" "bucket_us" {
  bucket = "my-bucket-us-east-1-demo123"
}

# S3 Bucket in Mumbai (alias provider)
resource "aws_s3_bucket" "bucket_mumbai" {
  provider = aws.mumbai  //calling alias
  bucket   = "my-bucket-mumbai-demo123"
}
```

---

# 🌱 **Terraform Resource Behaviors**

Terraform decides how to manage infrastructure whenever you run:

```
terraform plan
terraform apply
```

There are **four main behaviors** Terraform uses to modify resources.
These notes explain each behavior **simply** with examples.

---

## 🚀 **1. Create**

Terraform will **create a new resource** when it does not exist.

### 🔸 When does it happen?

* First time applying configuration
* A new resource block is added
* Resource deleted manually outside Terraform

### ✔️ Example (plan output)

```
+ create
```

---

## 🗑️ **2. Destroy**

Terraform will **delete** an existing resource.

### 🔸 When does it happen?

* You remove the resource from the `.tf` file
* You run `terraform destroy`
* You changed a setting that forces removal

### ✔️ Example (plan output)

```
- destroy
```

---

## 🔧 **3. Update in Place**

Terraform will **modify** the resource **without deleting it**.

### 🔸 When does it happen?

* You change editable fields
  Example: tags, description, versioning, instance type, etc.

The underlying resource **stays the same**, only its properties are updated.

### ✔️ Example (plan output)

```
~ update in-place
```

---

## 🔁 **4. Destroy and Recreate**

Terraform needs to **destroy the resource first** and then **create a new one**.

This occurs when the field you changed is **immutable** (cannot be modified directly).

### 🔸 When does it happen?

* Changing S3 bucket name
* Changing VPC CIDR
* Changing RDS storage type
* Changing IAM immutable fields

### ✔️ Example (plan output)

```
-/+ destroy and recreate
```

---

## 📘 **Summary Table**

| Behavior               | Meaning                  | When It Occurs                    |
| ---------------------- | ------------------------ | --------------------------------- |
| **Create**             | Makes a new resource     | First apply / new block added     |
| **Destroy**            | Deletes the resource     | Removed in code / destroy command |
| **Update In Place**    | Updates without deleting | Editable fields changed           |
| **Destroy & Recreate** | Delete → create again    | Immutable fields changed          |

---

# **Terraform EC2 – Update in Place vs Destroy & Recreate**

This README shows **two simple EC2 examples** that demonstrate how Terraform decides:

* **Update in Place**
* **Destroy and Recreate**

Both examples use EC2 **without key pairs**.

---

## 🟦 **1. Update in Place (EC2 Example)**

### ✔️ Change: Tags

Tags can be updated without recreating the instance.

```hcl
resource "aws_instance" "demo" {
  ami           = "ami-1234567890abcd"
  instance_type = "t2.micro"

  tags = {
    Name = "Server1-Updated"
  }
}
```

### **Terraform Behavior**

```
~ update in-place
```

### **Why?**

Tags are editable → EC2 does not need replacement.

---

## 🟥 **2. Destroy and Recreate (EC2 Example)**

### ✔️ Change: AMI

AMI cannot be changed in place.

```hcl
resource "aws_instance" "demo" {
  ami           = "ami-0987654321fedcba"   # changed AMI
  instance_type = "t2.micro"
}
```

### **Terraform Behavior**

```
-/+ destroy and recreate
```

### **Why?**

Changing AMI requires a new EC2 → Terraform destroys and recreates it.

---

## ✔️ **Summary**

| Behavior               | What Changed | Reason                             |
| ---------------------- | ------------ | ---------------------------------- |
| **Update in Place**    | Tags         | Editable property                  |
| **Destroy & Recreate** | AMI          | Cannot be modified → must recreate |

---

# **LAB: Create a VPC and Add Subnets Using Terraform**

This lab demonstrates how to create a **VPC** and then add **public and private subnets** inside it using Terraform.
We also add **Name tags** to identify resources easily.

---

## 🏗️ **1. Create a VPC**

We create a VPC with CIDR **10.0.0.0/16** and a Name tag.

```hcl
resource "aws_vpc" "MainVPC" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "My-VPC"
  }
}
```

---

## 🌐 **2. Create Subnets Inside the VPC**

We must use valid Availability Zones like:
`us-east-1a`, `us-east-1b`, `us-east-1c`, etc.
(AWS does NOT accept the region name like `us-east-1`.)

---

### **Public Subnet (10.0.1.0/24)**

```hcl
resource "aws_subnet" "public_subnet_1" {
  vpc_id            = aws_vpc.MainVPC.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "us-east-1a"

  tags = {
    Name = "Public-Subnet-1"
  }
}
```

---

### **Private Subnet (10.0.2.0/24)**

```hcl
resource "aws_subnet" "private_subnet_1" {
  vpc_id            = aws_vpc.MainVPC.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-east-1b"

  tags = {
    Name = "Private-Subnet-1"
  }
}
```

---

## ✅ **Summary**

* Created a **VPC**
* Added **Name tag**
* Added **Public Subnet** in AZ `us-east-1a`
* Added **Private Subnet** in AZ `us-east-1b`
* Used valid availability zones to avoid errors

---

# **LAB: Terraform Lab: VPC, Subnets, IGW, Route Tables & EC2 with Explanation**

# 1️⃣ **Create VPC**

```hcl
resource "aws_vpc" "MainVPC" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "My-VPC"
  }
}
```

### 📝 Explanation

A VPC is your private network in AWS.
`10.0.0.0/16` gives ~65K IPs and will hold all our resources.

---

# 2️⃣ **Create Public Subnet**

```hcl
resource "aws_subnet" "public_subnet_1" {
  vpc_id            = aws_vpc.MainVPC.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "us-east-1a"

  tags = {
    Name = "Public-Subnet-1"
  }
}
```

### 📝 Explanation

A public subnet is one that will later get internet access using IGW.
CIDR `10.0.1.0/24` gives 256 IPs.

---

# 3️⃣ **Create Private Subnet**

```hcl
resource "aws_subnet" "private_subnet_1" {
  vpc_id            = aws_vpc.MainVPC.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-east-1b"

  tags = {
    Name = "Private-Subnet-1"
  }
}
```

### 📝 Explanation

The private subnet will not get internet access.
Used for backend or database instances.

---

# 4️⃣ **Create Internet Gateway**

```hcl
resource "aws_internet_gateway" "MainIGW" {
  vpc_id = aws_vpc.MainVPC.id

  tags = {
    Name = "My-Internet-Gateway"
  }
}
```

### 📝 Explanation

Internet Gateway gives the VPC a connection to the internet.
Only public subnet uses this.

---

# 5️⃣ **Public Route Table**

```hcl
resource "aws_route_table" "public_rt" {
  vpc_id = aws_vpc.MainVPC.id

  tags = {
    Name = "Public-Route-Table"
  }
}
```

### 📝 Explanation

Route tables decide how traffic flows inside/outside AWS.
This one is for public subnet.

---

# 6️⃣ **Add Route to IGW**

```hcl
resource "aws_route" "public_route" {
  route_table_id         = aws_route_table.public_rt.id
  destination_cidr_block = "0.0.0.0/0"
  gateway_id             = aws_internet_gateway.MainIGW.id
}
```

### 📝 Explanation

`0.0.0.0/0` means internet traffic.
Sending it to IGW makes the subnet **public**.

---

# 7️⃣ **Private Route Table**

```hcl
resource "aws_route_table" "private_rt" {
  vpc_id = aws_vpc.MainVPC.id

  tags = {
    Name = "Private-Route-Table"
  }
}
```

### 📝 Explanation

Used for private subnet.
No internet route → fully isolated.

---

# 8️⃣ **Associate Public Subnet**

```hcl
resource "aws_route_table_association" "public_association" {
  subnet_id      = aws_subnet.public_subnet_1.id
  route_table_id = aws_route_table.public_rt.id
}
```

### 📝 Explanation

Links the public subnet → public route table → internet access enabled.

---

# 9️⃣ **Associate Private Subnet**

```hcl
resource "aws_route_table_association" "private_association" {
  subnet_id      = aws_subnet.private_subnet_1.id
  route_table_id = aws_route_table.private_rt.id
}
```

### 📝 Explanation

Links the private subnet → private route table → no internet.

---

# 🔟 **Public Security Group**

```hcl
resource "aws_security_group" "public_sg" {
  name        = "public-sg"
  description = "Allow SSH and HTTP"
  vpc_id      = aws_vpc.MainVPC.id

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

### 📝 Explanation

* Allows SSH from anywhere
* Allows HTTP from anywhere
  Needed for public EC2 instance.

---

# 1️⃣1️⃣ **Private Security Group**

```hcl
resource "aws_security_group" "private_sg" {
  name        = "private-sg"
  description = "Private Instance Security Group"
  vpc_id      = aws_vpc.MainVPC.id

  ingress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["10.0.0.0/16"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

### 📝 Explanation

Allows traffic only from VPC internal IP range.
Good for private instances like DB/backends.

---

# 1️⃣2️⃣ **Create Key Pair (NEW)**

```hcl
resource "aws_key_pair" "mykey" {
  key_name   = "my-terraform-key"
  public_key = file("~/.ssh/id_rsa.pub")
}
```

### 📝 Explanation

* A key pair is needed to **SSH into EC2**.
* Terraform will upload your **public key** to AWS.
* Make sure you already have:

  ```
  ~/.ssh/id_rsa
  ~/.ssh/id_rsa.pub
  ```
* You will use the **private key** (`id_rsa`) to connect to EC2.

---

# 1️⃣3️⃣ **Public EC2 Instance (with key pair)**

```hcl
resource "aws_instance" "public_instance" {
  ami           = "ami-0c02fb55956c7d316"
  instance_type = "t2.micro"
  subnet_id     = aws_subnet.public_subnet_1.id
  security_groups = [aws_security_group.public_sg.id]

  associate_public_ip_address = true
  key_name = aws_key_pair.mykey.key_name

  tags = {
    Name = "Public-Instance"
  }
}
```

### 📝 Explanation

* Public instance → has public IP
* Uses the **key pair** for SSH access
* Security Group allows HTTP + SSH
* Great for web servers or bastion host

---

# 1️⃣4️⃣ **Private EC2 Instance (with key pair)**

```hcl
resource "aws_instance" "private_instance" {
  ami           = "ami-0c02fb55956c7d316"
  instance_type = "t2.micro"
  subnet_id     = aws_subnet.private_subnet_1.id
  security_groups = [aws_security_group.private_sg.id]

  associate_public_ip_address = false
  key_name = aws_key_pair.mykey.key_name

  tags = {
    Name = "Private-Instance"
  }
}
```

### 📝 Explanation

* Private instance → **no public IP**
* Still has the key pair, but you must SSH **via the public instance (bastion)**
* Only internal access allowed
* Good for private app layers / database

---

# **🌟 Terraform Meta Arguments**
![TerraForm GIF](https://github.com/shyamdevk/Terraform-Basic-to-Advanced/blob/image/meta.webp)

Meta arguments are **special instructions** you add inside a Terraform resource block.
They **don’t represent a resource**, but they **control how Terraform should create, update, or manage** a resource.

You can use them inside **any resource** like this:

```hcl
resource "aws_instance" "example" {
  ami           = "ami-123456"
  instance_type = "t2.micro"

  # meta arguments
  count      = 2
  depends_on = [aws_vpc.main]
}
```

---

## 🚀 Why Meta Arguments Are Useful?

They help you:

* Create multiple resources easily
* Control resource order
* Prevent accidental destruction
* Ignore certain changes
* Select which provider to use

---

# 🧱 **1. count**

Used to **create multiple copies** of the same resource using a single block.

### ✔ Example:

```hcl
resource "aws_instance" "server" {
  count = 3
  ami   = "ami-123"
  instance_type = "t2.micro"
}
```

This creates **3 EC2 instances**.

---

# 🧱 **2. for_each**

Also creates multiple resources but with **better control** than `count`.

Useful with **maps** or **sets**.

### ✔ Example:

```hcl
resource "aws_s3_bucket" "b" {
  for_each = {
    bucket1 = "projectA"
    bucket2 = "projectB"
  }

  bucket = each.key
  tags = {
    Name = each.value
  }
}
```

---

# 🧱 **3. depends_on**

Terraform normally auto-detects dependencies.
Use `depends_on` when you want to **force a creation order**.

### ✔ Example:

```hcl
resource "aws_instance" "app" {
  depends_on = [aws_security_group.sg]
}
```

This ensures the security group is created **first**.

---

# 🧱 **4. lifecycle**

Controls **how Terraform manages resources** during create, update, destroy.

---

### 🔸 `create_before_destroy`

Create new resource **before** deleting old one
→ Avoid downtime

```hcl
lifecycle {
  create_before_destroy = true
}
```

---

### 🔸 `prevent_destroy`

Protects resource from accidental deletion.

```hcl
lifecycle {
  prevent_destroy = true
}
```

---

### 🔸 `ignore_changes`

Tell Terraform to **not modify** certain attributes.

```hcl
lifecycle {
  ignore_changes = [
    tags
  ]
}
```

---

# 🧱 **5. provider**

Select a **specific provider configuration** when you have more than one.

### ✔ Example:

```hcl
resource "aws_instance" "db" {
  provider = aws.us_east_1
}
```

---

# 📌 Summary Table

| Meta Argument  | What it Does                                   |
| -------------- | ---------------------------------------------- |
| **count**      | Creates multiple copies of a resource          |
| **for_each**   | Creates multiple resources with better control |
| **depends_on** | Forces resource creation order                 |
| **lifecycle**  | Controls create/update/delete behavior         |
| **provider**   | Selects which provider configuration to use    |

---

# 🌟 Terraform Meta Arguments — Easy Labs

This guide contains **simple, beginner-friendly labs** to understand all **Meta Arguments in Terraform**.

Meta arguments help Terraform control **how resources are created, updated, or destroyed**.

---

# 📘 Meta Arguments Covered

* `count`
* `for_each`
* `depends_on`
* `lifecycle`

  * `create_before_destroy`
  * `prevent_destroy`
  * `ignore_changes`
* `provider`

---

---

# 🧪 LAB 1 — Using `count`

### 🎯 Goal

Create **2 EC2 Instances** using the `count` meta argument.

### 📄 main.tf

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "web" {
  count = 2
  ami = "ami-0c02fb55956c7d316"
  instance_type = "t2.micro"

  tags = {
    Name = "Server-${count.index}"
  }
}
```

### ▶️ Steps

1. `terraform init`
2. `terraform apply`
3. Go to AWS → EC2 → You will see **2 instances created**.

---

---

# 🧪 LAB 2 — Using `for_each`

### 🎯 Goal

Create **2 S3 Buckets** using `for_each`.

### 📄 main.tf

```hcl
provider "aws" {
  region = "us-east-1"
}

locals {
  bucket_list = {
    bucket1 = "my-demo-bucket-a"
    bucket2 = "my-demo-bucket-b"
  }
}

resource "aws_s3_bucket" "demo" {
  for_each = local.bucket_list

  bucket = each.value

  tags = {
    Name = each.key
  }
}
```

### ▶️ Steps

1. `terraform init`
2. `terraform apply`
3. Check AWS S3 → You will see **bucket-a** and **bucket-b**.

---

---

# 🧪 LAB 3 — Using `depends_on`

### 🎯 Goal

Make sure the EC2 instance is created **after** the Security Group.

### 📄 main.tf

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_security_group" "web_sg" {
  name = "web-sg"
}

resource "aws_instance" "server" {
  ami           = "ami-0c02fb55956c7d316"
  instance_type = "t2.micro"

  depends_on = [
    aws_security_group.web_sg
  ]
}
```

### ▶️ Steps

1. `terraform apply`
2. Terraform will first create the **security group**, then the **EC2 instance**.

---

---

# 🧪 LAB 4 — Using `lifecycle`

This lab contains **3 small tests** to understand all lifecycle rules.

---

## 🔸 LAB 4A — `create_before_destroy`

### 🎯 Goal

Terraform should create a new instance **before deleting** the old one.

### 📄 main.tf

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "demo" {
  ami = "ami-0c02fb55956c7d316"
  instance_type = "t2.micro"

  lifecycle {
    create_before_destroy = true
  }
}
```

### ▶️ Steps

1. `terraform apply`
2. Change instance type → `"t3.micro"`
3. `terraform apply` again
4. Terraform creates **new instance first**, then destroys old one.

---

## 🔸 LAB 4B — `prevent_destroy`

### 🎯 Goal

Stop Terraform from deleting the resource.

### 📄 main.tf

```hcl
resource "aws_s3_bucket" "safe" {
  bucket = "my-protected-bucket-1234"

  lifecycle {
    prevent_destroy = true
  }
}
```

### ▶️ Steps

1. `terraform apply`
2. Run `terraform destroy`
3. Destroy will **fail** → Resource protected ✔

---

## 🔸 LAB 4C — `ignore_changes`

### 🎯 Goal

Tell Terraform to ignore changes in specific attributes.

### 📄 main.tf

```hcl
resource "aws_instance" "web" {
  ami = "ami-0c02fb55956c7d316"
  instance_type = "t2.micro"

  tags = {
    Name = "Demo"
  }

  lifecycle {
    ignore_changes = [
      tags
    ]
  }
}
```

### ▶️ Steps

1. Apply once
2. Change the tag name manually in EC2 console
3. Run `terraform apply`
4. Terraform **ignores tag changes**

---

---

# 🧪 LAB 5 — Using `provider`

### 🎯 Goal

Use **two AWS regions** and deploy one bucket in each region.

### 📄 main.tf

```hcl
provider "aws" {
  alias  = "east"
  region = "us-east-1"
}

provider "aws" {
  alias  = "west"
  region = "us-west-1"
}

resource "aws_s3_bucket" "east_bucket" {
  provider = aws.east
  bucket   = "bucket-in-east-1234"
}

resource "aws_s3_bucket" "west_bucket" {
  provider = aws.west
  bucket   = "bucket-in-west-1234"
}
```

### ▶️ Steps

1. `terraform init`
2. `terraform apply`
3. Check AWS S3

   * One bucket in **us-east-1**
   * One bucket in **us-west-1**

---
Understood!
Here is a **simple, clean, beginner-friendly README.md** showing:

✅ How to create a **userdata.sh file in VS Code**
✅ How to write nginx installation script
✅ How to call this userdata file from **main.tf**
✅ Very easy explanation for freshers

---

# 🌟Using External User Data File (VS Code) for Nginx Installation

This guide explains how to:

1. Create a **userdata.sh** file in VS Code
2. Add nginx installation script
3. Call that userdata file inside **Terraform EC2 resource**
4. Launch EC2 with nginx automatically installed

Perfect for beginners.

---

# 1️⃣ Step 1: Create a User Data File in VS Code

Open VS Code and create a new file:

```
userdata.sh
```

Your project folder will look like:

```
vpc-project/
 ├── main.tf
 ├── provider.tf
 ├── userdata.sh   <-- (new file)
```

---

# 2️⃣ Step 2: Add Nginx Installation Script in userdata.sh

Open **userdata.sh** and paste:

```bash
#!/bin/bash
sudo yum update -y
sudo yum install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
```

### 📝 Explanation

* This script installs nginx automatically
* Runs when EC2 first boots
* Starts the webserver immediately

Save the file:

```
CTRL + S
```

---

# 3️⃣ Step 3: Call User Data File in main.tf

In your EC2 resource, replace inline user_data with:

```hcl
user_data = file("${path.module}/userdata.sh")
```

### ✔ Full Example EC2 Resource (Simple)

```hcl
resource "aws_instance" "public_instance" {
  ami                    = "ami-0c02fb55956c7d316"
  instance_type          = "t2.micro"
  subnet_id              = aws_subnet.public_subnet_1.id
  security_groups        = [aws_security_group.public_sg.id]
  associate_public_ip_address = true
  key_name               = aws_key_pair.mykey.key_name

  user_data = file("${path.module}/userdata.sh")

  tags = {
    Name = "Public-Instance"
  }
}
```

### 📝 Explanation

* `file()` → reads an external script
* `${path.module}` → points to the current folder
* EC2 will run **userdata.sh** when it launches

---

Terraform will:

✔ Launch EC2
✔ Upload user_data.sh script
✔ Install nginx
✔ Start nginx
✔ EC2 becomes web server

---

# 6️⃣ Summary (Very Beginner-Friendly)

| File                | Purpose                                   |
| ------------------- | ----------------------------------------- |
| **userdata.sh**     | Holds nginx installation script           |
| **main.tf**         | Calls the file using `user_data = file()` |
| **VS Code**         | Create & edit the script easily           |
| **Terraform Apply** | Runs the script on EC2 boot               |

---
# Create AWS Key Pair and EC2

**Purpose**

This README explains, step-by-step, how to use Terraform to generate an SSH key pair locally, upload the public key to AWS as an EC2 Key Pair, and launch a simple EC2 instance that you can SSH into. It's written for beginners and assumes very little prior knowledge.

---

## Prerequisites

1. **AWS Account** with permissions to create EC2 instances and key pairs.
2. **AWS CLI** configured (optional but helpful). You can configure with `aws configure`.
3. **Terraform** installed (v0.12+ recommended). Download from [https://www.terraform.io](https://www.terraform.io).
4. **A terminal** (Linux/macOS/Windows WSL) and basic familiarity with running commands.

> Tip: If you use Windows, prefer WSL or Git Bash for consistent behavior with file permissions.

---

## What this Terraform does

Below is a **simple and clear explanation of the process BEFORE showing the code**, so beginners understand how Terraform generates a key, stores it, uploads the public key to AWS, and finally associates it with the EC2 instance.

---

# 📘 STEP‑BY‑STEP (Code Snippet + Explanation Format)

## 1️⃣ Generate Private Key

```hcl
resource "tls_private_key" "mykey" {
  algorithm = "RSA"
  rsa_bits  = 4096
}
```

📝 **Explanation**
This block creates a private SSH key **locally**. Terraform does *not* send this key to AWS. You will use this key later to SSH into the EC2 instance.

---

## 2️⃣ Save Private Key to a .pem File

```hcl
resource "local_file" "private_key_pem" {
  content         = tls_private_key.mykey.private_key_pem
  filename        = "mykey.pem"
  file_permission = "0400"
}
```

📝 **Explanation**
This writes the private key to a secure file called **mykey.pem**. SSH requires strict permissions, so the file is set to `0400` (read-only for owner).

---

## 3️⃣ Create AWS Key Pair Using PUBLIC Key

```hcl
resource "aws_key_pair" "mykey" {
  key_name   = "mykey"
  public_key = tls_private_key.mykey.public_key_openssh
}
```

📝 **Explanation**
AWS only stores the **public key**, not the private key. This allows AWS EC2 to verify that you hold the matching private key during SSH.

---

## 4️⃣ Launch EC2 and Attach Key Pair

```hcl
resource "aws_instance" "my_ec2" {
  ami           = "ami-0c02fb55956c7d316"
  instance_type = "t2.micro"
  key_name      = aws_key_pair.mykey.key_name

  tags = {
    Name = "MyEC2"
  }
}
```

📝 **Explanation**
This EC2 instance is created with the key pair `mykey`. This means you can SSH into this instance using:

```
ssh -i mykey.pem ec2-user@<EC2-IP>
```

---

Below this section is the Terraform code that performs all these steps automatically. is the Terraform code that performs all these steps automatically.

* Generates an RSA private key on your machine (not on AWS).
* Saves the private key to a local file `mykey.pem` with secure permissions.
* Creates an AWS Key Pair resource using the generated public key.
* Launches a single EC2 instance and associates it with the created key pair so you can SSH.

---

## Files created by this example

* `main.tf` — Terraform configuration (contains resources shown below).
* `mykey.pem` — Private key file created by Terraform (sensitive; keep safe).

---

## The Terraform code (what to put in `main.tf`)

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
    tls = {
      source  = "hashicorp/tls"
      version = "~> 3.0"
    }
  }
}

provider "aws" {
  region = "us-east-1" # change to your preferred region
}

# 1. Generate an RSA private key locally
resource "tls_private_key" "mykey" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

# 2. Save the private key to a local .pem file
resource "local_file" "private_key_pem" {
  content          = tls_private_key.mykey.private_key_pem
  filename         = "mykey.pem"
  file_permission  = "0400" # ensures owner read only
}

# 3. Create the AWS key pair using the public key generated above
resource "aws_key_pair" "mykey" {
  key_name   = "mykey"
  public_key = tls_private_key.mykey.public_key_openssh
}

# 4. Launch a simple EC2 instance using the key pair
resource "aws_instance" "my_ec2" {
  ami           = "ami-0c02fb55956c7d316" # example: Amazon Linux 2 (change if needed)
  instance_type = "t2.micro"
  key_name      = aws_key_pair.mykey.key_name

  tags = {
    Name = "MyEC2"
  }
}
```


# 🌍 Terraform Workspaces

![TerraForm GIF](https://github.com/shyamdevk/Terraform-Basic-to-Advanced/blob/image/workflow.gif)

This lab explains **Terraform Workspaces** using a **real-world example** of different departments:
- Developer
- Tester
- Production

We will use **one Terraform code** to create **separate EC2 instances** for each department.

---

## 🧠 What is a Terraform Workspace?

A **Terraform workspace** allows you to manage **multiple environments** (dev, test, prod) using the **same Terraform configuration**, but with **separate state files**.

👉 Same code  
👉 Different environments  
👉 No resource conflict  

---

## 🏢 Real-Life Example (Departments)

| Department | Use Case |
|----------|---------|
| Developer | Feature development |
| Tester | QA testing |
| Production | Live application |

Each department:
- Uses the same infrastructure structure
- Needs isolated resources

Terraform workspaces solve this problem.

---

## 📂 How Terraform Stores Workspaces

Terraform automatically creates separate state files:

```

terraform.tfstate.d/
├── dev/
├── test/
└── prod/

````

Each folder contains its own `terraform.tfstate` file.

---

## 🎯 Lab Goal

We will:
- Create **3 workspaces**
- Launch **1 EC2 per workspace**
- Use **different instance sizes**
- Use **workspace name in resource tags**

---

## ✅ Prerequisites

Make sure you have:
- Terraform installed
- AWS CLI configured using `aws configure`
- IAM user with EC2 permissions

---

## 📁 Step 1: Create Project Folder

```bash
mkdir terraform-workspace-lab
cd terraform-workspace-lab
````

This folder will contain all Terraform files.

---

## 📄 Step 2: Create `main.tf`

This file defines **what infrastructure to create**.

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0c02fb55956c7d316"
  instance_type = var.instance_type

  tags = {
    Name       = "EC2-${terraform.workspace}"
    Department = terraform.workspace
  }
}
```

### 🔍 Explanation:

* `terraform.workspace` automatically gives the workspace name
* Each EC2 gets a unique name like `EC2-dev`, `EC2-test`, etc.
* Same code works for all departments

---

## 📄 Step 3: Create `variables.tf`

This file defines **input values**.

```hcl
variable "instance_type" {
  description = "EC2 instance type based on department"
  type        = string
}
```

This allows us to change EC2 size per workspace.

---

## 🚀 Step 4: Initialize Terraform

```bash
terraform init
```

### What this does:

* Downloads AWS provider
* Prepares Terraform to run

You must run this **once per project**.

---

## 🏗 Step 5: Create Workspaces

```bash
terraform workspace new dev
terraform workspace new test
terraform workspace new prod
```

Terraform now has **three environments**.

Check workspaces:

```bash
terraform workspace list
```

---

## 👨‍💻 Step 6: Developer Environment

Switch to **dev workspace**:

```bash
terraform workspace select dev
```

Apply Terraform:

```bash
terraform apply -var="instance_type=t2.micro"
```

### Result:

* EC2 instance created
* Name: `EC2-dev`
* Used by Developers

---

## 🧪 Step 7: Tester Environment

Switch to **test workspace**:

```bash
terraform workspace select test
```

Apply Terraform:

```bash
terraform apply -var="instance_type=t2.small"
```

### Result:

* EC2 instance created
* Name: `EC2-test`
* Used by QA team

---

## 🚀 Step 8: Production Environment

Switch to **prod workspace**:

```bash
terraform workspace select prod
```

Apply Terraform:

```bash
terraform apply -var="instance_type=t2.medium"
```

### Result:

* EC2 instance created
* Name: `EC2-prod`
* Production-ready server

---

## 🔍 Step 9: Verify in AWS Console

Go to **AWS EC2 Dashboard** and you will see:

* EC2-dev
* EC2-test
* EC2-prod

Each instance:

* Created using same Terraform code
* Managed by different workspace state

---

## 🧹 Step 10: Destroy a Specific Environment

Destroy **only developer resources**:

```bash
terraform workspace select dev
terraform destroy
```

✔ Test and Production are not affected

---

## ⚠️ Important Notes

* Workspaces isolate **state**, not code
* One workspace cannot see another
* Always check workspace before applying or destroying
* Use workspaces for:

  * dev / test / prod
  * teams or departments

---

# 🪣 Terraform Lab – Create S3 Bucket with Versioning

This lab shows how to **create an Amazon S3 bucket** and **enable versioning** using **Terraform**.

This guide is written for **beginners**, so every step is explained clearly and simply.

---

## 📁 Step 1: Create Project Folder

```bash
mkdir terraform-s3-versioning
cd terraform-s3-versioning
````

This folder will store all Terraform files.

---

## 📄 Step 2: Create `main.tf`

Create a file named **`main.tf`** and add the following code:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "my_bucket" {
  bucket = "shyamdevk-terraform-s3-versioning-001"
}

resource "aws_s3_bucket_versioning" "versioning" {
  bucket = aws_s3_bucket.my_bucket.id

  versioning_configuration {
    status = "Enabled"
  }
}
```

---

## 🔍 Code Explanation (Very Simple)

### 🔹 AWS Provider

```hcl
provider "aws" {
  region = "us-east-1"
}
```

* Tells Terraform to use AWS
* Resources will be created in `us-east-1`

---

### 🔹 S3 Bucket Creation

```hcl
resource "aws_s3_bucket" "my_bucket" {
  bucket = "shyamdevk-terraform-s3-versioning-001"
}
```

* Creates an S3 bucket
* Bucket name must be **globally unique**
* If name already exists, change the number (001 → 002)

---

### 🔹 Enable Versioning

```hcl
resource "aws_s3_bucket_versioning" "versioning" {
  bucket = aws_s3_bucket.my_bucket.id
```

* Links versioning to the created bucket

```hcl
  versioning_configuration {
    status = "Enabled"
  }
}
```

* Turns ON versioning
* Keeps all file versions

---

## 🚀 Step 3: Initialize Terraform

```bash
terraform init
```

This command:

* Downloads required AWS plugins
* Prepares Terraform to run

---

## 🏗 Step 4: Apply Terraform Code

```bash
terraform apply
```

Type **yes** when asked.

Terraform will:

* Create the S3 bucket
* Enable versioning

---

## 🔍 Step 5: Verify in AWS Console

1. Open **AWS Console**
2. Go to **S3**
3. Click your bucket name
4. Open **Properties**
5. Check **Bucket Versioning**
6. Status should show **Enabled**

---



