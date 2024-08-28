 config map and secrets


Can be created by both imperative and Declerative way. It is used to store non-confidential data in key value pair. 

k create configMap <name> --from-literals=<key=value> 

we can also create a configMap yaml file and add it to the pod. 
