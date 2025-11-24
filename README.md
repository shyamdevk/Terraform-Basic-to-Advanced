
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


