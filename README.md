# Only for Testing Username Password jenkins:
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
  