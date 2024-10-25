# TorSimulation

**K8s-Enhanced Lightweight Simulation Method for the Tor Network**

We divide the deployment into three phases: **Creating Docker Images**, which is used to prepare the necessary Tor relay images; **K8s Cluster Build**, which is used to set up the K8s cluster environment; and **Build a Private Tor Network**, which is used to networking in order to build a Tor network simulation environment. The order of execution of **Creating Docker Images** and **K8s Cluster Build** can be interchanged.

## Creating Docker Images

We use ```Dockerfile``` to make images of different Tor relays, the core of which is to make the Tor program use different ```torrc``` configuration files. The configuration files for the different kinds of Tor relays are shown in the ```torrc_s``` folder, ```au_torrc```: Directory Authority Server, ```client_torrc```: Onion Proxy, ```exit_torrc```: Exit relay, ```onion_torrc```: Hidden Service, and ```router_torrc```: Normal relay.

## K8s Cluster Build

We use ```Kubeadm``` to set up the K8s cluster environment, see https://kubernetes.io/docs/reference/setup-tools/kubeadm/.

## Build a Private Tor Network

The networking process is shown in the following figure, where the Pod of the Directory Authority Servers is started first, and then the Pods of the other relays are started to add them to the private Tor network. Note that the ```DirAuthority XXX orport=XXXX no-v2 hs v3ident=XXXXX 9.0.0.1:9000 XXXXXXX``` in the ```torrc``` configuration file should be configured as the IP, port and fingerprint of the Directory Authority Servers.

![组网](https://github.com/user-attachments/assets/5b2505d7-d167-4f10-b44b-9fb4a29a92f7)



