🚀 One-Node K8s Cluster (Talos + Omni)
Supporting resources for my blog post about ditching 7-node k3s for a minimalist Talos Linux setup.

⚡ What’s Here?
Configs, scripts, and docs to replicate my single-node production-ready Kubernetes cluster using:

Talos Linux (k8s OS, API-driven, no SSH!)

Omni Sidero (cluster lifecycle management)

🛠️ Repo Structure
Copy
.  
├── omni-sideros-deploy/      # Docker Compose + setup notes for Omni  
├── k8s-cluster/           # Talos cluster.yaml + custom patches  
└── ...  

🤔 Customizing?
Tweak cluster-config/cluster.yaml for your hardware/cloud.

