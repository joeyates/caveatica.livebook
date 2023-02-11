# Setup

```sh
echo "export DOKKU_APP=APP_DOMAIN_NAME" >> .envrc
echo "export DOKKU_HOST=HOSTNAME" >> .envrc
dokku apps:create $DOKKU_APP
dokku config:set $DOKKU_APP DOKKU_DOCKERFILE_PORTS="8080/tcp"
```
