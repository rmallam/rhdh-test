# rhdh-test

Quarkus golden-path backend with Jenkins, Helm, and OpenAPI

Catalog: **System** `acme-demo` ← **Component** (service) `rhdh-test` **providesApis** `rhdh-test-api`.

| Piece | Path |
|---|---|
| App | `GET /health`, `GET /api` |
| Tests | `mvn test` |
| Sonar | `sonar-project.properties` |
| CI | `Jenkinsfile` |
| Deploy | `chart/` (Helm + OSSM: Route → Gateway → HTTPRoute, deny-all, STRICT mTLS) |
| IDE | `devfile.yaml` |

```bash
mvn -q test
helm lint chart
```
