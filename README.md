# ⚠️ Make sure you copy and change the .dist files!

# Install the hub a.k.a. the base
```
aws --region=$r cloudformation create-stack --stack-name openwow-base --template-body file://cfn_base.yaml --parameters file://cfn_base_parameters.json
```
## Which includes:
* a micro'ish RDS
* a CloudWatch log group

Note that after the initial databse setup, you'll need to run the setup and migrations sql files. See CMaNGOS realmd documentation for more information.


# Install the edge locations
```
for r in us-east-1 eu-central-1 ap-southeast-1 ap-southeast-2; do
  aws --region=$r cloudformation create-stack --stack-name openwow-edge --template-body file://cfn_edge.yaml --parameters file://cfn_edge_parameters.json;
done
```
## Which includes:
* an ECS task definition (see below)
* an ECS cluster with a running service
* an AutoScalingGroup (does not auto scale quite yet however)
* a classic ELB to connect / load balance running containers
