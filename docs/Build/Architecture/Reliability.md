# Reliability

Almost all of the business and technical components are deployed over kubernetes.
Some of the architectural benefits we derive from using Kubernetes are

 * Simplified scaling
     - Scale components vertically by increasing/decreasing available Memory and CPU
     - Scale components up and down automaticaly based on load using the Horizontal Pod Autoscaler (HPA).
     - Scale compute nodes automatically using the AWS node auto-scaler using node compute thresholds. This in turn allows the HPA to make use of additional compute available
 * Simplified deployment
     - Automated deployments and upgrades using Helm
     - Component configuration via ConfigMaps and Secrets
 * Simplified Reliability
     - Automatic Recovery when components fail
     - Health-checks to prevent unhealthy components from serving requests and automatic recycling of the same.
     - Built-in load balancing and fail-over

