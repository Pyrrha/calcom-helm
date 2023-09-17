# Calcom Helm

Helm chart for [cal.com](https://github.com/calcom/cal.com).

## Purpose

This Chart stands for a proposal to deploy Cal.com on a Kuberbetes cluster, using Helm. It uses the [docker image](https://github.com/calcom/docker) from cal.com.

## Variables

Variables are taken from the latest application [env file example](https://github.com/calcom/cal.com/blob/main/.env.example). It could be some missing ones, or newly released. Feel free to open a PR to contribute by adding it.

As most of the variables contains tokens or password information, they should be stored into a secret. Already handled variables are located in the [deployment file](https://github.com/Pyrrha/calcom-helm/blob/main/charts/calcom/templates/deployment.yaml).

You can find an [example](https://github.com/Pyrrha/calcom-helm/blob/main/examples/secret.yaml) of minimal requirements variables in the example directory.

### Mandatory runtime variables

> ⚠️ These variables must also be provided at runtime, otherwise the Chart will not work.

| Variable | Description |
| --- | --- |
| NEXT_PUBLIC_WEBAPP_URL | Base URL of the site. |
| NEXTAUTH_SECRET | Secret en encrypt JWT used by NextAuth |
| CALENDSO_ENCRYPTION_KEY | Application Key for symmetric encryption and decryption. Must be 32 bytes for AES256 encryption algorithm |
| DATABASE_URL | Database url with credentials |

## Contributing

Work in progress. You can open an Issue at this time.

## Troubleshooting

### An application variable doesn't work on the Chart

The development of the Chart can be delayed. Please check first if the variable is present in the [deployment file](https://github.com/Pyrrha/calcom-helm/blob/main/charts/calcom/templates/deployment.yaml). If not, you can open a PR or an issue to add it.