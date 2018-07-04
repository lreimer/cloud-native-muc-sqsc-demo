# Enterprise Cloud Native for SME - Demo

The demo instructions for the Cloud Native Night demo with SquareScale.

https://www.meetup.com/de-DE/cloud-native-muc/

## Login to SquareScale

```
$ open https://www.production.sqsc.squarely.io

$ sqsc status
$ sqsc login
```

## Managing Projects

```
# create a single node project for development
$ sqsc project create -infra-type single-node -name cloud-native-night-dev

# create a HA project and cluster
$ sqsc project create -name cloud-native-night

$ sqsc project list
```



## Webhook Integration

```
$ sqsc project slackbot cloud-native-night-dev https://hooks.slack.com/services/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

$ sqsc project slackbot cloud-native-night https://hooks.slack.com/services/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
```

## Working with Repositories

```
$ sqsc repository add -project cloud-native-night-dev -build-service internal -url https://github.com/lreimer/cloud-native-muc-sqsc-nodejs
$ sqsc repository list -project cloud-native-night-dev
```

## Working with Load Balancer

```
$ sqsc lb list -project cloud-native-night-dev
$ sqsc lb url -project cloud-native-night-dev
$ sqsc lb set -project cloud-native-night-dev -container lreimer/cloud-native-muc-sqsc-nodejs -port 8080
$ http get http://www.production.cloud-native-night-dev.squarely.io
```

## Working with Containers

```
$ sqsc container list -project cloud-native-night-dev
$ sqsc container show -project cloud-native-night-dev -name lreimer/cloud-native-muc-sqsc-nodejs

$ sqsc container set -project cloud-native-night-dev -container lreimer/cloud-native-muc-sqsc-nodejs -memory 128
$ sqsc container set -project cloud-native-night-dev -container lreimer/cloud-native-muc-sqsc-nodejs -instances 3
```

## Working with Logs

```
$ sqsc logs -project cloud-native-night-dev -f
$ sqsc logs -project cloud-native-night-dev -container lreimer/cloud-native-muc-sqsc-nodejs -f
```

## Working with Environment Variables

```
$ sqsc env get -project cloud-native-night-dev -all
$ sqsc env get -project cloud-native-night-dev

$ sqsc env get -project cloud-native-night-dev -container lreimer/cloud-native-muc-sqsc-nodejs

$ sqsc env set -project cloud-native-night-dev MESSAGE 'Hello Cloud Native Night Demo.'
```

## Working with Travis.CI

```
$ sqsc repository add -project cloud-native-night-dev -build-service travis -url https://github.com/lreimer/cloud-native-muc-sqsc-golang
$ sqsc repository list -project cloud-native-night-dev

$ sqsc lb set -project cloud-native-night-dev -container lreimer/cloud-native-muc-sqsc-golang -port 9090
$ http get http://www.production.cloud-native-night-dev.squarely.io

$ sqsc repository add -project cloud-native-night-dev -build-service travis -url  https://github.com/lreimer/cloud-native-muc-sqsc-jigsaw
$ sqsc repository list -project cloud-native-night-dev

$ sqsc lb set -project cloud-native-night-dev -container lreimer/cloud-native-muc-sqsc-jigsaw -port 9000
$ http get http://www.production.cloud-native-night-dev.squarely.io
```

## Working with Docker Images

```
$ sqsc image add -project cloud-native-night-dev -name rabbitmq:3.7.6-alpine
$ sqsc container show -project cloud-native-night-dev -type DockerImage

$ sqsc env get -project cloud-native-night-dev -container rabbitmq:3.7.6-alpine

$ echo 'rabbitmq-3-7-6-alpine.service.consul is the DNS Name'
$ sqsc env set -project cloud-native-night-dev RABBITMQ_PORT 5672
```

## Working with DBs

```
$ sqsc db list
$ sqsc db show -project cloud-native-night
$ sqsc db set -project cloud-native-night -size medium
```

## Working with Clusters

```
$ sqsc cluster set -project cloud-native-night -nowait -size 5
```

## Destroy Containers

```
$ sqsc container delete -project cloud-native-night-dev -yes lreimer/cloud-native-muc-sqsc-nodejs
$ sqsc container delete -project cloud-native-night-dev -yes lreimer/cloud-native-muc-sqsc-golang
$ sqsc container delete -project cloud-native-night-dev -yes rabbitmq:3.7.6-alpine
```

## Destroy Projects

```
$ sqsc project remove -yes cloud-native-night-dev
$ sqsc project remove -yes cloud-native-night
```
