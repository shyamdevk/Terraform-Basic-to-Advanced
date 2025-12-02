
# 🌍 **Terraform Basics**

A clean and simple guide to understanding **IaC** and **Terraform** for beginners.
![Terraform GIF](terraform.gif)


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
  provider = aws.mumbai
  bucket   = "my-bucket-mumbai-demo123"
}
```

---


