# 🚀 Kubernetes Monitoring with Prometheus & Grafana

[![GitHub repo size](https://img.shields.io/github/repo-size/atulupadhyay2004/k8s_Monitoring-with-Prometheus-Grafana)](https://github.com/atulupadhyay2004/k8s_Monitoring-with-Prometheus-Grafana)
[![GitHub stars](https://img.shields.io/github/stars/atulupadhyay2004/k8s_Monitoring-with-Prometheus-Grafana?style=social)](https://github.com/atulupadhyay2004/k8s_Monitoring-with-Prometheus-Grafana/stargazers)

> A complete Kubernetes monitoring stack that deploys a sample application with Horizontal Pod Autoscaling (HPA), scrapes metrics using Prometheus, and visualizes them in Grafana dashboards.

---

## 📋 Table of Contents
- [About The Project](#-about-the-project)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [System Architecture](#-system-architecture)
- [Workflow](#-workflow)
- [HPA & Resource Management](#-hpa--resource-management)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Deploy the Application](#deploy-the-application)
  - [Set up Prometheus](#set-up-prometheus)
  - [Set up Grafana](#set-up-grafana)
  - [Configure HPA](#configure-hpa)
- [Monitoring Dashboards](#-monitoring-dashboards)
- [Contributing](#-contributing)
- [License](#-license)
- [Contact](#-contact)

---

## 📖 About The Project

This project sets up a **production-ready monitoring stack** for Kubernetes workloads. It includes:

- A sample **NGINX application** deployed as a Kubernetes Deployment
- **Horizontal Pod Autoscaling (HPA)** that automatically scales pods based on CPU utilization
- **Prometheus** for metrics collection and storage
- **Grafana** for beautiful, customizable dashboards

The goal is to demonstrate how to monitor your Kubernetes cluster, visualize resource usage, and implement auto-scaling based on real-time metrics.

---

## ✨ Features

- ✅ **Kubernetes Deployment** – Sample NGINX app with resource requests and limits
- ✅ **Horizontal Pod Autoscaling** – Auto-scales from 2 to 5 replicas based on CPU usage
- ✅ **Resource Management** – CPU and memory requests/limits defined for each pod
- ✅ **Prometheus Integration** – Scrapes Kubernetes and application metrics
- ✅ **Grafana Dashboards** – Pre-configured dashboards for cluster and pod monitoring
- ✅ **Metric-Based Scaling** – HPA uses Prometheus metrics (via metric-server or custom adapter)

---

## 🛠 Tech Stack

| Category | Technology |
|----------|------------|
| **Orchestration** | Kubernetes (Minikube / EKS / GKE / AKS) |
| **Application** | NGINX (latest) |
| **Auto-scaling** | Horizontal Pod Autoscaler (HPA) |
| **Metrics Collection** | Prometheus + kube-state-metrics + node-exporter |
| **Visualization** | Grafana |
| **Metrics API** | Kubernetes Metrics Server |

---

## 🧠 System Architecture

Below is the high-level architecture of the monitoring and auto-scaling setup:

---

## 🔄 Workflow

This diagram illustrates the end-to-end flow of metrics collection, auto-scaling, and visualization:

```mermaid
flowchart TD
    A[Developer deploys application] --> B[Kubernetes Deployment creates pods]
    B --> C[Pods run with resource requests/limits]
    C --> D[Metrics Server collects CPU/Memory usage]
    D --> E[HPA reads metrics from Metrics Server]
    E --> F{CPU > 50%?}
    F -->|Yes| G[HPA scales up replicas]
    F -->|No| H[HPA maintains or scales down]
    G --> I[New pods are created]
    I --> J[Load is distributed]
    H --> K[Pods are terminated if idle]
    
    C --> L[Prometheus scrapes metrics]
    L --> M[Prometheus stores metrics in TSDB]
    M --> N[Grafana queries Prometheus]
    N --> O[Grafana displays dashboards]
    O --> P[User monitors cluster health]
    
    G --> Q[Scaling event logged]
    H --> Q
    Q --> R[Alert sent if configured]
