# OpenVINO 2025.3.0 Offline .deb Packages for Ubuntu

This repository provides **prebuilt `.deb` packages** of OpenVINO 2025.3.0 for **Ubuntu 22.04 and 24.04**. The packages are designed for **offline installation** on embedded or air-gapped systems and contain the **C++ runtime only**, without Python bindings.

The repository does **not** include a build workflow or source code. Detailed instructions on how the packages were built are provided for reproducibility.

---

## 📦 Provided Packages

| Package                                     | Description                              | Ubuntu Version |
| ------------------------------------------- | ---------------------------------------- | -------------- |
| `openvino-runtime_2025.3.0_22.04_amd64.deb` | OpenVINO C++ runtime, no Python bindings | 22.04          |
| `openvino-runtime_2025.3.0_24.04_amd64.deb` | OpenVINO C++ runtime, no Python bindings | 24.04          |

* Installed files are placed under: `/opt/openvino-runtime/`
* The `.deb` packages can be installed offline using `dpkg`.

# Quick Start

For Ubuntu 22.04:
```bash
# Download the package from Releases
wget https://github.com/eickeler/openvino-workflow/releases/download/v2025.3.0/openvino-runtime_2025.3.0_22.04_amd64.deb

# Install the package
sudo dpkg -i openvino-runtime_2025.3.0_22.04_amd64.deb
sudo apt --fix-broken install

# Verify installation
ls /opt/openvino-runtime/
```
For Ubuntu 24.04:
```bash
# Download the package from Releases

wget https://github.com/eickeler/openvino-workflow/releases/download/v2025.3.0/openvino-runtime_2025.3.0_24.04_amd64.deb

# Install the package
sudo dpkg -i openvino-runtime_2025.3.0_24.04__amd64.deb
sudo apt --fix-broken install

# Verify installation
ls /opt/openvino-runtime/
```

---

## 🔗 References

* Official OpenVINO repository: [https://github.com/openvinotoolkit/openvino](https://github.com/openvinotoolkit/openvino)
* Official OpenVINO documentation: [https://docs.openvino.ai/](https://docs.openvino.ai/)

This repository makes it easy to **deploy OpenVINO offline** without relying on Intel’s APT repositories or pip packages.
