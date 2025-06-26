# 📦 Helm Project Documentation: E-commerce Microservices (Payment & Shipping)

## 📁 Project Structure

```
E-commerce/
│
├── payment/                 # Helm chart for payment service
│   ├── templates/           # Kubernetes manifest templates
│   ├── Chart.yaml           # Chart metadata
│   ├── values.yaml          # Default configuration values
│
├── shipping/                # Helm chart for shipping service
│   ├── templates/
│   ├── Chart.yaml
│   ├── values.yaml
│
├── index.yaml               # Helm repository index
├── payment-0.1.0.tgz        # Packaged payment chart
├── shipping-0.1.0.tgz       # Packaged shipping chart
└── README.md                # Project description (you can paste this content here)
```

## 🚀 Project Goal

This project demonstrates how to **package and deploy multiple microservices** (`payment` and `shipping`) to Kubernetes using **Helm**. It simulates a basic e-commerce architecture.

---

## 💠 Steps Performed

### 1️⃣ Create Individual Helm Charts

You created separate Helm charts for each microservice:

```bash
helm create payment
helm create shipping
```

Each chart comes with its own templated Kubernetes manifests and config files.

---

### 2️⃣ Customize Each Chart

You edited:

* `Chart.yaml` → Provided chart metadata like name and version
* `values.yaml` → Defined image, ports, replicas, and service settings
* `templates/` → Modified manifests for `Deployment`, `Service`, etc.

Each chart defines a complete deployable unit.

---

### 3️⃣ Package the Charts

You packaged each service into `.tgz` files using:

```bash
helm package payment
helm package shipping
```

This created:

* `payment-0.1.0.tgz`
* `shipping-0.1.0.tgz`

These are deployable Helm artifacts.

---

### 4️⃣ Create a Helm Repository Index

You generated an `index.yaml` so your Helm directory can function as a **Helm repository**:

```bash
helm repo index . --url https://arijit0405.github.io/helm/E-commerce
```

This created an `index.yaml` with entries like:

```yaml
entries:
  payment:
  - name: payment
    version: 0.1.0
    urls:
    - payment-0.1.0.tgz
```

This lets Helm clients discover and install your charts directly from GitHub.

---

### 5️⃣ (Optional) Deploy the Charts to Kubernetes

If you wanted to deploy the charts, you'd use:

```bash
helm install payment ./payment-0.1.0.tgz
helm install shipping ./shipping-0.1.0.tgz
```

You could also deploy directly from GitHub if hosted correctly:

```bash
helm repo add ecommerce https://arijit0405.github.io/helm/E-commerce
helm install payment ecommerce/payment
helm install shipping ecommerce/shipping
```

---

## 📜 Example Helm Values (from `values.yaml`)

```yaml
replicaCount: 2

image:
  repository: arijit/payment
  tag: latest
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 8080
```

---

This project structure is scalable and maintainable for deploying microservices using Helm.
