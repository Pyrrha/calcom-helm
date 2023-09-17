# Calcom Helm

[Cal.com](https://cal.com/fr) is a powerful tool to book meetings. Using integrations, a contact can be stored into a CRM as the event booked in your Calendar. The pretty nice interface helps your leads and customers to reach you out.

## Purpose

This Chart stands for a proposal to deploy Cal.com on a Kuberbetes cluster, using Helm. It uses the [docker image](https://github.com/calcom/docker) from cal.com.

![Terminal install](.attachments/term_install.png)

## Usage

```sh
# Install
helm repo add calcom https://pyrrha.github.io/calcom-helm

# Verify
helm search repo calcom
```

### Use standalone calcom

Simply use :

```
helm upgrade --install --values values.yaml calcom calcom
```

In the value file, the ingress, ingress class and some TLS information should be provided in order to workproperly. For configuration options, please refers to **Variables** section below.

### Use calcom stack

Simply use :

```
helm upgrade --install --values values.yaml calcom-stack calcom-stack
```

For this value file, you can also configure theingress information. You can also use the postgresql fields to configure user, password and database. This is not a secure option, the recommandation leads to use another secret for this, and [postgresql.auth.existingSecret](https://github.com/bitnami/charts/blob/main/bitnami/postgresql/values.yaml).

👉 An [example of PV](https://github.com/Pyrrha/calcom-helm/blob/main/examples/pv.yaml) is provided to quickly makes you start quickly. It will be used for the database to store all information about the application. Use it at your own risks.

## Variables

Variables are taken from the latest application [env file example](https://github.com/calcom/cal.com/blob/main/.env.example). It could be some missing ones, or newly released. Feel free to open a PR to contribute by adding it.

As most of the variables contains tokens or password information, they should be stored into a **secret**. Already handled variables are located in the [deployment file](https://github.com/Pyrrha/calcom-helm/blob/main/charts/calcom/templates/deployment.yaml).

👉 You can find an [example](https://github.com/Pyrrha/calcom-helm/blob/main/examples/secret.yaml) of minimal requirements variables in the example directory.

### Mandatory runtime variables

> ⚠️ These variables must also be provided at runtime, otherwise the Chart will not work.
> They must be present in the secret referenced as secretRef in calcom's values.

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

The development of the Chart can be delayed. Please check first if the variable is present in the [deployment file](https://github.com/Pyrrha/calcom-helm/blob/main/charts/calcom/templates/deployment.yaml). If not, you can open a PR or an issue to add it. Otherwise, you can be selfish and just  override the deployment file as a template in your own configuration.