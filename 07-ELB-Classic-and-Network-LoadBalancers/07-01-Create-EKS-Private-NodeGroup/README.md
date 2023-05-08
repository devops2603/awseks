# EKS - Create EKS Node Group in Private Subnets
Classic Load Balancer is a legacy load balancer which can be depricate din the near future. If we mention 'LoadBalancer' as type in service the default load balancer that is going to get created in AWS is Classic Load Balancer. Application Load Balancer supports the highest number of features. In this section we are going to create a classic load balancer. Also we will see network load balancer in this section.
In real time we dont use node port service, we map it to DNS and use it. From this section we will use private network to host our woker nodes as this is the architecture that is followed in 3-tier architecture in real time. As we are creating the worker nodes in provate subnets, the EKS control plane will be communicating with the worker nodes through NAT gateway provided the EKS control pane is having the public access. We can also enable the direct access which is VPC access where the EKS control pane can directly talk to worker nodes through VPC. We will create the RDS DB's in the same provate subnets or we can create another 2 private subnets and install RDS DB in there. 

![image](https://user-images.githubusercontent.com/115634064/236815147-329a070a-acdc-4fab-8102-e5b1d32f673b.png)

![image](https://user-images.githubusercontent.com/115634064/236814730-ae0a8e00-ced6-4f38-8343-afa459edbe71.png)

![image](https://user-images.githubusercontent.com/115634064/236815439-322b72bd-b2a1-4b7e-8b0b-b214dd87831c.png)

![image](https://user-images.githubusercontent.com/115634064/236819868-973f9092-7111-4ea8-a822-37d3a0e48df1.png)

## Step-01: Introduction
- We are going to create a node group in VPC Private Subnets
- We are going to deploy workloads on the private node group wherein workloads will be running private subnets and load balancer gets created in public subnet and accessible via internet.

## Step-02: Delete existing Public Node Group in EKS Cluster
```
# Get NodeGroups in a EKS Cluster
eksctl get nodegroup --cluster=<Cluster-Name>
eksctl get nodegroup --cluster=eksdemo1

# Delete Node Group - Replace nodegroup name and cluster name
eksctl delete nodegroup <NodeGroup-Name> --cluster <Cluster-Name>
eksctl delete nodegroup eksdemo1-ng-public1 --cluster eksdemo1
```

## Step-03: Create EKS Node Group in Private Subnets
- Create Private Node Group in a Cluster
- Key option for the command is `--node-private-networking`

```
eksctl create nodegroup --cluster=eksdemo1 \
                        --region=us-east-1 \
                        --name=eksdemo1-ng-private1 \
                        --node-type=t3.medium \
                        --nodes-min=2 \
                        --nodes-max=4 \
                        --node-volume-size=20 \
                        --ssh-access \
                        --ssh-public-key=kube-demo \
                        --managed \
                        --asg-access \
                        --external-dns-access \
                        --full-ecr-access \
                        --appmesh-access \
                        --alb-ingress-access \
                        --node-private-networking                       
```

## Step-04: Verify if Node Group created in Private Subnets

### Verify External IP Address for Worker Nodes
- External IP Address should be none if our Worker Nodes created in Private Subnets
```
kubectl get nodes -o wide (this should return nodes without external ip)
```
### Subnet Route Table Verification - Outbound Traffic goes via NAT Gateway
- Verify the node group subnet routes to ensure it created in private subnets
  - Go to Services -> EKS -> eksdemo -> eksdemo1-ng1-private
  - Click on Associated subnet in **Details** tab
  - Click on **Route Table** Tab.
  - We should see that internet route via NAT Gateway (0.0.0.0/0 -> nat-xxxxxxxx)
