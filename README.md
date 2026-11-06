# TEST The tempate in local helm
  helm template . --name-template jenkins --namespace jenkins --debug
# Pasword jenkins
admin
admin

# Add in ARGOCD TEMPLATE
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: jenkins
  namespace: argocd
spec:
  project: default

  destination:

    namespace: jenkins
    server: https://kubernetes.default.svc

  source:
    path: .
    repoURL: https://github.com/swapnilshrirao9/helm-jenkins.git
    targetRevision: main

  syncPolicy:
    automated:
      prune: true
      selfHeal: true

    syncOptions:
      - CreateNamespace=true
  # TEST The tempate in local helm
  helm template . --name-template jenkins --namespace jenkins --debug

  # Issue I encounter 
   1) PVC PV  for sonar Its not Create for Sonar proper one pvc not work required 3 
   2) Issue in the Environement in Sonarqube
   3) Limmit to update request quta 8GB