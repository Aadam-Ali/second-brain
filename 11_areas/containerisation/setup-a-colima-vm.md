---
id: 20240614144459
tags: [docker]
---

# Setup a Colima VM

Run the following command:
```bash
colima start \
--profile default \
--activate \
--arch aarch64 \
--cpu 10 \
--disk 48 \
--memory 24 \
--mount ${HOME}:w \
--mount-inotify \
--ssh-agent \
--vm-type vz \
--vz-rosetta \
--verbose
```

Related:
  * <https://medium.com/@guillem.riera/the-most-performant-docker-setup-on-macos-apple-silicon-m1-m2-m3-for-x64-amd64-compatibility-da5100e2557d>
