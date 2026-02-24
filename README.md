# Secure Static Website Infrastructure (AWS | Terraform)

## Project Summary

Designed and deployed a production-pattern static website architecture using AWS and Terraform, emphasizing security, repeatability, and infrastructure-as-code best practices. The solution eliminates public S3 exposure and enforces least-privilege access through CloudFront Origin Access Control (OAC).

This project demonstrates practical cloud engineering skills including secure architecture design, CDN integration, state management, and deterministic infrastructure deployments.

---

## Architecture Overview

- **Amazon S3** – Private object storage (Block Public Access enabled)
- **CloudFront** – Global CDN with HTTPS enforcement
- **Origin Access Control (OAC)** – Restricts S3 access exclusively to CloudFront
- **Terraform** – Infrastructure as Code for reproducible deployments
- **Git** – Version-controlled workflow

---

## Security & Design Principles

- Zero public S3 exposure
- Least-privilege bucket policy scoped to CloudFront service principal
- HTTPS-only delivery enforced at CDN layer
- Deterministic file updates using content hashing (`filemd5`)
- No manual AWS Console configuration (fully IaC-managed)

---

## Key Implementation Detail

Content-based redeployment detection:

```hcl
etag = filemd5("website/index.html")
