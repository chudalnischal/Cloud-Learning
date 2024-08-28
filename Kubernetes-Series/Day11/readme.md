 Auto scaling in kubernetes

 Auto Scaling is Scaling the workload to meet the demand. It can be done manually or automatically.
 It also refers to the increasing the resources based on the customer demand.

 Types of Scaling 

 Horizontal Pod Auto Scaling 
 Vertical Pod Auto Scaling
 

 Summary of today task / workflow

 creating a cluster 
 adding metric server in kube-system namespace 
 creating thr deployement and default service 
 scaling deployment with hpa( horizontal ) 
 command kubectl autoscale deployment <deployement_name> --cpu=50 --min=num --max=num 
                  if the cpu utilization of the deployement increases to 50 or more then the replica will also increases.

                  