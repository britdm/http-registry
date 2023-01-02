# http registry
version 2.0

## quickstart
Setup local private registry for testing.
```
    docker run -p 5000:5000 --rm --name registry brittanym/registry:2.0
```

### login information
The authorization file was created using htpasswd. Use `docker login` to authenticate with the registry username `admin` password `admin123`. The assumption is that there is not another docker user logged into the system where the registry is deployed.

Login:
```docker login localhost:5000 -u admin```

(Optional) The default login can be changed by overwriting the htpasswd file `/auth/.htpasswd`:
```htpasswd -Bbn admin [new_password] > /auth/.htpasswd```
To add another user replace `>` with `>>` and replace `admin` with the new username.
