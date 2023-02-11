# Setup

```sh
echo "export DOKKU_APP=APP_DOMAIN_NAME" >> .envrc
echo "export DOKKU_HOST=HOSTNAME" >> .envrc
direnv allow
dokku apps:create $DOKKU_APP
dokku config:set --no-restart $DOKKU_APP DOKKU_DOCKERFILE_PORTS="8080/tcp"
dokku config:set --no-restart $DOKKU_APP LIVEBOOK_PASSWORD={{password of at least 12 characters}}
dokku domains:add $DOKKU_APP $DOKKU_APP
dokku config:set --no-restart $DOKKU_APP DOKKU_LETSENCRYPT_EMAIL=EMAIL
dokku letsencrypt:enable $DOKKU_APP
git remote add dokku dokku@$DOKKU_HOST:$DOKKU_APP
```

# Deploy

```sh
git push dokku
```
