# traefiked-wordpress

This *example project* will create four services in a Docker swarm mode cluster:
* Two Wordpress services for two different wordpress sites (beluga and humpback), with labels for Traefik to load-balance
* One MariaDB database configured for Galera-based clustering using swarm mode DNS for discovery
* One Traefik proxying/load balancing container 

Note this is for demonstration purposes, only. To use this in
production, data for Traefik, WordPress, and MariaDB needs to be
stored in appropriate durable Docker Volumes

# Usage

These services can be started using the following command:
    
```
docker stack deploy --compose-file docker-compose.yml traefiked-wordpress
```

This will bring up 2 wordpress containers, a single dbcluster
container, and a traefik container.

## Testing
In this example, Traefik is configured to provide hostname-based
HTTP proxying for 2 WordPress sites: beluga and humpback. You'll
probably need to edit your hosts file to define these 2 hosts,
probably to 127.0.0.1 if you are running the composition locally
through Docker for (Mac,Windows,Linux). If you're running the stack
somewhere other than on your local machine, hopefully you'll know
the IP address that you're connecting to, and can use that in your
hosts file. Rackspace has a nice set of instructions
[here](https://support.rackspace.com/how-to/modify-your-hosts-file/) to
edit your hosts file for various OSes.

When finished, the following command shuts everything down:

```
docker service rm traefiked-wordpress_dbcluster traefiked-wordpress_beluga-wordpress traefiked-wordpress_traefik traefiked-wordpress_humpback-wordpress
```

# References
This project uses the following Docker images:
* PHP 7.1/Apache version of the [Official Docker Wordpress image](https://hub.docker.com/_/wordpress/)
* ToughIQ's [MariaDB Galera Cluster image](https://hub.docker.com/r/toughiq/mariadb-cluster/)
* The [Traefik](https://hub.docker.com/_/traefik/) load balancer
