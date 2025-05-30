# Module 11 Reflection
Ivan Jehuda Angi - 2306152222 - Advance Programming A
## Tutorial: Hello Minikube
### Compare the application logs before and after you exposed it as a Service.Try to open the app several times while the proxy into the Service is running.What do you see in the logs? Does the number of logs increase each time you open the app?



* **Before Exposure:**

  * Prior to making the Pod accessible via a Service, I used the command `kubectl logs hello-node-c74958b5d-zcs8g` to view the logs. At that time, the logs only displayed the application's startup messages:

  * ![Before expose](screenshots/1.png)

  * These entries confirmed the app was running, but there was no indication of any external traffic reaching it yet.

* **After Exposure:**

  * Once I exposed the Pod using `minikube service hello-node`, I accessed the application through a web browser multiple times. Each refresh in the browser triggered a new HTTP GET request routed through the Service. When I checked the logs again, I noticed new entries corresponding to these incoming requests.

  * ![After expose](screenshots/2.png)

  * This demonstrated that exposing the Pod via a Service enables external access, allowing clients like browsers to interact with the application—each request being captured in the container’s logs.

### What is the purpose of the `-n` option and why did the output not list the pods/services that youexplicitly created?


* During the tutorial, I ran two variations of the `kubectl get pods` command:

  * `kubectl get pods`
  * `kubectl get pods -n kube-system`

* The first command, without any flags, retrieves Pods from the **default namespace**, which is where user-created resources like the `hello-node` Pod and Service are deployed by default.

* The second command uses the `-n kube-system` flag to query the **kube-system** namespace. This namespace contains core Kubernetes components such as DNS services, kube-proxy, and the dashboard.

* When I executed `kubectl get pods -n kube-system`, the `hello-node` Pod didn’t appear because it was not deployed in that namespace. This experience helped clarify the role of namespaces in Kubernetes—they serve to isolate and organize different sets of resources, effectively acting as separate virtual clusters within the main Kubernetes environment. Understanding which namespace you're operating in is essential for managing cluster resources effectively.

