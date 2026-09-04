# Ghost application stack for Kubernetes on Wodby

Deploy Ghost with MySQL and transactional email support on Kubernetes using Wodby.

This repository defines the Wodby stack manifest and default service composition for Ghost.

- [Ghost stack on Wodby](https://wodby.com/stacks/ghost)
- [Browse Wodby application stacks](https://wodby.com/stacks)
- [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/)
- [Stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)

## Service definitions

- [Ghost service](https://github.com/wodby/service-ghost)
- [MySQL service](https://github.com/wodby/service-mysql)
- [OpenSMTPD service](https://github.com/wodby/service-opensmtpd)

## What's included

| Component / service | Default configuration |
| --- | --- |
| Ghost (`ghost`)<br>`ghost` | required; main HTTP service; one replica; 20 GB content volume |
| MySQL (`mysql`)<br>`mysql` | required; MySQL 8; one replica; 20 GB data volume |
| OpenSMTPD (`opensmtpd`)<br>`opensmtpd` | required; relays Ghost transactional email |

Ghost supports MySQL 8 in production; MariaDB is not supported. Configure an SMTP integration for OpenSMTPD and set
Ghost's required email sender to an address accepted by that provider.

Ghost 6 persists files in `/var/lib/ghost/content`. A future Ghost 7 option will require an explicit storage migration
and must not be introduced as a compatible image update.

## Deploy this stack

Add this stack from the Wodby catalog, configure the email sender and OpenSMTPD relay integration, then create the app.
The Ghost administration interface is available at `/ghost/` on the main application route.

Review storage sizes and resource allocations when creating production applications. Ghost runs as one application
replica; use an external CDN or cache for additional delivery capacity rather than increasing the replica count.

## Maintain a custom version

1. Fork this repository.
2. Edit `stack.yml`.
3. Import the repository as a [Git-backed stack](https://wodby.com/docs/2.0/stacks/create/#create-a-git-backed-stack).

When replacing or renaming a stack service, update every related link target. Stack-local names and referenced service
names are distinct identifiers.

Validate the manifest with:

```bash
wodby stack validate-manifest stack.yml --org <org-id>
```

See the [managed stacks index](https://github.com/wodby/stacks) for other Wodby application stacks.
