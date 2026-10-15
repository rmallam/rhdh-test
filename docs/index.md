# rhdh-test

Quarkus golden-path backend with Jenkins, Helm, and OpenAPI

Backend for system **acme-demo**. Provides API `rhdh-test-api` (`GET /api`). Create the Node.js website template next and pick this Component + API.

## Pipeline

Jenkinsfile stages: **Unit tests → SonarQube → Helm lint**.

Point a Jenkins job named `demo/rhdh-test` at this repo. Set credential `SONAR_TOKEN` to run the scanner against `http://sonarqube.sonarqube.svc:9000`.

## Deploy

North-south is **OpenShift Route → Gateway API Gateway → HTTPRoute → app**. AuthZ in this chart is **deny-all** plus ALLOW from the ingress gateway. **STRICT mTLS** is namespace-wide (Kyverno on enroll).

```bash
oc label namespace demo-dev acme.io/mesh-enroll=true istio.io/dataplane-mode=ambient --overwrite
helm upgrade --install rhdh-test chart -n demo-dev
```

Ingress: `https://rhdh-test-demo-dev.apps.ocp.dkccw.sandbox3257.opentlc.com`

The chart labels pods `backstage.io/kubernetes-id=rhdh-test` for Topology.

## Dev Spaces

https://devspaces.devspaces.ocp.dkccw.sandbox3257.opentlc.com#https://github.com/alan/rhdh-test?new&devfilePath=devfile.yaml
