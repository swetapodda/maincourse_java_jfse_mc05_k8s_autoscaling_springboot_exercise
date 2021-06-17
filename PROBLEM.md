## Exercise: Experiment with autoscaling on a K8s Cluster

* In this Exercise, you will practice scaling up and down pods in a K8s Cluster.
You will use Kubernetes Horizontal Pod Autoscaler(HPA) to scale pods.

This exercise contains following file in k8-manifests folder

	- springboot-deployment.yml - To create the deployment
	- springboot-svc - To create the service

  

To define Deployment, understand and perform the following steps: 

	1. Build the `springboot-app` Docker image for the service-app microservice and push to Docker Hub.
	2. Define a deployment named `springboot-deployment` in `springboot-deployment.yml` with 1 replica. Use the image created in the preceding step.
	3. Define a service named `springboot-svc` in `springboot-svc.yml` for the deployment created in the preceding step as selector.


Understand and perform the following steps to complete this exercise:

	1. Open terminal and cd into the folder where yml files defined above are present.
	2. Run `minikube start` to start the Minikube cluster and `minikube status` to make sure that the Minikube cluster is running.
	3. Run command `kubectl apply -f springboot-deployment.yml` to create deployment.
	4. Run command `kubectl get pods` to watch your Pod coming alive.
	5. Run command `kubectl apply -f springboot-svc.yml` to create service.
	6. Run command `minikube addons enable metrics-server` to enable metrics server.
	7. Run command `kubectl autoscale deployment <deployment-name> --cpu-percent=50 --min=1 --max=10` to autoscale pods whenever CPU load exceeds 50%. Ensure that the minimum and maximum number of running pods is one and ten respectively.
	8. Run command `kubectl get hpa` to check the current status of the autoscaler.
	9. Run command `kubectl run -it --rm load-generator --image=busybox /bin/sh` in a different terminal to start a new container.
	10. Run command `while true; do wget -q -O- http://<minikune-ip>:<NodePort>/api/v1/hello; done` in a different terminal to send request to the server.
	11. Again run the command in step 8 to check how the autoscaler reacts to the increased load on the server.
	12. Run command `kubectl get pods` to check the number of pods running.
	13. Exit the terminals of step 9 and step 10 to terminate the loops sending requests to the server and stop the user load.
	14. Run command `kubectl get pods` to see the pods scaling down.


### Instructions

- Take care of whitespace/trailing whitespace
- Do not change the provided code unless instructed
- Ensure your code compiles without any errors/warning/deprecations
- Follow best practices while coding