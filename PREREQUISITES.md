## Prerequisites

* Apache Maven and Java v11+

* [Testcontainers](https://www.testcontainers.org)
  * -> running [Docker](https://docs.docker.com/engine/install/) environment 
  * Reason:🧠used by some of the build🧠 

### Docker Troubleshooting

#### Cgroups

**Error:** docker: Error response from daemon: OCI runtime create failed: container_linux.go:345: starting container process

This might be because your OS is using cgroupsV2 by default, which is not yet supported by the container runtimes.

**Fix:** Disable cgroupsV2:

* Fedora: `sudo grubby --update-kernel=ALL --args="systemd.unified_cgroup_hierarchy=0"` then restart your machine.
* Ubuntu: `sudo update-grub "systemd.unified_cgroup_hierarchy=0""` then restart your machine.
