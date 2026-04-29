<p align="center">
  <img src="https://raw.githubusercontent.com/ahmadsheikhi89/devops-cli-text-processing-cheat-sheet/main/assets/banner.png"
       alt="DevOps CLI Text Processing Cheat Sheet Banner"
       width="100%" />
</p>

<h1 align="center">DevOps CLI Text Processing Cheat Sheet</h1>

<p align="center">
  Production-grade CLI text processing reference for DevOps, SRE, Linux, Kubernetes, Helm, CI/CD, and automation workflows.
</p>

<p align="center">
  <strong>grep</strong> •
  <strong>rg</strong> •
  <strong>jq</strong> •
  <strong>yq</strong> •
  <strong>sed</strong> •
  <strong>awk</strong> •
  <strong>fzf</strong> •
  <strong>perl</strong> •
  <strong>regex</strong>
</p>

---

## Overview

This repository is a practical, enterprise-friendly cheat sheet for daily DevOps operations, troubleshooting, Kubernetes workflows, Helm values management, CI/CD scripting, log analysis, and safe text processing on Linux systems.

It is designed to be useful for both learning and real production work.

The goal is not to memorize every command.

The goal is to build safe, reusable, and reliable command-line workflows.

---

## Target Audience

This repository is designed for:

- Junior DevOps Engineers
- Mid-level DevOps Engineers
- Senior DevOps Engineers
- Linux System Administrators
- Kubernetes Operators
- SRE / Platform Engineers
- CI/CD Engineers
- Infrastructure Automation Engineers

---

## Supported Environments

Designed for:

- Rocky Linux / RHEL
- Ubuntu / Debian
- On-premise environments
- Air-gapped environments
- Enterprise Linux platforms
- Kubernetes clusters
- Helm-based deployments
- GitLab CI/CD workflows

---

## Tool Coverage

| Tool | Purpose |
|---|---|
| `grep` | Basic text search |
| `rg` | Fast recursive search |
| `jq` | JSON parsing and transformation |
| `yq` | YAML parsing and modification |
| `fzf` | Interactive fuzzy selection |
| `sed` | Stream editing and replacement |
| `awk` | Column-based text processing |
| `perl` | Advanced regex and multiline editing |
| Regex | Pattern matching for logs, configs, and automation |
| Vim | Emergency editing on Linux servers |

---

## Recommended Repository Layout

```text
devops-cli-text-processing-cheat-sheet/
├── README.md
├── assets/
│   └── banner.png
├── cheatsheets/
│   ├── grep-rg.md
│   ├── jq-yq.md
│   ├── sed-awk-perl.md
│   ├── regex.md
│   └── kubernetes-workflows.md
├── examples/
│   ├── app.log
│   ├── pods.json
│   ├── values.yaml
│   └── deployment.yaml
├── scripts/
│   ├── install-tools-rocky.sh
│   ├── install-tools-ubuntu.sh
│   └── validate-tools.sh
└── LICENSE
```

---

# 1. Quick Start

Clone the repository:

```bash
git clone https://github.com/ahmadsheikhi89/devops-cli-text-processing-cheat-sheet.git
cd devops-cli-text-processing-cheat-sheet
```

Validate installed tools:

```bash
bash scripts/validate-tools.sh
```

Install tools on Rocky Linux / RHEL:

```bash
bash scripts/install-tools-rocky.sh
```

Install tools on Ubuntu / Debian:

```bash
bash scripts/install-tools-ubuntu.sh
```

---

# 2. Installation

## Rocky Linux / RHEL

```bash
sudo dnf install -y \
  grep \
  sed \
  gawk \
  perl \
  jq \
  ripgrep \
  fzf
```

This repository expects `mikefarah/yq` v4 syntax.

For air-gapped environments, install `yq` from an internally approved binary:

```bash
sudo install -m 0755 yq_linux_amd64 /usr/local/bin/yq
yq --version
```

Expected output:

```text
yq version v4.x.x
```

---

## Ubuntu / Debian

```bash
sudo apt update

sudo apt install -y \
  grep \
  sed \
  gawk \
  perl \
  jq \
  ripgrep \
  fzf
```

Install `mikefarah/yq` v4 from an internally approved binary:

```bash
sudo install -m 0755 yq_linux_amd64 /usr/local/bin/yq
yq --version
```

Expected output:

```text
yq version v4.x.x
```

---

## Air-Gapped Installation Notes

For enterprise or isolated environments:

1. Download approved RPM, DEB, or static binaries in a connected staging zone.
2. Upload artifacts to an internal repository such as Nexus.
3. Install only from internal trusted sources.
4. Validate versions after installation.
5. Avoid direct internet downloads from production servers.

Example internal repository structure:

```text
nexus.example.local/repository/linux-tools/ripgrep/
nexus.example.local/repository/linux-tools/yq/
nexus.example.local/repository/linux-tools/fzf/
```

---

# 3. Tool Validation

Run:

```bash
grep --version | head -n 1
rg --version | head -n 1
jq --version
yq --version
fzf --version
sed --version | head -n 1
awk --version | head -n 1
perl -v | head -n 2
```

Expected example:

```text
grep (GNU grep) 3.x
ripgrep 13.x.x
jq-1.6
yq version v4.x.x
0.x.x
sed (GNU sed) 4.x
GNU Awk 5.x.x
This is perl 5
```

---

# 4. Production Safety Rules

Before modifying files in production-like environments, follow these rules.

## Always Preview Before Applying Changes

Preview:

```bash
sed 's/old/new/g' config.yaml
```

Apply:

```bash
sed -i 's/old/new/g' config.yaml
```

---

## Always Create a Backup Before Inline Changes

```bash
cp values.yaml values.yaml.bak
```

---

## Always Validate the Difference

```bash
diff -u values.yaml.bak values.yaml
```

---

## Prefer Structured Tools for Structured Data

| Data Type | Recommended Tool |
|---|---|
| JSON | `jq` |
| YAML | `yq` |
| Plain text | `grep`, `rg`, `awk`, `sed` |
| Large recursive search | `rg` |
| Interactive selection | `fzf` |

---

## Avoid Manual Editing for Large YAML Files

Prefer:

```text
yq
helm
kubectl patch
kubectl set image
kustomize
```

Instead of manually scrolling through large files.

---

# 5. grep

## Purpose

`grep` searches text in files and command output.

It is commonly used for:

- Log filtering
- Quick config checks
- Pipeline filtering
- Basic operational troubleshooting

---

## Basic Search

```bash
grep "error" app.log
```

---

## Case-Insensitive Search

```bash
grep -i "error" app.log
```

---

## Show Line Numbers

```bash
grep -n "error" app.log
```

---

## Recursive Search

```bash
grep -r "nginx" .
```

---

## Count Matching Lines

```bash
grep -c "error" app.log
```

---

## Show Only Matching Files

```bash
grep -rl "prometheus" .
```

---

## Exclude Directory

```bash
grep -r "password" . --exclude-dir=.git
```

---

## Search Multiple Patterns

```bash
grep -E "error|failed|timeout" app.log
```

---

## Show Lines Before and After Match

```bash
grep -C 3 "timeout" app.log
```

---

## Kubernetes Example

```bash
kubectl get pods -A | grep prometheus
```

---

# 6. ripgrep / rg

## Purpose

`ripgrep` is a modern, fast replacement for recursive `grep`.

It is recommended for:

- Searching large repositories
- Searching Kubernetes manifests
- Searching Helm charts
- Searching CI/CD files
- Searching logs and configuration trees

---

## Basic Search

```bash
rg "image"
```

---

## Search Specific File Type

```bash
rg "replicas" -g '*.yaml'
```

---

## Ignore Case

```bash
rg -i "error"
```

---

## List Matching Files

```bash
rg -l "grafana"
```

---

## Show Line Numbers

```bash
rg -n "timeout" app.log
```

---

## Search Hidden Files

```bash
rg "token" --hidden
```

---

## Search Hidden Files and Ignore `.git`

```bash
rg "password" --hidden -g '!.git'
```

---

## Search Kubernetes Manifests

```bash
rg "kind: Deployment" .
```

```bash
rg "image:" .
```

```bash
rg "resources:" .
```

---

## Kubernetes Runtime Example

```bash
kubectl get pods -A | rg nginx
```

---

# 7. jq

## Purpose

`jq` parses, filters, and transforms JSON safely.

It is essential for:

- Kubernetes JSON output
- API responses
- CI/CD metadata
- Docker inspect output
- Terraform/OpenTofu JSON output
- Monitoring and alert payloads

---

## Pretty Print JSON

```bash
jq . data.json
```

---

## Extract a Field

```bash
jq -r '.metadata.name' pod.json
```

---

## Extract Array Items

```bash
jq -r '.items[].metadata.name' pods.json
```

---

## Kubernetes: Get Pod Names

```bash
kubectl get pods -A -o json |
jq -r '.items[].metadata.name'
```

---

## Kubernetes: Get Namespace and Pod Name

```bash
kubectl get pods -A -o json |
jq -r '.items[] | [.metadata.namespace, .metadata.name] | @tsv'
```

---

## Kubernetes: Get Container Images

```bash
kubectl get pods -A -o json |
jq -r '.items[] | .spec.containers[].image'
```

---

## Kubernetes: Get Pod, Namespace, Container, and Image

```bash
kubectl get pods -A -o json |
jq -r '
  .items[]
  | . as $pod
  | .spec.containers[]
  | [$pod.metadata.namespace, $pod.metadata.name, .name, .image]
  | @tsv
'
```

---

## Kubernetes: Get Node Names

```bash
kubectl get nodes -o json |
jq -r '.items[].metadata.name'
```

---

## Docker: Inspect Container IP Address

```bash
docker inspect my-container |
jq -r '.[0].NetworkSettings.IPAddress'
```

---

## Docker: List Container Names, Images, and Status

```bash
docker ps --format '{{json .}}' |
jq -r '[.Names, .Image, .Status] | @tsv'
```

---

# 8. yq

## Purpose

`yq` parses and modifies YAML safely.

This repository uses `mikefarah/yq` v4 syntax.

Validate:

```bash
yq --version
```

Expected:

```text
yq version v4.x.x
```

---

## Read Value

```bash
yq '.image.tag' values.yaml
```

---

## Read Value as Raw Text

```bash
yq -r '.image.tag' values.yaml
```

---

## Update Value In Place

```bash
yq -i '.image.tag = "1.25"' values.yaml
```

---

## Update Replica Count

```bash
yq -i '.replicaCount = 3' values.yaml
```

---

## Extract Service Type

```bash
yq -r '.service.type' values.yaml
```

---

## Kubernetes: Read Deployment Image

```bash
yq -r '.spec.template.spec.containers[0].image' deployment.yaml
```

---

## Kubernetes: Change Deployment Image

```bash
yq -i '.spec.template.spec.containers[0].image = "nginx:1.27"' deployment.yaml
```

---

## Helm: Update Values Safely

Preview:

```bash
yq '.replicaCount = 3' values.yaml
```

Backup:

```bash
cp values.yaml values.yaml.bak
```

Apply:

```bash
yq -i '.replicaCount = 3' values.yaml
```

Validate:

```bash
diff -u values.yaml.bak values.yaml
```

---

# 9. fzf

## Purpose

`fzf` is an interactive fuzzy finder.

It is useful for:

- Selecting files
- Selecting pods
- Selecting namespaces
- Selecting logs
- Selecting command history
- Reducing typing errors during operations

---

## Basic Usage

```bash
history | fzf
```

---

## Search Files

```bash
find . -type f | fzf
```

---

## Open Selected File in Vim

```bash
vim "$(find . -type f | fzf)"
```

---

## Kubernetes: Select a Pod

```bash
kubectl get pods -A | fzf
```

---

## Kubernetes: Tail Logs from Selected Pod

```bash
read ns pod < <(
  kubectl get pods -A --no-headers |
  fzf |
  awk '{print $1, $2}'
)

kubectl -n "$ns" logs -f "$pod"
```

---

## Kubernetes: Exec into Selected Pod

```bash
read ns pod < <(
  kubectl get pods -A --no-headers |
  fzf |
  awk '{print $1, $2}'
)

kubectl -n "$ns" exec -it "$pod" -- sh
```

---

## Kubernetes: Describe Selected Pod

```bash
read ns pod < <(
  kubectl get pods -A --no-headers |
  fzf |
  awk '{print $1, $2}'
)

kubectl -n "$ns" describe pod "$pod"
```

---

# 10. sed

## Purpose

`sed` is a stream editor used for search, replace, deletion, and line-based transformations.

It is commonly used in:

- Config updates
- CI/CD scripts
- Template adjustments
- Log cleanup
- Simple automation

---

## Basic Replace

```bash
sed 's/old/new/' file
```

---

## Replace Globally Per Line

```bash
sed 's/old/new/g' file
```

---

## Edit File Inline

```bash
sed -i 's/nginx/apache/g' config.yaml
```

---

## Replace Only on a Specific Line

```bash
sed -i '5s/old/new/' file
```

---

## Delete Matching Lines

```bash
sed '/DEBUG/d' app.log
```

---

## Print Specific Line

```bash
sed -n '10p' file
```

---

## Print Line Range

```bash
sed -n '10,30p' file
```

---

## Production-Safe Replace Workflow

Preview:

```bash
sed 's/old/new/g' file
```

Backup:

```bash
cp file file.bak
```

Apply:

```bash
sed -i 's/old/new/g' file
```

Validate:

```bash
diff -u file.bak file
```

---

# 11. awk

## Purpose

`awk` is used for column-based text processing.

It is powerful for:

- Extracting columns
- Filtering command output
- Summarizing logs
- Processing tabular CLI output
- Building quick operational reports

---

## Print First Column

```bash
awk '{print $1}' file
```

---

## Print Multiple Columns

```bash
awk '{print $1, $3}' file
```

---

## Filter Rows

```bash
awk '$3 > 100' file
```

---

## Skip Header

```bash
awk 'NR>1 {print $1, $2}' file
```

---

## Kubernetes: Get Namespaces Only

```bash
kubectl get pods -A |
awk 'NR>1 {print $1}' |
sort -u
```

---

## Kubernetes: Get Pod Names Only

```bash
kubectl get pods -A |
awk 'NR>1 {print $2}'
```

---

## Kubernetes: Find Pods with Restarts

```bash
kubectl get pods -A |
awk 'NR>1 && $5 > 0 {print $1, $2, $5}'
```

---

## Docker: Show Container Names

```bash
docker ps |
awk 'NR>1 {print $NF}'
```

---

# 12. perl

## Purpose

`perl` is useful for advanced text manipulation, complex regex, and multiline replacement.

It is less common in modern day-to-day DevOps work, but still very powerful.

---

## Replace Text In Place

```bash
perl -pi -e 's/old/new/g' file
```

---

## Match Lines

```bash
perl -ne 'print if /error/' app.log
```

---

## Case-Insensitive Match

```bash
perl -ne 'print if /error/i' app.log
```

---

## Multiline Replace

```bash
perl -0777 -pi -e 's/foo\nbar/baz/g' file
```

---

## Extract IP Addresses

```bash
perl -ne 'print "$1\n" if /(\b(?:[0-9]{1,3}\.){3}[0-9]{1,3}\b)/' app.log
```

---

# 13. Advanced Regex

## Important Regex Note

Regex syntax is not identical across all tools.

| Tool | Regex Style |
|---|---|
| `grep` | Basic Regex by default |
| `grep -E` | Extended Regex |
| `grep -P` | PCRE, if supported |
| `rg` | Modern regex engine |
| `awk` | Extended Regex style |
| `perl` | Perl-compatible regex |

For portable digit matching in shell tools, prefer:

```regex
[[:digit:]]+
```

Instead of:

```regex
\d+
```

---

## Match Digits

Portable:

```regex
[[:digit:]]+
```

PCRE-style:

```regex
\d+
```

---

## Match IPv4 Address

```regex
\b(?:[0-9]{1,3}\.){3}[0-9]{1,3}\b
```

Example with `rg`:

```bash
rg '\b(?:[0-9]{1,3}\.){3}[0-9]{1,3}\b' app.log
```

---

## Match Email Address

```regex
[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}
```

Example:

```bash
rg '[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}' app.log
```

---

## Match Kubernetes Resource Name

```regex
[a-z0-9]([-a-z0-9]*[a-z0-9])?
```

---

## Match YAML Key

```regex
^\s*[a-zA-Z0-9_-]+:
```

Example:

```bash
rg '^\s*[a-zA-Z0-9_-]+:' values.yaml
```

---

# 14. Kubernetes and Helm Real Workflows

## Find CrashLoopBackOff Pods

```bash
kubectl get pods -A | rg CrashLoopBackOff
```

---

## Find Pending Pods

```bash
kubectl get pods -A | rg Pending
```

---

## Find Restarting Pods

```bash
kubectl get pods -A |
awk 'NR>1 && $5 > 0 {print $1, $2, $5}'
```

---

## Get All Pod Images

```bash
kubectl get pods -A -o json |
jq -r '
  .items[]
  | . as $pod
  | .spec.containers[]
  | [$pod.metadata.namespace, $pod.metadata.name, .name, .image]
  | @tsv
'
```

---

## Search Ingress Definitions

```bash
rg "kind: Ingress" .
```

---

## Search LoadBalancer Services

```bash
kubectl get svc -A | rg LoadBalancer
```

---

## Update Helm Replica Count

```bash
cp values.yaml values.yaml.bak
yq -i '.replicaCount = 3' values.yaml
diff -u values.yaml.bak values.yaml
```

---

## Render Helm Template and Search Output

```bash
helm template my-release ./chart -f values.yaml |
rg "image:"
```

---

## Render Helm Template and Validate YAML

```bash
helm template my-release ./chart -f values.yaml > /tmp/rendered.yaml
yq '.' /tmp/rendered.yaml >/dev/null
```

---

## Interactive Pod Logs

```bash
read ns pod < <(
  kubectl get pods -A --no-headers |
  fzf |
  awk '{print $1, $2}'
)

kubectl -n "$ns" logs -f "$pod"
```

---

# 15. Helm Values Operations

## Read Image Repository

```bash
yq -r '.image.repository' values.yaml
```

---

## Read Image Tag

```bash
yq -r '.image.tag' values.yaml
```

---

## Update Image Tag

```bash
cp values.yaml values.yaml.bak
yq -i '.image.tag = "1.2.3"' values.yaml
diff -u values.yaml.bak values.yaml
```

---

## Update Resource Requests

```bash
yq -i '.resources.requests.cpu = "250m"' values.yaml
yq -i '.resources.requests.memory = "256Mi"' values.yaml
```

---

## Update Resource Limits

```bash
yq -i '.resources.limits.cpu = "500m"' values.yaml
yq -i '.resources.limits.memory = "512Mi"' values.yaml
```

---

## Validate Rendered Manifest

```bash
helm template app ./chart -f values.yaml > /tmp/app-rendered.yaml
yq '.' /tmp/app-rendered.yaml >/dev/null
```

---

# 16. Log Investigation Workflows

## Search for Errors

```bash
rg -i "error|failed|timeout|exception" app.log
```

---

## Count Error Lines

```bash
rg -i "error" app.log | wc -l
```

---

## Show Context Around Match

```bash
grep -i -C 3 "timeout" app.log
```

---

## Extract IP Addresses from Logs

```bash
rg -o '\b(?:[0-9]{1,3}\.){3}[0-9]{1,3}\b' app.log | sort -u
```

---

## Top Repeated IP Addresses

```bash
rg -o '\b(?:[0-9]{1,3}\.){3}[0-9]{1,3}\b' app.log |
sort |
uniq -c |
sort -nr |
head
```

---

# 17. CI/CD Useful Patterns

## Extract Docker Image from YAML

```bash
yq -r '.spec.template.spec.containers[0].image' deployment.yaml
```

---

## Validate JSON File

```bash
jq . config.json >/dev/null
```

---

## Validate YAML File

```bash
yq . values.yaml >/dev/null
```

---

## Find Dockerfiles in Repository

```bash
find . -name Dockerfile -type f
```

---

## Search CI/CD Variables

```bash
rg "NEXUS|REGISTRY|IMAGE|DEPLOY|TOKEN|PASSWORD" .gitlab-ci.yml
```

---

## Search Hardcoded Secrets Carefully

```bash
rg -i "password|secret|token|apikey|api_key" --hidden -g '!.git'
```

---

# 18. Vim Survival Guide for DevOps

## Open File

```bash
vim values.yaml
```

---

## Insert Mode

```text
i
```

---

## Exit Insert Mode

```text
ESC
```

---

## Save and Quit

```text
:wq
```

---

## Quit Without Saving

```text
:q!
```

---

## Search

```text
/error
```

Next match:

```text
n
```

Previous match:

```text
N
```

---

## Go to Line

```text
:120
```

---

## Replace in Entire File

```text
:%s/old/new/g
```

---

## Show Line Numbers

```text
:set number
```

---

# 19. Useful Aliases

Add to `~/.bashrc` or `~/.zshrc`:

```bash
alias k='kubectl'
alias kgp='kubectl get pods'
alias kgs='kubectl get svc'
alias kgn='kubectl get nodes'
alias kga='kubectl get all'
alias d='docker'
alias dc='docker compose'
alias h='history'
```

Reload shell configuration:

```bash
source ~/.bashrc
```

Or:

```bash
source ~/.zshrc
```

---

# 20. Recommended Learning Path

## Beginner

Start with:

```text
grep
rg
fzf
vim basics
```

Goal:

```text
Search logs, find files, inspect command output, edit emergency configs.
```

---

## Intermediate

Continue with:

```text
jq
yq
sed
awk
```

Goal:

```text
Parse JSON/YAML, update configs safely, process CLI output.
```

---

## Advanced

Then learn:

```text
perl
advanced regex
complex jq filters
multiline processing
automation scripts
```

Goal:

```text
Build reliable, repeatable, production-safe operational workflows.
```

---

# 21. Enterprise DevOps Mindset

The goal is not to memorize every command.

The goal is to build reliable workflows.

A strong DevOps Engineer:

- reuses proven snippets
- validates before applying changes
- backs up important files
- avoids manual risky edits
- uses structured tools for structured data
- automates repetitive work
- reduces cognitive load during incidents
- documents reusable operational patterns

---

# 22. Recommended Daily Stack

## Core Tools

```text
grep
rg
jq
yq
fzf
```

## Important Tools

```text
sed
awk
vim
```

## Advanced Tools

```text
perl
advanced regex
complex jq/yq expressions
```

---

# 23. Suggested Next Topics

After mastering this cheat sheet, continue with:

- Kubernetes debugging
- Helm templating
- Kustomize
- ArgoCD GitOps
- GitLab CI/CD
- Prometheus alerting
- Loki log queries
- Terraform / OpenTofu
- Kyverno policies
- Container image scanning
- Linux troubleshooting

---

# 24. Example Script: validate-tools.sh

Create:

```bash
mkdir -p scripts
vim scripts/validate-tools.sh
```

Content:

```bash
#!/usr/bin/env bash
set -euo pipefail

REQUIRED_TOOLS=(
  grep
  sed
  awk
  perl
  jq
  rg
  yq
  fzf
)

echo "Validating required CLI tools..."
echo

for tool in "${REQUIRED_TOOLS[@]}"; do
  if command -v "$tool" >/dev/null 2>&1; then
    printf "[OK]      %s -> %s\n" "$tool" "$(command -v "$tool")"
  else
    printf "[MISSING] %s\n" "$tool"
  fi
done

echo
echo "Version details:"
echo "----------------"

grep --version | head -n 1 || true
sed --version | head -n 1 || true
awk --version | head -n 1 || true
perl -v | head -n 2 || true
jq --version || true
rg --version | head -n 1 || true
yq --version || true
fzf --version || true
```

Make it executable:

```bash
chmod +x scripts/validate-tools.sh
```

Run:

```bash
bash scripts/validate-tools.sh
```

---

# 25. Example Script: install-tools-rocky.sh

Create:

```bash
vim scripts/install-tools-rocky.sh
```

Content:

```bash
#!/usr/bin/env bash
set -euo pipefail

sudo dnf install -y \
  grep \
  sed \
  gawk \
  perl \
  jq \
  ripgrep \
  fzf

echo "Base tools installed."

if ! command -v yq >/dev/null 2>&1; then
  echo "yq is not installed."
  echo "Install mikefarah/yq v4 from your approved internal binary repository."
  echo "Example:"
  echo "sudo install -m 0755 yq_linux_amd64 /usr/local/bin/yq"
fi
```

Make it executable:

```bash
chmod +x scripts/install-tools-rocky.sh
```

---

# 26. Example Script: install-tools-ubuntu.sh

Create:

```bash
vim scripts/install-tools-ubuntu.sh
```

Content:

```bash
#!/usr/bin/env bash
set -euo pipefail

sudo apt update

sudo apt install -y \
  grep \
  sed \
  gawk \
  perl \
  jq \
  ripgrep \
  fzf

echo "Base tools installed."

if ! command -v yq >/dev/null 2>&1; then
  echo "yq is not installed."
  echo "Install mikefarah/yq v4 from your approved internal binary repository."
  echo "Example:"
  echo "sudo install -m 0755 yq_linux_amd64 /usr/local/bin/yq"
fi
```

Make it executable:

```bash
chmod +x scripts/install-tools-ubuntu.sh
```

---

# 27. Git Workflow

Initialize repository:

```bash
git init
git add README.md assets/ scripts/
git commit -m "docs: add production-grade DevOps text processing cheat sheet"
```

Add remote:

```bash
git remote add origin https://github.com/ahmadsheikhi89/devops-cli-text-processing-cheat-sheet.git
```

Push:

```bash
git branch -M main
git push -u origin main
```

---

# 28. Suggested GitHub Repository Description

```text
Production-grade CLI text processing cheat sheet for DevOps, SRE, Linux, Kubernetes, Helm, jq, yq, grep, rg, sed, awk, perl, fzf, and regex workflows.
```

---

# Final Principle

```text
Do not just run commands.
Understand the input, transform it safely, validate the output, then apply the change.
```
