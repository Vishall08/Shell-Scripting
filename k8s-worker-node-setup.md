# Kubernetes Worker Node Join Instructions

This guide provides the commands to run **only on Worker Nodes** to join them to the Kubernetes cluster after the Master node has been initialized.

---

## 🧠 Execute on ALL of your Worker Nodes

### ✅ 1. Reset Any Existing Kubernetes State (Pre-flight Check)

```bash
sudo kubeadm reset pre-flight checks
```

---

### ✅ 2. Join the Cluster

Use the `kubeadm join` command that was generated on the Master node and append the required parameters.

### 🔔 Note:
- Add `sudo` at the beginning.
- Add `--v=5` at the end for verbose output.
- Add `--cri-socket unix:///run/containerd/containerd.sock`

### 🔧 Command Format:

```bash
sudo kubeadm join <private-ip-of-control-plane>:6443 --token <token> \
  --discovery-token-ca-cert-hash sha256:<hash> \
  --cri-socket unix:///run/containerd/containerd.sock --v=5
```

Replace:
- `<private-ip-of-control-plane>` with your master node's internal IP
- `<token>` and `<hash>` from the master’s `kubeadm token create --print-join-command` output

---

## ✅ Example

```bash
sudo kubeadm join 192.168.56.100:6443 --token abcdef.0123456789abcdef \
  --discovery-token-ca-cert-hash sha256:1234567890abcdef... \
  --cri-socket unix:///run/containerd/containerd.sock --v=5
```

---

## ✅ Notes

- This command must be run as `sudo`.
- Each worker node that runs this command will join the cluster.
- Ensure containerd is running before you execute the join.