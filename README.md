# Setup

```sh
echo "export DOKKU_APP=APP_DOMAIN_NAME" >> .envrc
echo "export DOKKU_HOST=HOSTNAME" >> .envrc
echo "export LIVEBOOK_PASSWORD={{password of at least 12 characters}}" >>.envrc
direnv allow
dokku apps:create $DOKKU_APP
dokku proxy:ports-set $DOKKU_APP 'http:80:8080 https:443:8080'
dokku config:set --no-restart $DOKKU_APP DOKKU_DOCKERFILE_PORTS="8080/tcp"
dokku config:set --no-restart $DOKKU_APP LIVEBOOK_PASSWORD=$LIVEBOOK_PASSWORD
dokku domains:add $DOKKU_APP $DOKKU_APP
git remote add dokku dokku@$DOKKU_HOST:$DOKKU_APP
```

# Deploy

```sh
git push dokku
```

# Certificate

```
dokku config:set --no-restart $DOKKU_APP DOKKU_LETSENCRYPT_EMAIL=EMAIL
dokku config:set --no-restart $DOKKU_APP DOKKU_LETSENCRYPT_SERVER=staging
dokku letsencrypt:enable $DOKKU_APP
# and, when it works...
dokku config:unset --no-restart $DOKKU_APP DOKKU_LETSENCRYPT_SERVER
dokku letsencrypt:enable $DOKKU_APP
```
