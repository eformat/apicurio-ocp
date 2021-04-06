## respin of apicurio-studio

Uses an updated keycloak image for OCP4 integration
```bash
# jboss/keycloak:10.0.1
podman build -t quay.io/eformat/apicurio-studio-auth:latest -f Dockerfile
```

Re-generate full objects from template
```bash
oc process -f apicurio-standalone-template.yml \
  -p UI_ROUTE=apicurio-studio.apps.cluster.example.com \
  -p API_ROUTE=apicurio-studio-api.apps.cluster.example.com \
  -p WS_ROUTE=apicurio-studio-ws.apps.cluster.example.com \
  -p AUTH_ROUTE=apicurio-studio-auth.apps.cluster.example.com \
  -p GENERATED_KC_USER=admin \
  -p GENERATED_KC_PASS=password \
  -p APICURIO_MICROCKS_API_URL=https://microcksinstall-microcks.apps.cluster.example.com/api \
  -p APICURIO_MICROCKS_CLIENT_ID=microcks-serviceaccount \
  -p APICURIO_MICROCKS_CLIENT_SECRET=abcdefg-123-45ab-ab999-ec0934938093
```

See ArgoCD kustomize deployment here
- https://github.com/eformat/argocd/tree/master/apicurio
# apicurio-ocp
