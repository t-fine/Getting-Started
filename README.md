## Welcome to the Open Horizon Services project!

This project was created to house edge micro-services that can be easily built, tested, and published to any open horizon management hub.

## Learn more about Open Horizon 
**Open Horizon documentation repository coming soon!** For the time being, you can learn more about [Open Horizon here](https://www.ibm.com/support/knowledgecenter/SSFKVV_4.2/kc_welcome_containers.html).

## Management Hub Installation
Before you can publish and use any of the services in this repository, you must first deploy your own Horizon Management Hub. This can be done with one simple command using the `deploy-mgmt-hub.sh` script located in the [devops repository](https://github.com/open-horizon/devops/tree/master/mgmt-hub#horizon-management-hub). This will give you with a Management Hub with several services, policies and patterns published in the exchange. 

## Register an Edge Node with your Management Hub
Edge nodes must first be registered with a Management Hub before services can be deployed to them. The `agent-install.sh` script is a fast and easy way to register an edge node with a Management Hub, more information can be found in the [open-horizon/anax](https://github.com/open-horizon/anax/tree/master/agent-install#edge-node-agent-install) repository. Edge nodes can be either a device or a cluster. Open Horizon edge cluster capability helps you manage and deploy workloads from a management hub cluster to remote instances of OpenShift® Container Platform or other Kubernetes-based clusters. 

Typically, **edge devices** have a prescriptive purpose, provide (often limited) compute capabilities, and are located near or at the data source. Currently supported edge device OS and architectures:
* x86_64
  * Linux x86_64 devices or virtual machines that run Ubuntu 20.x (focal), Ubuntu 18.x (bionic), Debian 10 (buster), Debian 9 (stretch)
  * Red Hat Enterprise Linux® 8.2
  * Fedora Workstation 32
  * CentOS 8.2
  * SuSE 15 SP2
* ppc64le (Horizon Agent version >=2.28)
  * Red Hat Enterprise Linux® 7.9
* ARM (32-bit)
  * Linux on ARM (32-bit), for example Raspberry Pi, running Raspberry Pi OS buster or stretch
* ARM (64-bit)
  * Linux on ARM (64-bit), for example NVIDIA Jetson Nano, TX1, or TX2, running Ubuntu 18.x (bionic)
* Mac
  * macOS

## Contributing a New Microservice 

If you have a service you would like to contribute to the `open-horizon-services` project, please create a post on the Matrix chat server [open-horizon-examples](https://chat.lfx.linuxfoundation.org/#/room/#open-horizon-examples:chat.lfx.linuxfoundation.org) channel and tag it with `#new-edge-service`. In your post, please provide a brief description of the service you want to add, the desired name, and a list of the github usernames of each maintainer/contributor you would like added to your new repo(s). **Please note**, we do have a naming convention where microservices designed to be a building-block and incorporated into a variety of edge solutions, like [service-mqtt](https://github.com/open-horizon-services/service-mqtt), are prepended with `"service-"`.

Each service in the `open-horizon-services` project has a similar structure, and set of files, in an attempt to make each service as easy as possible to build, test, publish, and deploy. See the [web-helloworld-python](https://github.com/open-horizon-services/web-helloworld-python) service for an example of the minimum set of files a service should have.

#### Makefile targets for microservices

- `init` - mostly used for operator services to create the scaffolding of a new operator, or any form of code generation required to build
- `build` - build the container
- `dev` - open a shell in the container, for development, with source dir mounted. See [web-helloworld-python](https://github.com/open-horizon-services/web-helloworld-python/blob/89ecbea75dfbd40ab939a711c879db81907120d1/Makefile#L18) for an example of how this is done
- `run` - run container locally
- `stop` - stop and remove the container
- `agent-run` - deploy the container to your edge node using the agent
- `agent-stop` - stop the container running from `agent-run` 
- `test` - assumes container is running. See [web-helloworld-python](https://github.com/open-horizon-services/web-helloworld-python/blob/89ecbea75dfbd40ab939a711c879db81907120d1/Makefile#L31) for one example of how this can be done
- `push` - to docker compliant registry
- `publish` - verify and publish the service
- `clean` - calls stop and also removes the container image
- `distclean` - clean as much as possible, e.g., remove all container and all images, and docker network prune, etc.

#### Files for microservices

Each service should at least have a service definition json file that can be used to publish the service to a management hub. See the `service.json` file of the [web-helloworld-python](https://github.com/open-horizon-services/web-helloworld-python/blob/main/service.json) service for an example. 

## Contributing a new top-level service designed to be a deployment pattern or deployment policy

Similar to the instructions above for contributing a microservice, if you want to add a top-level service that is designed to be used as a deployment pattern or policy, we ask you still create a post on the Matrix chat server [open-horizon-examples](https://chat.lfx.linuxfoundation.org/#/room/#open-horizon-examples:chat.lfx.linuxfoundation.org) channel and tag it with `#new-edge-service`, provide a brief description of the service, and include a list of the github usernames of each maintainer/contributor you would like added to your new repository. However, the name of your edge solution should be capitalized, similar to the `Achatina` **(add link when we have it merged)** service.

#### Makefile targets for top-level services designed to be a deployment pattern or deployment policy

- `init` - mostly used for operator services to create the scaffolding of a new operator, or any form of code generation required to build
- `build` - build the container
- `dev` - open a shell in the container, for development, with source dir mounted. See [web-helloworld-python](https://github.com/open-horizon-services/web-helloworld-python/blob/89ecbea75dfbd40ab939a711c879db81907120d1/Makefile#L18) for an example of how this is done
- `run` - run container locally
- `stop` - stop and remove the container
- `agent-run` - deploy the container to your edge node using the agent
- `agent-stop` - stop the container running from `agent-run` 
- `test` - assumes container is running. See [web-helloworld-python](https://github.com/open-horizon-services/web-helloworld-python/blob/89ecbea75dfbd40ab939a711c879db81907120d1/Makefile#L31) for one example of how this can be done
- `push` - to docker compliant registry
- `publish-service` - verify and publish the service
- `publish-pattern` - publish the pattern using the properties defined in the `pattern.json` file
- `register-pattern` - register an edge node with the published pattern
- `clean` - calls stop and also removes the container image
- `distclean` - clean as much as possible, e.g., remove all container and all images, and docker network prune, etc.

#### Files for a top-level service designed to be a deployment pattern or deployment policy

Each service designed to be composed as a deployment pattern should at least have a service definition json file, and a deployment pattern json that can be used to publish the service to a management hub. See the `service.json`, and `pattern.json` file of the `Achatina` **(add link when we have it merged)** service for an example.
