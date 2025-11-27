
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

---



