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

## 🛠 How the Packages Were Built

The `.deb` packages were built from the **official OpenVINO 2025.3.0 source** on Ubuntu 22.04 and 24.04 using the following steps:

1. **Prepare a clean Ubuntu system** with build dependencies installed:

```bash
sudo apt-get update
sudo apt-get install -y \
    build-essential cmake git ccache patchelf lsb-release wget unzip pkg-config \
    libgtk-3-dev libdrm-dev libtbb-dev libpugixml-dev
```

2. **Clone OpenVINO source**:

```bash
git clone https://github.com/openvinotoolkit/openvino.git
cd openvino
git checkout tags/2025.3.0 -b build-2025.3.0
git submodule update --init --recursive
```

3. **Configure build (C++ runtime only)**:

```bash
mkdir build && cd build
cmake .. \
  -DCMAKE_BUILD_TYPE=Release \
  -DENABLE_PYTHON=OFF \
  -DENABLE_TESTS=OFF \
  -DENABLE_SAMPLES=ON \
  -DCMAKE_INSTALL_PREFIX=/opt/openvino-runtime
```

4. **Build OpenVINO**:

```bash
make -j$(nproc)
```

5. **Install into staging directory (`debroot`)**:

```bash
DESTDIR=$PWD/debroot make install
```

6. **Create Debian control files**:

```bash
mkdir -p debroot/DEBIAN
cat << 'EOF' > debroot/DEBIAN/control
Package: openvino-runtime
Version: 2025.3.0
Section: libs
Priority: optional
Architecture: amd64
Maintainer: Your Name <you@example.com>
Description: |
  OpenVINO Runtime (C++ only), built from official sources (2025.3.0).
  No Python bindings. Ubuntu 22.04/24.04 build.
EOF
```

7. **Build `.deb` package**:

```bash
dpkg-deb --build debroot openvino-runtime_2025.3.0_amd64.deb
```

8. **Test installation on a clean Ubuntu system**:

```bash
sudo dpkg -i openvino-runtime_2025.3.0_amd64.deb
sudo apt --fix-broken install
ls /opt/openvino-runtime/
```

---

## 🔗 References

* Official OpenVINO repository: [https://github.com/openvinotoolkit/openvino](https://github.com/openvinotoolkit/openvino)
* Official OpenVINO documentation: [https://docs.openvino.ai/](https://docs.openvino.ai/)

This repository makes it easy to **deploy OpenVINO offline** without relying on Intel’s APT repositories or pip packages.
