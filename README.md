# Setup DOX CLI
Install and configure **DOX CLI** on GitHub Actions runners.  
After this step, `dox` is available for all workflow steps.
More details: [DOX CLI GitHub](https://github.com/dopxlab/dox-cli)

---

## 🚀 Quick Start

Get started with DOX CLI in seconds:

```yaml
- name: Setup DOX CLI
  uses: dopxlab/setup-dox-cli@v1

- name: Install tools
  run: dox config terraform kubectl helm
```

That's it! Your tools are ready to use.

### 🔗 Chain Dependencies

DOX automatically handles tool dependencies. For example, `maven-gvm` will automatically install `jdk-gvm`:

```bash
dox config maven-gvm
```

This single command installs both Maven and JDK with GraalVM support - perfect for building GraalVM native images!

<details>
<summary>📋 Click to see example output</summary>

```
dox@M-C12345 ~ % dox config maven-gvm
▶️ DOX CLI running... Action: config; Arguments: maven-gvm
--------------------------------------------------
DOX_CLI_VERSION           : v4.1.1
DOX_DIR                   : /Users/joby/.dox
DOX_CUSTOM_DIR            : /Users/joby/.dox/customize
DOX_RESOURCES_DIR         : /Users/joby/dox_resources
--------------------------------------------------
✓ Using  JDK_VERSION_GVM=jdk-25.0.2
⬇ Downloading graalvm-community-jdk-25.0.2_macos-aarch64_bin.tar.gz from https://github.com/graalvm/graalvm-ce-builds/releases/download/jdk-25.0.2/graalvm-community-jdk-25.0.2_macos-aarch64_bin.tar.gz
✓ Moved Contents/Home to /Users/joby/dox_resources/jdk-gvm/jdk-25.0.2
✓ Configuring jdk-gvm jdk-25.0.2
✓ Using  MAVEN_VERSION=3.9.12
⬇ Downloading apache-maven-3.9.12-bin.tar.gz from https://dlcdn.apache.org/maven/maven-3/3.9.12/binaries/apache-maven-3.9.12-bin.tar.gz
✓ Configuring maven-gvm 3.9.12
✓ Environment loaded. Variables are now available in this shell. To use in new shells, run:
   source ./dox_env
✓ Environment variables loaded into current shell
```

</details>

---

## 📖 What is DOX CLI?

**DOX** is a universal tool installer and environment manager that simplifies DevOps workflows. Instead of manually installing and configuring multiple tools (terraform, kubectl, aws-cli, etc.) across different environments, DOX automates the entire process with a single command.

### Why use DOX?

* **Consistency** - Ensure the same tool versions across all environments  
* **Speed** - Install multiple tools with one command or config file  
* **Simplicity** - No more writing complex installation scripts  
* **Caching** - Download once, reuse across builds  
* **Declarative** - Define your toolchain in YAML  
* **Version Control** - Pin specific versions or use latest  
* **Automatic Dependencies** - Chain dependencies are resolved automatically

Perfect for CI/CD pipelines, development environments, and containerized workflows.

---

## 📋 Few Available Tools and Configurations (Customizable & Extensible)

| # | Tool | Environment Variable Override | Example Version |
|---|------|------------------------------|-----------------|
| 1 | angular | ANGULAR_VERSION | 21.1.2 |
| 2 | argocd | ARGOCD_VERSION | v3.3.0 |
| 3 | aws | - | latest |
| 4 | az | AZ_VERSION | 2.82.0 |
| 5 | buildkit | BUILDKIT_VERSION | v0.27.1 |
| 6 | conftest | CONF_TEST_VERSION | 0.66.0 |
| 7 | cosign | COSIGN_VERSION | 3.0.4 |
| 8 | docker-buildx | DOCKER_BUILDX_VERSION | 0.31.1 |
| 9 | docker | DOCKER_CLI_VERSION | 29.2.0 |
| 10 | go | GO_VERSION | 1.25.6 |
| 11 | gradle | GRADLE_VERSION | 9.3.1 |
| 12 | grype | GRYPE_VERSION | 0.107.0 |
| 13 | helm | HELM_VERSION | v4.1.0 |
| 14 | helmfile | HELMFILE_VERSION | 0.144.0 |
| 15 | jdk-gvm | JDK_VERSION_GVM | jdk-25.0.2 |
| 16 | jdk | JDK_VERSION | 25 |
| 17 | jreleaser | JRELEASER_VERSION | 1.22.0 |
| 18 | k3d | K3D_VERSION | 5.8.3 |
| 19 | k9s | K9S_VERSION | v0.50.18 |
| 20 | kind | KIND_VERSION | 0.31.0 |
| 21 | kubectl | KUBECTL_VERSION | v1.35.0 |
| 22 | kubectx | KUBECTX_VERSION | 0.9.5 |
| 23 | kubedns | KUBENS_VERSION | 0.9.5 |
| 24 | kubeseal | KUBESEAL_VERSION | 0.34.0 |
| 25 | kustomize | KUSTOMIZE_VERSION | v5.8.0 |
| 26 | maven-gvm | MAVEN_VERSION | 3.9.12 |
| 27 | maven | MAVEN_VERSION | 3.9.12 |
| 28 | node | NODE_VERSION | v25.5.0 |
| 29 | opa | OPA_VERSION | 1.13.1 |
| 30 | python | PYTHON_BUILD_VERSION | 20260127 |
| 31 | slsa-verifier | SLSA_VERIFIER_VERSION | 2.7.1 |
| 32 | sonar-scanner | SONAR_SCANNER_VERSION | 8.0.1.6346 |
| 33 | syft | SYFT_VERSION | 1.41.1 |
| 34 | terraform | TERRAFORM_VERSION | 1.14.4 |
| 35 | tfsec | TFSEC_VERSION | 1.28.14 |
| 36 | trivy | TRIVY_VERSION | 0.69.0 |
| 37 | yarn | YARN_VERSION | 1.22.22 |

### Version Configuration Approaches

**Approach 1: Environment Variables**
```yaml
- name: Setup DOX CLI
  uses: dopxlab/setup-dox-cli@v1
- name: Configure tools with specific versions
  env:
    TERRAFORM_VERSION: 1.14.4
    KUBECTL_VERSION: v1.35.0
    HELM_VERSION: v4.1.0
  run: dox config terraform kubectl helm
```

**Approach 2: tools.yaml Configuration**
```yaml
# tools.yaml
terraform: 1.14.4
kubectl: v1.35.0
helm: v4.1.0
go: 1.25.6
python: 20260127
```

---

## 🔧 Example 1: Command-based configuration
```yaml
- name: Setup DOX CLI
  uses: dopxlab/setup-dox-cli@v1
- name: Configure Go
  run: dox config go
- name: Check Go version
  run: go version
```

**Note:** You can also install multiple tools at once:
```bash
dox config jdk python terraform
```

---

## 🔧 Example 2: File-based configuration with versions
`tools.yaml`:
```yaml
az: 2.82.0          # Specific version
terraform: 1.14.4   # Specific version
kubectl:            # Latest version (no version specified)
helm: v4.1.0        # Specific version
```

Workflow:
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Setup DOX CLI
        uses: dopxlab/setup-dox-cli@v1

      - name: Configure tools
        run: dox config -f tools.yaml

      - name: Verify tools
        run: |
          python3 --version
          az version
          terraform --version
          kubectl version --client
```

---

## 🔧 Example 3: Custom cache directories
`Note`: Useful for Github [ARC Runners](https://docs.github.com/en/actions/reference/runners/self-hosted-runners)
```yaml
- name: Setup DOX CLI with custom paths
  uses: dopxlab/setup-dox-cli@v1
  with:
    custom-dir: "$HOME/.dox/customize"
    resources-dir: "$HOME/dox_resources"

- name: Configure tools
  run: dox config terraform kubectl
```

---

## 🔧 Example 4: Persistent cache with GitHub Actions Cache
```yaml
- name: Cache DOX resources
  uses: actions/cache@v3
  with:
    path: ~/dox_resources
    key: dox-resources-${{ runner.os }}-${{ hashFiles('**/tools.yaml') }}
    restore-keys: |
      dox-resources-${{ runner.os }}-

- name: Setup DOX CLI
  uses: dopxlab/setup-dox-cli@v1
  with:
    resources-dir: "$HOME/dox_resources"

- name: Configure tools
  run: dox config -f tools.yaml
```

---

## 🔧 Example 5: GraalVM Native Image Workflow
```yaml
- name: Setup DOX CLI
  uses: dopxlab/setup-dox-cli@v1

- name: Install Maven with GraalVM
  run: dox config maven-gvm

- name: Build Native Image
  run: |
    mvn -Pnative native:compile
```

---

## ⚙️ Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `custom-dir` | Custom directory for DOX customization files | No | `$HOME/.dox/customize` |
| `resources-dir` | Directory for DOX resources cache (downloaded tools/binaries) | No | `$HOME/dox_resources` |

**Note:** For Kubernetes deployments, you can use a persistent volume (RWX) and bind it to the `resources-dir` path.

---

## 📝 Version Management

In `tools.yaml`, you can specify tool versions in two ways:

```yaml
# Specific version
terraform: 1.14.4

# Latest version (leave empty or omit version)
kubectl:
```

**If no version is specified, DOX will automatically install the latest available version.**

For command-based configuration, DOX installs the latest version by default:
```bash
dox config go           # Installs latest Go
dox config jdk python   # Installs latest JDK and Python
```

---

## ✨ Features
* Installs the latest DOX CLI
* Makes `dox` available in workflows
* Supports file-based and command-based configuration
* **Install single or multiple tools in one command**
* **Automatic chain dependency resolution** (e.g., `maven-gvm` → `jdk-gvm`)
* **Version pinning or automatic latest version installation**
* **Configurable cache directories** for customization and resources
* **GitHub Actions cache integration** for faster builds
* Works on GitHub-hosted Linux runners

---

## 📄 License
MIT License