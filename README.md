# A testing challenge

Hi and welcome!

If you have stumbled upon this repository, it must be because you love a good challenge, open source code and state-of-the-art tech.

## Intro
The goal of this challenge is to test the hell out of a small mixnet composed of a small amount of HOPR nodes. Wanna know what a HOPR node does? Feel free to read more in the [light introduction](https://medium.com/hoprnet/hopr-basics-episode-1-what-is-hopr-7d8cc4daf014) at medium.com.

## Setup
A mini-cluster composed of multiple HOPR nodes can be started by running the docker image `gcr.io/hoprassociation/hopr-pluto:1.92.7`. The image contains a running cluster and exports a variety of API ports for external services to latch onto individual cluster nodes ([approximate image content](https://github.com/hoprnet/hoprnet/blob/master/scripts/pluto/Dockerfile)).

Run the pluto cluster:
```bash
docker run --rm -d --name pluto_cluster gcr.io/hoprassociation/hopr-pluto:1.92.7
```

The cluster setup will take some time, note that all nodes are bootstrapped, funded and initialized. Once the process has finished, the logs of the pluto image will contain a list of open API connections along with necessary credentials. The last line in the image log output should contain the following string:

```shell
[setup-local-cluster] Terminating this script will clean up the running local cluster
```

You can observe the cluster initialization and setup by tailing the docker log output:

```shell
docker logs -f pluto_cluster
```

Note that the running image `expose`s the API ports, there is no port-mapping to the `localhost`!

## The Challange
With the running cluster it is possible to test the application. The challenge is open and will be evaluated based on delivering basic expectations:
* Test the message transport mechanism
  * Implement a Python wrapper around the API that will allow to call the send message for a specific node of the cluster in a pythonesque way
  * Idenitfy expected usage and edge cases for the message transport functionality
  * Verify that the message transport over the cluster nodes works correctly
  * Implement the `pytest` tests to thouroughly verify the message transport using the cluster
    * both sunny and rainy day scenarios
* Take care of the code
  * Organize features reasonably
  * Use clean, minimal code
  * Make sure everything runs properly
* Document the challenge
  * There's no fixed test environment layout
    * document the approach you choose
    * document any changes/deviations from the proposed setup
  * Document how to install, setup and run the test environment
  * Document the type of tests implemented and their reasoning
  * Document possible test types not supported by the current cluster setup
