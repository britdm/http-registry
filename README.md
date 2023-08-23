# http-registry

version 2.0

## quickstart

Setup a local private Docker registry with basic auth for testing.

Deploy the registry using docker, the `restart` flag will allow the registry to always run when the Docker Engine starts up on port 5000.

```
    docker run -p 5000:5000 --restart always --name registry brittanym/registry:2.0
```

When running this registry as is, it is insecure and uses self-signed certs.

### optional

Follow the [Deploy a plain HTTP registry](https://docs.docker.com/registry/insecure/#deploy-a-plain-http-registry) section to add the insecure registry to the Docker host and follow the next section [Use self-signed certificates](https://docs.docker.com/registry/insecure/#use-self-signed-certificates) to add the custom certificate so that the Docker daemon will trust the registry.

## login information

The authorization file was created using htpasswd. Use `docker login` to authenticate with the registry, username `admin` and password `admin123`.

Login:
```docker login localhost:5000 -u admin```

### modify default admin password

The default password can be modified by overwriting the htpasswd file at `/auth/.htpasswd`:
```htpasswd -Bbn admin [new_password] > /auth/.htpasswd```

To manually add another user using htpasswd use the previous command with a few modifications:

1. replace `>` with `>>`
2. replace the username `admin` with the new username

## build

To build an image with unique or secure specifications, use the Dockerfile provided in this repo. A docker image is available to pull directly from [Docker Hub](https://hub.docker.com/r/brittanym/registry). 

The defaults of this project are not secure and should not be deployed directly into a production environment.
