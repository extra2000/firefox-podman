# firefox-podman

| License | Versioning | Build |
| ------- | ---------- | ----- |
| [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) | [![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release) | [![Build status](https://ci.appveyor.com/api/projects/status/0e45b0444em4wlmd/branch/master?svg=true)](https://ci.appveyor.com/project/nikAizuddin/firefox-podman/branch/master) |

Firefox in Podman.


## Creating configs

Create configmap:
```
cp -v ./configmaps/firefox.yaml{.example,}
```

Create pod file:
```
cp -v ./firefox-pod.yaml{.example,}
```


## SELinux

Load SELinux policy:
```
sudo semodule -i selinux/firefox_pod.cil /usr/share/udica/templates/{base_container.cil,net_container.cil}
```


## Running

Execute:
```
podman run -it --rm -p 127.0.0.1:3000:3000 --shm-size "2gb" --security-opt label=type:firefox_pod.process docker.io/linuxserver/firefox
```


## Running as Pod

Execute:
```
podman play kube --configmap configmaps/firefox.yaml --seccomp-profile-root ./seccomp firefox-pod.yaml
```
