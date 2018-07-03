# Enterprise Cloud Native for SME with Squarescale

The demo instructions for the Cloud Native Night demo with SquareScale. https://www.meetup.com/de-DE/cloud-native-muc/

## Logging into SquareScale

```
$ sqsc status
$ sqsc login
```

## Managing Projects

```
# create a single node project for development
$ sqsc project create -infra-type "single-node" -name "cloud-native-night-dev"

# create a HA project and cluster
$ sqsc project create -infra-type "single-node" -name "cloud-native-night-dev"

$ sqsc project list
$ sqsc project remove -yes cloud-native-night-dev
```

## Webhook Integration

```
$ sqsc project slackbot cloud-native-night https://hooks.slack.com/services/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
$ sqsc project slackbot cloud-native-night-dev https://hooks.slack.com/services/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
```
