# Docker on CoreOS with Vagrant

This provides the (imho easiest) way on how to run Docker on CoreOS via Vagrant.
Vagrant uses [`boot2docker`](https://atlas.hashicorp.com/mitchellh/boxes/boot2docker)
as a default Linux distribution for Docker, but it can be told to use CoreOS
via a Vagrantfile option.

## More resources

http://docs.vagrantup.com/v2/docker/basics.html

## Requirements (for OSX)
 - Homebrew (= XCode CLI tools too)
 - `brew cask tap caskroom/homebrew-cask`
 - `brew cask install virtualbox vagrant`

## Usage

Spin up the docker container(s) + host OS (CoreOS)

```
vagrant up
```

run some one-off commands in the container through Vagrant

```
vagrant docker-run -- redis-cli --version
```

or connect to the host VM (the host VM is not visible through `vagrant status`)

```
$ vagrant global-status
id       name    provider   state   directory                             
--------------------------------------------------------------------------
538c0cb  default virtualbox running /private/var/workspace/vagrant/docker 
5a669f1  default docker     running /private/var/workspace/vagrant/docker 

$ vagrant ssh 538c0cb
```

and play around with docker directly

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS               NAMES
3869edd06c1f        redis:2             "/entrypoint.sh redi   27 minutes ago      Up 17 minutes       6379/tcp            docker_default_1420655258

$ docker run -it --link docker_default_1420655258:redis --rm redis sh -c 'exec redis-cli -h "$REDIS_PORT_6379_TCP_ADDR" -p "$REDIS_PORT_6379_TCP_PORT"'
172.17.0.4:6379> SET name Radek
OK
172.17.0.4:6379> GET name
"Radek"
```
