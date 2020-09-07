[Helm Repo](https://braedon.github.io/helm)
====
The helm repository for projects from [github.com/braedon](https://github.com/braedon).

# Use Repo
```bash
helm repo add braedon https://braedon.github.com/helm
helm repo update
```

# Charts
- [Prometheus Elasticsearch Exporter](/helm/prometheus-es-exporter)
- [Prometheus MySQL Exporter](/helm/prometheus-mysql-exporter)

# Rebuild Repo
```bash
helm package ./*/
helm repo index --url https://braedon.github.io/helm .
```
