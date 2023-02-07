---
description: >-
  Learn how to distribute your design tokens and assets from Specify to your
  GitHub repositories via automated Pull Request.
---

# GitHub

{% embed url="https://www.loom.com/share/771e1001bfe84c418e8afcf07455c02e" %}

{% hint style="info" %}
By default, Specify can only syncs your GitHub repository if you have a config file `.specifyrc.json` at the root of your GitHub repository. If you want to sync design tokens from several Specify repositories you need to run the Specify CLI inside a GitHub Action.
{% endhint %}

## Prerequisites

Please make sure you have:

* A GitHub account
* A Specify account
* A Specify repository containing some design tokens and/or assets

{% hint style="info" %}
Want to connect a GitHub repository from your GitHub organization? Please make sure you have the correct access rights. Otherwise, you'll need for an owner to approve your installation request.
{% endhint %}

## Installation

1. Go to the applications catalog [on the Destinations page](https://specifyapp.com/apps/add/destinations)
2. Select GitHub
3. Click on "Connect"
4. Select the repositories you want Specify to have access to
5. You will now be able to connect your Specify and your GitHub repositories together 🎉

## Connecting Specify and GitHub

Once you've connected your GitHub account, Specify has to know what design tokens to synchronize and how.

1. Go to the Specify repository page you want to distribute design data from
2. Go to its "Destinations" page
3. Click on "Create Pipeline"
4. Select "GitHub application"
5. Select your GitHub account
6. Select the GitHub repository you want to distribute your design data to
7. Select your configuration template ([Learn more](../apps/broken-reference/))
8. Create the Pull Request containing your configuration file
9. Merge the PR created by Specify containing your configuration file
10. Specify will now automatically sync design data to your GitHub repository 🎉

## Fixing sync issues

Have trouble getting Pull Requests in your GitHub repository? Learn more about [how to fix most common issues](https://help.specifyapp.com/en/articles/4722450-how-to-use-github-as-a-destination).

## Useful resources

* [How to pull design tokens from several Specify repositories in GitHub](https://specifyapp.com/blog/how-to-pull-design-tokens-from-several-specify-repositories-on-github)
* [How to run Style Dictionary with a GitHub Action](https://specifyapp.com/blog/github-actions-style-dictionary)
