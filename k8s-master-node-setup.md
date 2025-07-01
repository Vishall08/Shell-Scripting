# Kubernetes Master Node Setup Instructions

This guide provides the exact commands to run on the **Master Node only** after running the common `k8s-node-setup.sh` script.

---

## 🧠 Execute ONLY on the "Master" Node

### ✅ 1. Initialize the Kubernetes Cluster

```bash
sudo kubeadm init
```

---

### ✅ 2. Set Up Local kubeconfig

```bash
mkdir -p "$HOME"/.kube
sudo cp -i /etc/kubernetes/admin.conf "$HOME"/.kube/config
sudo chown "$(id -u)":"$(id -g)" "$HOME"/.kube/config
```

---

### ✅ 3. Install a Network Plugin (Calico)

```bash
kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.26.0/manifests/calico.yaml
```

---

### ✅ 4. Generate the Join Command for Worker Nodes

```bash
kubeadm token create --print-join-command
```

> 🔁 Copy the output of this command and run it on each **Worker Node** to join the cluster.

---

## ✅ Notes

- This is only for the control-plane node (master).
- Use Calico as the CNI plugin; compatible with most cloud and bare-metal setups.
- You must run the `join` command from step 4 on each worker node.