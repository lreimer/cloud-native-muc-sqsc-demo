# Enterprise Cloud Native for SME - Demo

The demo instructions for the Cloud Native Night demo with SquareScale.

https://www.meetup.com/de-DE/cloud-native-muc/

## Login to SquareScale

```
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

$ sqsc project remove -yes cloud-native-night-dev
$ sqsc project remove -yes cloud-native-night
```

## Webhook Integration

```
$ sqsc project slackbot cloud-native-night https://hooks.slack.com/services/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
$ sqsc project slackbot cloud-native-night-dev https://hooks.slack.com/services/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
```

## Working with Repositories

```
$ sqsc repository add -project cloud-native-night-dev -build-service internal -url https://github.com/lreimer/cloud-native-muc-sqsc-nodejs
$ sqsc repository list -project cloud-native-night-dev
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

$ sqsc env set -project cloud-native-night-dev MESSAGE 'Hello Demo.'
```

## Working with Load Balancer

```
$ sqsc lb list -project cloud-native-night-dev
$ sqsc lb url -project cloud-native-night-dev
$ sqsc lb set -project cloud-native-night-dev -container lreimer/cloud-native-muc-sqsc-nodejs -port 8080
$ http get http://www.production.cloud-native-night-dev.squarely.io
```
