# my-crossplane-resources

## aws quick start part 2

### bucket managed resource

```shell
kubectl apply -f aws-quickstart-part2/s3bucket-mr.yaml
kubectl get bucket.s3.aws.upbound.io/alfay-crossplane-bucket
kubectl get bucket.s3.aws.upbound.io/alfay-crossplane-bucket -o json | jq .status.atProvider.id -r
kubectl delete bucket.s3.aws.upbound.io/alfay-crossplane-bucket 
```

### dynamodb-with-bucket

```shell
kubectl apply -f aws-quickstart-part2/xdatabase-composition.yaml
kubectl get composition/dynamodb-with-bucket
kubectl apply -f aws-quickstart-part2/xdatabase-xrd.yaml
kubectl get xrd/xdatabases.custom-api.example.org
kubectl apply -f aws-quickstart-part2/xdatabase-xr.yaml
kubectl get xdatabase/my-composite-resource
kubectl create namespace my-crossplane-namespace
kubectl apply -f aws-quickstart-part2/xdatabase-claim.yaml
kubectl get database/claimed-database -n my-crossplane-namespace
```

```shell
kubectl delete composition/dynamodb-with-bucket xrd/xdatabases.custom-api.example.org xdatabase/my-composite-resource 
kubectl delete database/claimed-database -n my-crossplane-namespace
```

## aws quick start part 3

```shell
kubectl apply -f aws-quickstart-part3/xdatabase-composition.yaml
kubectl get composition/dynamodb-with-bucket
kubectl apply -f aws-quickstart-part3/xdatabase-claim-eu.yaml
kubectl get database/claimed-eu-database -n my-crossplane-namespace
```

```shell
kubectl delete composition/dynamodb-with-bucket xrd/xdatabases.custom-api.example.org xdatabase/my-composite-resource 
kubectl delete database/claimed-eu-database -n my-crossplane-namespace
```

## Dependencies

```shell
kubectl apply -f dependencies/vpc-composition.yaml
kubectl apply -f dependencies/vpc-xrd.yaml
kubectl apply -f dependencies/vpc-claim.yaml
kubectl get composition/my-vpcs
kubectl get xrd/xvpcs.custom-api.example.org
kubectl get subnet.claythorn.com/claimed-subnets -n my-crossplane-namespace
kubectl describe subnet.claythorn.com/claimed-subnets -n my-crossplane-namespace
kubectl get VPC.ec2.aws.upbound.io -o json | jq '.items[].status.atProvider.id'
```

```shell
kubectl delete composition/my-vpcs xrd/xvpcs.claythorn.com
kubectl apply -f dependencies/vpc.yaml
kubectl apply -f dependencies/vpc-claim.yaml
kubectl get vpc.claythorn.com/claimed-vpcs -n my-crossplane-namespace
kubectl get vpc.claythorn.com/claimed-vpcs -n my-crossplane-namespace -o json | jq '.status.id' -r
```

```shell
kubectl delete composition/my-subnets xrd/xsubnets.claythorn.com
kubectl apply -f dependencies/subnet.yaml
kubectl apply -f dependencies/subnet-claim.yaml
kubectl get subnet.claythorn.com/claimed-subnets -n my-crossplane-namespace 
kubectl get subnet.ec2.aws.upbound.io -o json |  jq '.items[0].status.atProvider'
```








