# Load Balancing workloads on EKS using AWS Application Load Balancer
![image](https://github.com/devops2603/awseks/assets/115634064/b0c1064d-4291-41a8-850a-7d1b875627dc)
![image](https://github.com/devops2603/awseks/assets/115634064/672cac1b-22d3-4950-a028-641d936491d7)
![image](https://github.com/devops2603/awseks/assets/115634064/8a1d8303-b84c-4866-be0f-55754051c644)
![image](https://github.com/devops2603/awseks/assets/115634064/6c0f7ad6-f2b1-4b11-ae24-9bcf404a86df)
AWS application load balancer can be provisioned for our kubernestes using kubernetes ingress manifest.
![image](https://github.com/devops2603/awseks/assets/115634064/aaefdba5-0b8f-4f30-92c2-5e12f904ea09)
![image](https://github.com/devops2603/awseks/assets/115634064/4ebdc6b7-8371-4f48-8986-9dbe3cb46248)
When you are using managed node groups in EKS cluster, then by default you can use instance mode or even you can use IP mode. But when you are using only fargate profile then you need to use IP mode because fargate profile doesnt support nodeport service.
Whenever we provision kubernetes ingress controller on our kubernetes cluster it is going to create AWS or ingress resources.
ALB that is going to create is of version ELB V2.
AWS EKS Load Balancer controller is the core controller which helps us in creating the ingress services in kubernetes cluster.
![image](https://github.com/devops2603/awseks/assets/115634064/4080b20e-6342-41f2-8c96-e7cc9472b5c2)
![image](https://github.com/devops2603/awseks/assets/115634064/b13dcf65-56bb-4106-8790-eee1285dd65e)

## Topics
- We will be looking in to this topic very extensively in a step by step and module by module model. 
- The below will be the list of topics covered as part of AWS ALB Ingress Perspective. 


| S.No  | Topic Name |
| ------------- | ------------- |
| 1.  | AWS Load Balancer Controller Installation  |
| 2.  | ALB Ingress Basics  |
| 3.  | ALB Ingress Context Path based Routing  |
| 4.  | ALB Ingress SSL  |
| 5.  | ALB Ingress SSL Redirect (HTTP to HTTPS) |
| 6.  | ALB Ingress External DNS |
| 7.  | ALB Ingress External DNS for k8s Ingress |
| 8.  | ALB Ingress External DNS for k8s Service |
| 9.  | ALB Ingress Name based Virtual Host Routing |
| 10. | ALB Ingress SSL Discovery - Host |
| 11. | ALB Ingress SSL Discovery - TLS |
| 12. | ALB Ingress Groups |
| 13. | ALB Ingress Target Type - IP Mode |
| 13. | ALB Ingress Internal Load Balancer |


## References: 
- Good to refer all the below for additional understanding.

### AWS Load Balancer Controller
- [AWS Load Balancer Controller Documentation](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/)


### AWS ALB Ingress Annotations Reference
- https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/guide/ingress/annotations/

### eksctl getting started
- https://eksctl.io/introduction/#getting-started

### External DNS
- https://github.com/kubernetes-sigs/external-dns
- https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/alb-ingress.md
- https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/aws.md
