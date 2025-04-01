![](https://img.shields.io/github/commit-activity/t/subhamay-bhattacharyya-gha/cfn-validate-scan-action)&nbsp;![](https://img.shields.io/github/last-commit/subhamay-bhattacharyya-gha/cfn-validate-scan-action)&nbsp;![](https://img.shields.io/github/release-date/subhamay-bhattacharyya-gha/cfn-validate-scan-action)&nbsp;![](https://img.shields.io/github/repo-size/subhamay-bhattacharyya-gha/cfn-validate-scan-action)&nbsp;![](https://img.shields.io/github/directory-file-count/subhamay-bhattacharyya-gha/cfn-validate-scan-action)&nbsp;![](https://img.shields.io/github/issues/subhamay-bhattacharyya-gha/cfn-validate-scan-action)&nbsp;![](https://img.shields.io/github/languages/top/subhamay-bhattacharyya-gha/cfn-validate-scan-action)&nbsp;![](https://img.shields.io/github/commit-activity/m/subhamay-bhattacharyya-gha/cfn-validate-scan-action)&nbsp;![](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/bsubhamay/eaa9233256e4cffdc5496854b34451c0/raw/cfn-validate-scan-action.json?)

# 🚀 Scan and Validate

**Scan and Validate** is a GitHub Composite Action that validates AWS CloudFormation templates and optionally runs a [Checkov](https://www.checkov.io/) scan for security and compliance issues.

---

## 🔍 What It Does

1. **Assumes an AWS IAM Role** using GitHub OIDC.
2. **Validates** the specified CloudFormation template.
3. **Runs Checkov** scan on supported IaC frameworks (CloudFormation, Terraform, Kubernetes, or all).

---

## 📦 Inputs

| Name            | Description                                                                 | Required | Default                                                             |
|-----------------|-----------------------------------------------------------------------------|----------|---------------------------------------------------------------------|
| `aws-role-arn`  | ARN of the IAM role to assume.                                              | ✅ Yes   | `arn:aws:iam::111122223333:role/github-oidc-role`                  |
| `aws-region`    | AWS region where resources are deployed.                                    | ✅ Yes   | `us-east-1`                                                         |
| `template-dir`  | Directory path where the IaC template is located.                           | ✅ Yes   | `cfn`                                                               |
| `template-file` | IaC template file name to validate.                                         | ✅ Yes   | `root-stack-template.yaml`                                         |
| `iac-framework` | IaC framework for Checkov (`cloudformation`, `terraform`, `kubernetes`, `all`). | ✅ Yes   | `cloudformation`                                                    |
| `soft-fail`     | If `true`, Checkov scan failures will not fail the pipeline.                | ✅ Yes   | `true`                                                              |
| `github-token`  | GitHub token for authenticating the workflow.                              | ✅ Yes   |                                                                     |

---

## 📤 Outputs

| Name                | Description                              |
|---------------------|------------------------------------------|
| `valid-template`    | `true` if the template is valid          |
| `validation-error`  | Validation error message, if any         |

---

## 🛠 Usage Example

```yaml
jobs:
  validate-template:
    runs-on: ubuntu-latest
    steps:
      - name: Scan and validate CloudFormation
        uses: your-org/scan-and-validate@v1
        with:
          aws-role-arn: arn:aws:iam::111122223333:role/github-oidc-role
          aws-region: us-east-1
          template-dir: cfn
          template-file: root-stack-template.yaml
          iac-framework: cloudformation
          soft-fail: true
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

## License

MIT