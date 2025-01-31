---
description: Learn what a custom domain is and how to set it up for your space.
---

# Add a custom domain

## What is a custom domain?

Custom domain is a unique branded domain name which you can use for your space instead of using the default Snapshot's URL. The displayed website is exatly the same, the only difference being the address you can see in the browser. Have a look at the example below:

Snapshot URL: [https://snapshot.org/#/balancer.eth](https://snapshot.org/#/balancer.eth)

Custom domain: [https://vote.balancer.fi/#/](https://vote.balancer.fi/#/)

As you already have a domain with ENS, adding a custom domain **is optional.**&#x20;

## Add a custom domain to your space

{% hint style="info" %}
You cannot create a custom domain through Snapshot. Make sure that you own the custom domain before setting it up.
{% endhint %}

### 1. Fork the snapshot-spaces repository

Create a fork of the snapshot-spaces Github repository:

{% embed url="https://github.com/snapshot-labs/snapshot-spaces" %}

### 2. Add your custom domain to domains.json

Follow the Snapshot spaces directory tree and open the [domains.json](https://github.com/snapshot-labs/snapshot-spaces/blob/master/spaces/domains.json) file.

```bash
└── spaces
    └── domains.json
```

Add the mapping for your custom domain and Snapshot space in the following format:

```
"my.custom.url": "my-space.eth"
```

{% hint style="warning" %}
To prevent conflicts, it is recommended to add your subdomain between two existing domains rather than at the end or beginning of the list, as in the example below.
{% endhint %}

```javascript
{
  ...
  "other.domain.com": "ens.eth",
  "my.custom.url": "my-space.eth",
  "other.domain.com": "ens.eth",
  ...
}
```

### 3. Create a pull request

Create a Pull Request on the original [snapshot-spaces](https://github.com/snapshot-labs/snapshot-spaces/) repository with the above changes.

It can take the team around **72 hours** to merge your Pull Request, so please be patient :pray:

Once the PR is merged you will have to wait for the release of a new version on [https://snapshot.org](https://snapshot.org). It can take up to a **couple of days**. Once the new version is released you can move on to the next step.

### 4. Update space settings

Head to your space settings on Snapshot and fill in the custom domain name field. It must match the one you added in the Pull Request.

![The domain name field in Snapshot settings.](../.gitbook/assets/capture-de-cran-2020-12-30-a-09.34.49.png)

### 5. Configure your DNS&#x20;

Update your DNS settings on the custom domain provider dashboard and set CNAME to:

`cname.snapshot.org`

### 6. Activate your domain

Once the PR is merged use the below link to activate the domain:

\
[https://ina9pk8175.execute-api.us-west-2.amazonaws.com/dev?domain=example.com](https://ina9pk8175.execute-api.us-west-2.amazonaws.com/dev?domain=example.com)\


**Replace "example.com" with your custom domain.**&#x20;

{% hint style="info" %}
Note that at this step the returned message could contain warnings, this could happen if the domain DNS zone is not fully resolved yet or if you've already successfully activated your domain. The bottom line is if you've setup the CNAME record correctly you should not worry at all.
{% endhint %}



That's all! You should now be able to use the custom domain for your space :tada:\
