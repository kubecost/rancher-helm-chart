# rancher-helm-chart
Rancher partner Helm chart tarball repository

v1.70.0 is built from the source files of Kubecost's v.1.70.0 release (https://github.com/kubecost/cost-analyzer-helm-chart/tree/release-1.70.0), with a few notable changes:

 - `requirements.yaml` has been deleted from the `cost-analyzer` directory because Rancher runs `helm dependency update`, which fails because of requirements
 - every subchart template yaml (Prometheus / Grafana / Thanos) has been wrapped with `{{ if .Values.global.<subchart-name>.enabled }}` and `{{ end }}` as a result of the requirements deletion
 - `cost-analyzer-deployment-template.yaml` needed a tweak at lines 430 and 584, from `{{- else if .Values.thanos }}` to `{{- else if and .Values.global.thanos.enabled .Values.thanos }}`
