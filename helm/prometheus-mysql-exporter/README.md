[Prometheus MySQL Exporter](https://github.com/braedon/prometheus-mysql-exporter)
====
This Prometheus exporter periodically runs configured queries against a MySQL server and exports the results as Prometheus gauge metrics.

[Source Code](https://github.com/braedon/prometheus-mysql-exporter) | [Python Package](https://pypi.org/project/prometheus-mysql-exporter) | [Docker Image](https://hub.docker.com/r/braedon/prometheus-mysql-exporter) | [Helm Chart](https://braedon.github.io/helm/prometheus-mysql-exporter)

# Installation
Deploy prometheus-mysql-exporter on a Kubernetes cluster with the default configuration:
```bash
helm repo add braedon https://braedon.github.com/helm
helm repo update

helm install braedon/prometheus-mysql-exporter --name <release name> \
                                               --set mysql.server=<mysql server address> \
                                               --set image.tag=<image tag>
```

Specify configuration via a YAML file:
```bash
helm install braedon/prometheus-mysql-exporter --name <release name> -f <config file>.yaml
```

# Configuration
Available configurable parameters and their default values.

Parameter                | Description                                         | Default
---                      | ---                                                 | ---
`mysql.server`           | address of mysql server to run queries on           | none
`mysql.cred.secret`      | name of the user credentials secret, if required    | none
`mysql.cred.usernameKey` | username key in credentials secret                  | `username`
`mysql.cred.passwordKey` | password key in credentials secret                  | `password`
`mysql.localTimezone`    | local timezone for SQL commands like NOW()          | none
`mysql.queries`          | mysql queries to run                                | see values.yaml
`deployment.replicas`    | exporter pod replicas to deploy                     | `1`
`pod.annotations`        | annotations to add to the exporter pods             | `{}`
`image.repository`       | exporter docker image repository                    | `braedon/prometheus-mysql-exporter`
`image.tag`              | exporter docker image tag                           | none
`image.pullPolicy`       | exporter docker image pull policy                   | `IfNotPresent`
`container.port`         | exporter container metrics port                     | `9206`
`container.portName`     | exporter container metrics port name                | `prometheus`
`container.extraArgs`    | extra arguments to pass to the exporter container   | `[]`
`container.resources`    | exporter container resource requests & limits       | `{}`
`nodeSelector`           | node labels for exporter pod assignment             | `{}`
`tolerations`            | node taints to tolerate (requires Kubernetes >=1.6) | `[]`
`affinity`               | node/pod affinities (requires Kubernetes >=1.6)     | `{}`
`service.port`           | exporter service port                               | `9206`
`service.portName`       | exporter service port name                          | `prometheus`
`service.annotations`    | annotations to add to the exporter service          | `{}`

See the [exporter README](https://github.com/braedon/prometheus-mysql-exporter#usage) for details on the format of exporter options like `mysql.server`.

See the [example query config file](https://github.com/braedon/prometheus-mysql-exporter/blob/master/exporter.cfg) for examples and explanations of query configurations for `mysql.queries`.
