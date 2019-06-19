## Bash
#### Open file handle counts
`sudo lsof | awk '{ print $2, $9 }' | sort | uniq -c | sort -n | tail -20`

## Docker

## Kafka

## Kubernetes
#### Replace configmaps which aren't actual config maps
`:; kubectl create configmap <MAP_NAME> --from-file=<DIR_OF_CONFIGS> -o yaml --dry-run | kubectl replace -f -`


