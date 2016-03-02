# Nginx Proxy Server for serving static files

## Setting up containers

I have two static sites I want to serve from nginx. Those sites are each
built into separate containers and stored as submodules in the repository.
Those dockerfiles build the sites (e.g.
jekyll or middleman) and then export the folders where the sites were built
via the `VOLUME` command.

You must also change the nginx.conf file to incorporate the appropriate
`server_name` and `root` parameters. The value for `root` will be the
paths to the folders you specified in the `VOLUME` command in the submodule's 
Dockerfiles.

Finally you must modify the docker-compose.yml. Make sure the nginx
container has the attributes for `volumes_from` and `depends_on` set
to the containers that rerpresent the static sites. Set the `context`
field of each container to be the location of its respective Dockerfile.

The current configuration e.g. submodules, submodule dockerfiles, nginx.conf,   
the nginx Dockerfile can all serve as a model.

## Systemd

There is also a docerized_site.service file which can be copied to
`/etc/systemd/system` and then started with `sudo systemctl start dockerized_site.service`
