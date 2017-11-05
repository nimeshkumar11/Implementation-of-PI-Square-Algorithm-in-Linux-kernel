# Implementation of PI2 algorithm in Linux kernel

## Course Code: CS822

## Assignment: #FP5

### Overview
PI2 or PISQUARE [1] is a simplified implementation of PIE AQM [2]. It is expected to perform similar to PIE (or sometimes better). This repository contains an implementation of PISQUARE in the Linux kernel.

### Steps to build the modified kernel with PISQUARE AQM

1. Download or clone this repository on your local machine

2. Configure the kernel

   `make menuconfig`

3. Compile the kernel

   `make`

4. Build and install the modules

   `make modules`

   `make modules_install`

5. Install the kernel

   `make install`

### Steps to test the functionality of PISQUARE AQM by using Flexible Network Tester (Flent) [3]

   1. Setup a physical topology of three nodes:

      Client <---> Router <---> Server

   2. Create a separate passwordless SSH connection between client and router machines, so that Flent can collect queue statistics from the router machine

   3. Install Netserver in server machine

   4. Install Flent in client machine

   5. Install the modified kernel with PISQUARE algorithm in router machine

   6. Run Flent for plotting different graphs

### Syntax of the command to run Flent

`./run-flent rrul -p [PLOT_NAME] -l 160 -H [SERVER_IP] --test-parameter bandwidth=800M --test-parameter qdisc_stats_hosts=[ROUTER_SSH_IP] --test-parameter qdisc_stats_interfaces=[ROUTER_AQM_INTERFACE] --test-parameter upload_streams=num_cpus --test-parameter download_streams=num_cpus -t PIESQUARE -o ~/Desktop/PIESQUARE/test.png`

PLOT_NAME - The type of graph needed

SERVER_IP - IP Address of the server

ROUTER_SSH_IP - IP Address using which ssh connection is setup with router

ROUTER_AQM_INTERFACE - Interface name of the router where AQM is installed

### Example command to run Flent

`./run-flent rrul -p all_scaled -l 160 -H 172.16.10.2 --test-parameter bandwidth=800M --test-parameter qdisc_stats_hosts=192.168.20.2 --test-parameter qdisc_stats_interfaces=eth1 --test-parameter upload_streams=num_cpus --test-parameter download_streams=num_cpus -t PIESQUARE -o ~/Desktop/PIESUARE/test.png`

### References

[1] De Schepper, K., Bondarenko, O., Tsang, I. J., & Briscoe, B. (2016, November). PI2: A Linearized AQM for both Classic and Scalable TCP. In CoNEXT (pp. 105-119).

[2] Pan, R., Natarajan, P., Piglione, C., Prabhu, M. S., Subramanian, V., Baker, F., & VerSteeg, B. (2013, July). PIE: A lightweight control scheme to address the bufferbloat problem. In High Performance Switching and Routing (HPSR), 2013 IEEE 14th International Conference on (pp. 148-155). IEEE.

[3] Flent: The FLExible Network Tester (https://flent.org/)
