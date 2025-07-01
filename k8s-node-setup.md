# Kubernetes Node Setup Script (Master & Worker)

This guide provides a step-by-step script to prepare both **Master** and **Worker** nodes for Kubernetes installation using `kubeadm`, with containerd as the runtime.

---

## ✅ Steps to Use

### 1. Save the Script

Create a file named `k8s-node-setup.sh` and paste the following content into it:

*(You already created this file.)*

---

### 2. Make the Script Executable

```bash
chmod +x k8s-node-setup.sh
```

---

### 3. Run the Script

```bash
sudo ./k8s-node-setup.sh
```

---

## ✅ After Script Execution

### On Master Node:

Initialize the Kubernetes cluster:

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

Configure kubectl access:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Apply a Pod Network (e.g., Flannel):

```bash
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

### On Worker Nodes:

Use the `kubeadm join ...` command printed at the end of `kubeadm init` to join the cluster.

---

## ✅ Notes

- Tested on **Ubuntu 20.04 / 22.04**
- Works for both **Master** and **Worker** setup
- Uses `containerd` (recommended container runtime)
- Automatically disables swap and sets kernel modules