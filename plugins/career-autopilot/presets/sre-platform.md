# Preset: sre-platform

For SRE, platform, DevOps, Kubernetes and cloud infrastructure engineers.
Setup writes these into Filters only for keys that are still empty. The user can edit any of them.

| Key | Value |
|---|---|
| target_roles | Site Reliability Engineer, Senior SRE, Platform Engineer, Kubernetes Engineer, Cloud Infrastructure Engineer, DevOps Engineer, Infrastructure Engineer |
| keywords | site reliability, kubernetes, platform engineering, openshift, terraform, ansible, observability, prometheus, grafana, linux, rhel, multi-cloud |
| seniority | mid, senior, staff, lead |
| exclude_keywords | intern, graduate, trainee, junior, helpdesk, desktop support |
| min_match | 75 |
| weights | must_have:45, years:15, stack:20, certs:10, domain:5, scope:5 |

## Stack groups (count overlap per group, not per word)

- Orchestration: Kubernetes, OpenShift, Rancher, EKS, AKS, GKE, Helm, Kustomize, Argo CD, Flux
- IaC / config: Terraform, Pulumi, Ansible, Packer, CloudFormation, Bicep
- CI/CD: Jenkins, GitHub Actions, GitLab CI, Tekton, Azure DevOps
- Observability: Prometheus, Grafana, Loki, Elastic, Datadog, Dynatrace, Splunk, OpenTelemetry
- OS: Linux, RHEL, Ubuntu, systemd, kernel tuning, STIG/CIS hardening
- Cloud: AWS, Azure, GCP, OCI, Alibaba Cloud
- Reliability practice: SLO/SLI, error budgets, incident response, postmortems, chaos engineering, on-call

## Cert equivalents (a cert counts as proof of the matching requirement)

CKA/CKAD/CKS → Kubernetes · RHCSA/RHCE/LFCS/LFCE → Linux · AWS SA Pro/Assoc → AWS · AZ-104/305/400 → Azure · GCP PCA/ACE → GCP · Terraform Associate → Terraform
