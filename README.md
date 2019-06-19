# Docker

# Kafka

# Kubernetes
## Replace configmaps which aren't actual config maps
`:; kubectl create configmap <MAP_NAME> --from-file=<DIR_OF_CONFIGS> -o yaml --dry-run | kubectl replace -f -`


