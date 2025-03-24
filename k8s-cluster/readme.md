# single-node-k8s :kubernetes: 

A minimalist single-node Kubernetes cluster deployment using [Talos Linux](https://www.talos.dev/) and [Sidero Omni](https://omni.siderolabs.com/tutorials/getting_started).

---

## :star: Overview
- Deploys a lightweight Kubernetes cluster on bare metal/virtual machines
- Leverages Talos Linux for immutable Kubernetes-oriented OS
- Managed via Sidero Omni control plane
- Designed for edge/low-resource environments

---

## :wrench: Prerequisites

### Tools
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [talosctl](https://www.talos.dev/latest/talos-guides/installation/)

### Infrastructure
- :exclamation: Operational Omni deployment ([setup guide](https://github.com/kr1ps/onenodecluster.git))
- Registered machine in Omni instance
- Network access to Omni API endpoint

---

## :computer: IP Configuration (Kernel Parameters)

Configure networking via kernel command line:
```bash
ip=<NodeIP>::<DefaultGateway>:<Netmask>:<Hostname>:<Interface>:DHCP:<DNS1>:<DNS2>
```

### Example Configuration
```bash
ip=200.1.154.226::200.1.154.225:255.255.255.240:talos-node:eth0:none:172.18.0.23:172.18.0.22
```

---

## :rocket: Quick Start

1. **Clone Repository**
   ```bash
   git clone https://github.com/kr1ps/onenodecluster.git
   cd omni-cluster
   ```

2. **Configure Cluster**
   ```bash
   vim cluster.yaml  # Update machine ID
   ```

3. **Deploy with omnictl**
   ```bash
   omnictl cluster create -f cluster.yaml
   ```

---


## :link: References
- [Talos Linux Documentation](https://www.talos.dev/latest/)
- [Omni Project Site](https://www.sidero.dev/omni/)
- [Kernel IP Parameters Guide](https://www.kernel.org/doc/html/latest/admin-guide/nfs/nfsroot.html)
