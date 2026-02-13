---
title:  "Azure Migrate and CMK: Secure Migrations from Day One."
category: code
collection: code
tags: AzureMigrate CMK Encryption Security
header:
  teaser: "/assets/images/Binary-Code-RLC-500x300.png"
---

### Introduction and Point-of-view.
As a Cloud Consultant, I help organizations transition to the cloud on a daily basis. A question that comes up more and more often — especially in regulated industries like healthcare, finance, and government — is: "How do we make sure our data is encrypted with our own keys, right from the start?"

This is a valid concern. By default, Azure encrypts all managed disk data at rest using **Platform Managed Keys** (PMK). Microsoft manages these keys on your behalf, which is perfectly secure in most scenarios. But for organizations with strict compliance requirements, this is simply not enough. Enter **Customer Managed Keys** (CMK) — and the good news is that Azure Migrate now supports migrating VMs directly to a CMK-encrypted configuration, so you don't have to choose between speed and security.

### What is the difference between PMK and CMK?
Before diving into the migration process, it's worth understanding what we are actually talking about.

With **Platform Managed Keys**, Azure handles the entire encryption key lifecycle. Microsoft generates, stores, rotates, and manages the keys used to encrypt your data. You don't have to think about it — and that is exactly the problem for some organizations.

With **Customer Managed Keys**, you bring your own key stored in **Azure Key Vault**. You are in full control: you decide when to rotate, who has access, and what happens when a key is revoked. If you revoke access to your key, VMs encrypted with that key will stop functioning — which is a powerful lever in a security or compliance incident. Think of it as the difference between renting a safety deposit box where the bank holds a master key versus one where only you have the key.

>For organizations subject to regulations like ISO 27001, NEN 7510, or GDPR, CMK is often not just a preference but a hard requirement. The ability to demonstrate full control over your encryption keys is increasingly expected by auditors.

This is where the integration between **Azure Migrate** and CMK becomes particularly powerful.

### How does it work in Azure Migrate?
The **Migration and modernization** tool within Azure Migrate supports agentless replication of VMware VMs to Azure with CMK-encrypted disks. The portal experience itself supports the Disk Encryption Set (DES) / CMK configuration, meaning you can set this up from the Azure Portal without writing a single line of PowerShell — though the ARM template approach remains available for more advanced scenarios.

There are a few things to understand before you start:

* **Disk Encryption Set (DES):** This is the Azure object that links your managed disks to the Key Vault containing your CMK. You need to create this before starting replication — it cannot be applied at the time of migration, only at the start of replication.
* **Azure Key Vault:** Your CMK must be stored here (or in Azure Key Vault Managed HSM for HSM-protected keys). Soft delete and purge protection must be enabled on the Key Vault.
* **Double encryption:** You can optionally configure the DES for double encryption — layering a customer-managed key on top of the default platform-managed key — for the highest possible level of compliance assurance.

The migration process then uses server-side encryption (SSE) to encrypt the replicated managed disks as they land in Azure. The data travels over HTTPS with TLS 1.2 or later, and the moment those disks are written, they are encrypted using your CMK.

### What I have learned.
Security and migration are often treated as sequential steps — first migrate, then secure. This approach creates a window of risk that is hard to justify to an auditor or a CISO. The ability to configure CMK directly within the Azure Migrate replication flow closes that gap.

The most important lesson I take from this in practice: **prepare your Key Vault and Disk Encryption Set before you start the project.** It sounds obvious, but the DES must exist and be correctly configured before replication begins. A last-minute scramble to get the right permissions in place — especially in environments with strict RBAC policies — can delay a migration significantly.

Another thing worth noting is that Azure Disk Encryption (ADE), which uses BitLocker or dm-crypt at the OS level, is a different feature and the two are not interchangeable. If a VM is currently protected with ADE, it cannot be directly migrated to SSE with CMK. In those cases, you will need to plan accordingly.

The bottom line: with CMK support in Azure Migrate, there is no longer a reason to make a trade-off between migration speed and encryption compliance. Done right, your workloads land in Azure already secured under your own keys — from day one.
