# pkg-urm-ext

This is the debian packaging side of the userspace-resource-manager-extensions project. Upstream project is hosted here: https://github.com/qualcomm/userspace-resource-manager-extensions

## Branches

- qli-cli
- qcom/debian/latest
- qcom/debian/next


## Build Instructions
This project has a build dependency on the URM (userspace-resource-manager) package. To build both the packages follow these steps:
 
### Install sbuild tool
```bash
sudo apt-get update
sudo apt-get install -y sbuild schroot debootstrap eatmydata ccache
```
 
### Add user to sbuild group
```bash
sudo adduser $USER sbuild
newgrp sbuild
```
 
### Create an Ubuntu noble chroot
```bash
sudo sbuild-createchroot \
   --include=eatmydata,ccache \
   --components=main,universe \
   noble \
   /srv/chroot/noble-amd64 \
   http://archive.ubuntu.com/ubuntu
```
 
### Build URM
```bash
cd pkg-urm/
sbuild -d noble
```

### Verify
```bash
ls ../*.deb
```
 
### Build urm-extensions
```bash
cd userspace-resource-manager-extensions-public/
sbuild -d noble \
  --extra-package=../userspace-resource-manager_1.0.0-1_amd64.deb
```

## Installation Instructions
```bash
sudo dpkg -i userspace-resource-manager-extensions_1.0.0-1_arm64.deb
```

## Getting in Contact
For support or inquiries, contact: Maintainers.pkg-urm-ext <maintainers.pkg-urm-ext@qualcomm.com>

## Development
We welcome contributions! Please see our CONTRIBUTING.md file for guidelines.

## License
pkg-urm-ext is licensed under the [BSD-3-Clause License](https://spdx.org/licenses/BSD-3-Clause.html). See [LICENSE.txt](LICENSE.txt) for the full license text.
