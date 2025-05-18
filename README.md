# tfiam

**tfiam** is a CLI tool that helps you analyze and manage AWS IAM permissions required to deploy Terraform manifests. It enables teams to ensure least privilege access by checking IAM roles against Terraform plan requirements — and in the future, it will dynamically grant and revoke temporary permissions during apply.

---

## 🚀 Features (Current & Roadmap)

### ✅ Current (MVP)
- Analyze `terraform plan` output (`-json`) to detect AWS resource operations
- Determine required IAM permissions for those resources
- Compare required permissions with an existing IAM role
- Print missing or insufficient permissions

### 🔜 Planned
- Temporarily grant missing permissions to a role before `terraform apply`
- Automatically revoke non-default permissions after apply
- Support allowlists, default policy baselines, and GitHub Actions
- Integrate with policy-as-code (OPA/Conftest)
- `diff`, `revoke`, and `grant` subcommands

---

## 🛠️ Installation

**(Coming soon)** via:
- Homebrew
- Prebuilt binaries on GitHub Releases
- Docker image

---

## 💡 Usage

```bash
# Check required permissions from a Terraform plan
terraform show -json tfplan > tfplan.json
tfiam check --plan tfplan.json --role my-deployer-role
```

## Sample Output

```txt
Missing permissions for role: arn:aws:iam::123456789012:role/my-deployer-role

Required:
- s3:CreateBucket
- s3:PutBucketTagging
- iam:PassRole

Granted:
- s3:CreateBucket

Suggestions:
Attach the following permissions or use `tfiam grant` (coming soon):
[
  "s3:PutBucketTagging",
  "iam:PassRole"
]
```

## 🔐 Why tfiam?

Terraform is powerful, but managing AWS IAM permissions manually is error-prone:

•	🛑 Missing permissions are only discovered at apply time

•	🧪 CI/CD pipelines often need elevated permissions temporarily

•	✅ tfiam helps validate before apply — and in the future, can grant just enough permissions, just in time


## 🤝 Contributing

Contributions, ideas, and feedback are welcome!

See CONTRIBUTING.md (coming soon) for how to get involved.

## 📜 License

MIT

