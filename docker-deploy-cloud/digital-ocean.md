# Digital Ocean

Digital ocean is a powerful way we have to deploy our application on the cloud. 

I already have some experience with this platform, I used it for a personal project once and I think I could replicate the architecture for our purposes without any problem.

Link to personal project as a reference: [moody arch on a swarm network](https://github.com/Abathargh/moody-do-swarm).


## Table of Contents
- [Digital Ocean](#digital-ocean)
  - [Table of Contents](#table-of-contents)
    - [Pros](#pros)
    - [Cons](#cons)
    - [How to](#how-to)

### Pros
- 100€ credit in the github education pack for students
- Easy to use both via website and terminal
- Native support for docker-machine based deploy and virtual node administration
- Accepts paypal
  
### Cons
- Requires a bit of knowledge of some specific tools to create the architecture from the ground up

### How to

You can create a droplet from the digitalocean web panel and access it as a normal linux server. This requires a bit more configuration than heroku.

The docker-machine support for this platform is included in the docker-machine cli, which is a tool that you have to install on your computer along with docker engine. This is an example of how to directly create a virtual private server as a docker node taken from my previously linked project. This makes it easy to log into the node or use it in a cluster with tools like swarm for orchestrating:

```bash
docker-machine create \
    --driver digitalocean \
    --digitalocean-image ubuntu-16-04-x64 \
    --digitalocean-size s-1vcpu-1gb \
    --digitalocean-region fra1 \
    --digitalocean-access-token $DOTOKEN \
    --engine-install-url "https://releases.rancher.com/install-docker/19.03.9.sh" \
    node-name
```