---
title: prometheus
author: Jerry.Baijy
tags:
  - dev
  - software
  - 监控平台
---

# Overview

[**Prometheus**](https://prometheus.io/) 是一个开源的监控和警报工具，最初由 Sound Cloud 开发。它专为云环境而设计，可以动态发现目标，并收集它们的度量指标，存储这些指标，并提供基于这些指标的警报功能。

# Install

## From NANA

- [This part is from NANA, and it is unfinished.](https://www.youtube.com/watch?v=QoDqxm7ybLc)

- **Requirement**

    - Cluster is running.
    - Helm has been installed and the repo 'arldka' is added into local.

- Install

    ```bash
    helm install prometheus arldka/prometheus-operator
    ```

## From IBM

- [**Source:** This part is from IBM.](https://www.youtube.com/watch?v=VMP48mMBDZw)

- **Requirement:** Git, Docker, Docker Compose

- install

    ```bash
    git clone https://gitlab.com/jerrybai/pmi-prometheus-grafana-sample.git
    cd pmi-prometheus-grafana-sample
    docker-compose up
    ```

- This will build and run 3 containers.

- Access WAS PMI metrics - Prometheus endpoint http://localhost:9080/metrics

- Access Prometheus Server UI [http://localhost:9090](http://localhost:9090/)

- Access Grafana [http://localhost:3000](http://localhost:3000/)

    Login: admin / admin

- Stop

    ```bash
    docker stop grafana prometheus twas_metrics
    ```

- Restart

    ```bash
    docker start grafana prometheus twas_metrics
    ```
