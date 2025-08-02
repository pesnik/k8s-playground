# k8s-playground

> **Hands-on Kubernetes experimentation and skill-building through progressive challenges**

A structured learning environment for mastering Kubernetes concepts through practical exercises, real-world scenarios, and incremental complexity. This playground follows a challenge-driven approach to build proficiency with container orchestration, cluster management, and cloud-native deployment patterns.

## 🎯 Learning Objectives

- **Core Concepts**: Pods, Services, Deployments, ConfigMaps, Secrets
- **Cluster Operations**: Scaling, rolling updates, health checks, resource management
- **Networking**: Service mesh basics, ingress controllers, network policies
- **Storage**: Persistent volumes, storage classes, stateful applications
- **Security**: RBAC, pod security policies, secrets management
- **Observability**: Logging, monitoring, debugging techniques
- **CI/CD Integration**: GitOps workflows, automated deployments

## 📁 Repository Structure

```
k8s-playground/
├── 01-fundamentals/          # Core Kubernetes concepts
│   ├── pods/                 # Pod lifecycle and management
│   ├── services/             # Service discovery and networking
│   ├── deployments/          # Application deployment patterns
│   └── configmaps-secrets/   # Configuration management
├── 02-intermediate/          # Advanced deployment scenarios
│   ├── scaling/              # Horizontal/vertical pod autoscaling
│   ├── rolling-updates/      # Zero-downtime deployments
│   ├── persistent-storage/   # StatefulSets and volume management
│   └── networking/           # Ingress, load balancing, DNS
├── 03-advanced/              # Production-ready patterns
│   ├── security/             # RBAC, network policies, pod security
│   ├── monitoring/           # Prometheus, Grafana, alerting
│   ├── operators/            # Custom resource definitions
│   └── multi-cluster/        # Federation and cross-cluster communication
├── 04-real-world/            # End-to-end application scenarios
│   ├── microservices/        # Multi-service architectures
│   ├── databases/            # Stateful workload patterns
│   ├── ci-cd/                # GitOps and pipeline integration
│   └── disaster-recovery/    # Backup, restore, failover strategies
├── environments/             # Cluster setup configurations
│   ├── local/                # minikube, kind, k3s setups
│   ├── cloud/                # EKS, GKE, AKS configurations
│   └── bare-metal/           # Self-managed cluster setup
├── tools/                    # Helper scripts and utilities
│   ├── setup/                # Environment bootstrapping
│   ├── monitoring/           # Observability stack deployment
│   └── troubleshooting/      # Debugging and diagnostic tools
└── docs/                     # Learning materials and references
    ├── concepts/             # Kubernetes architecture deep-dives
    ├── troubleshooting/      # Common issues and solutions
    └── best-practices/       # Production deployment guidelines
```

## 🚀 Quick Start

### Prerequisites

- **Kubernetes Cluster**: Local (minikube/kind/k3s) or cloud-managed (EKS/GKE/AKS)
- **kubectl**: Kubernetes command-line tool
- **Docker**: Container runtime (for local development)
- **Helm** (optional): Package manager for Kubernetes

### Environment Setup

Choose your preferred Kubernetes environment:

#### Option 1: Local Development (minikube)
```bash
# Install minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Start cluster
minikube start --driver=docker --memory=4096 --cpus=2

# Verify installation
kubectl cluster-info
```

#### Option 2: Lightweight Local (kind)
```bash
# Install kind
go install sigs.k8s.io/kind@latest

# Create cluster
kind create cluster --config environments/local/kind-config.yaml

# Set context
kubectl cluster-info --context kind-kind
```

#### Option 3: Cloud-Managed Cluster
```bash
# Example: Amazon EKS
eksctl create cluster --name k8s-playground --region us-west-2 --nodegroup-name workers --node-type t3.medium --nodes 2

# Example: Google GKE
gcloud container clusters create k8s-playground --zone us-central1-a --num-nodes 2 --machine-type e2-medium
```

### First Challenge: Deploy Your First Application

```bash
# Navigate to fundamentals
cd 01-fundamentals/pods

# Deploy a simple nginx pod
kubectl apply -f simple-pod.yaml

# Check pod status
kubectl get pods

# Access the application
kubectl port-forward pod/nginx-pod 8080:80
```

## 📚 Learning Path

### Phase 1: Fundamentals (Week 1-2)
- [ ] **Pod Basics**: Create, inspect, and manage individual pods
- [ ] **Services**: Expose applications with ClusterIP, NodePort, LoadBalancer
- [ ] **Deployments**: Manage application lifecycle with ReplicaSets
- [ ] **Configuration**: Use ConfigMaps and Secrets for environment variables

### Phase 2: Intermediate Operations (Week 3-4)
- [ ] **Scaling**: Implement horizontal pod autoscaling
- [ ] **Updates**: Perform rolling updates and rollbacks
- [ ] **Storage**: Mount persistent volumes for stateful applications
- [ ] **Networking**: Configure ingress controllers and DNS

### Phase 3: Advanced Patterns (Week 5-6)
- [ ] **Security**: Implement RBAC and network policies
- [ ] **Monitoring**: Deploy Prometheus and Grafana stack
- [ ] **Custom Resources**: Create operators and CRDs
- [ ] **Multi-tenancy**: Namespace isolation and resource quotas

### Phase 4: Production Scenarios (Week 7-8)
- [ ] **Microservices**: Deploy complex multi-service applications
- [ ] **Databases**: Run stateful workloads (PostgreSQL, MongoDB)
- [ ] **CI/CD**: Integrate with GitOps workflows (ArgoCD, Flux)
- [ ] **Disaster Recovery**: Implement backup and restore strategies

## 🛠 Challenge Categories

### 🎯 **Skill Builders** 
Progressive exercises focusing on specific Kubernetes concepts
- **Difficulty**: ⭐ Beginner → ⭐⭐⭐ Advanced
- **Duration**: 30 minutes - 2 hours per challenge
- **Format**: Step-by-step guided exercises with validation checkpoints

### 🏗 **Real-World Scenarios**
End-to-end implementations mimicking production environments
- **Complexity**: Multi-component applications
- **Focus**: Best practices, troubleshooting, optimization
- **Deliverable**: Fully functional, documented deployments

### 🔧 **Troubleshooting Labs**
Broken configurations requiring diagnostic and repair skills
- **Objective**: Develop debugging proficiency
- **Format**: "Fix the cluster" scenarios with hidden issues
- **Skills**: Log analysis, resource inspection, network troubleshooting

## 📖 Documentation Standards

Each challenge includes:

- **`README.md`**: Objective, prerequisites, step-by-step instructions
- **`manifests/`**: Kubernetes YAML configurations
- **`solution/`**: Reference implementation and explanation
- **`troubleshooting.md`**: Common issues and debugging tips
- **`validation.sh`**: Automated testing script for solution verification

## 🎓 Completion Criteria

**Challenge Completion**: 
- [ ] All resources deploy successfully
- [ ] Application functions as expected
- [ ] Validation script passes
- [ ] Documentation updated with learnings

**Module Completion**:
- [ ] 80% of challenges completed
- [ ] Troubleshooting scenario resolved
- [ ] Real-world implementation deployed
- [ ] Peer review of solution approach

## 🔍 Troubleshooting Resources

### Common Issues
- **Pod CrashLoopBackOff**: Check logs with `kubectl logs <pod-name>`
- **Service Not Accessible**: Verify selectors match pod labels
- **Image Pull Errors**: Confirm image exists and registry credentials
- **Resource Constraints**: Monitor with `kubectl top nodes/pods`

### Debugging Commands
```bash
# Pod inspection
kubectl describe pod <pod-name>
kubectl logs <pod-name> --previous

# Service debugging
kubectl get endpoints <service-name>
kubectl describe service <service-name>

# Cluster diagnostics
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl cluster-info dump
```

## 🤝 Contributing

We welcome contributions to expand the playground:

1. **New Challenges**: Add scenarios covering emerging Kubernetes features
2. **Environment Support**: Extend compatibility with additional cluster types
3. **Documentation**: Improve explanations and add visual diagrams
4. **Automation**: Enhance validation scripts and setup procedures

### Contribution Guidelines
- Follow existing directory structure and naming conventions
- Include comprehensive documentation and validation scripts
- Test challenges on multiple Kubernetes distributions
- Update main README with new learning path additions

## 📚 Additional Resources

### Official Documentation
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [kubectl Reference](https://kubernetes.io/docs/reference/kubectl/)
- [Kubernetes API Reference](https://kubernetes.io/docs/reference/kubernetes-api/)

### Learning Materials
- [Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way)
- [Certified Kubernetes Administrator (CKA)](https://www.cncf.io/certification/cka/)
- [CNCF Landscape](https://landscape.cncf.io/)

### Community
- [Kubernetes Slack](https://kubernetes.slack.com/)
- [r/kubernetes](https://reddit.com/r/kubernetes)
- [Stack Overflow - kubernetes](https://stackoverflow.com/questions/tagged/kubernetes)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Happy Kubernetes Learning! 🚢⚙️**

> *"The best way to learn Kubernetes is by breaking it, fixing it, and understanding why it broke." - k8s-playground philosophy*
