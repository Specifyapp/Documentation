---
description: >-
  In this guide you’ll learn how to sync your design tokens from Tokens Studio
  to your Specify repository and how to keep them updated.
---

# Tokens Studio

[Before getting started](tokens-studio.md#before-getting-started)\
[1. Sync your design tokens from Tokens Studio to a provider](tokens-studio.md#1.-sync-your-design-tokens-from-tokens-studio-to-github)\
[2. Add your JSON file from a provider to your Specify Repository](tokens-studio.md#2.-add-your-json-file-from-a-provider-to-your-specify-repository)\
&#x20;   [From a public URL](tokens-studio.md#from-a-public-url)\
&#x20;   [From a private URL](tokens-studio.md#from-a-private-url)\
[3. How to update your JSON File](tokens-studio.md#3.-how-to-update-your-json-file)\
[4. Non-supported design token types](tokens-studio.md#4.-non-supported-design-token-types)

### Before getting started

To get the most out of this guide, you will need:

* A [Specify](http://specifyapp.com/) account
* Access to the [Specify SDTF Beta](https://specifyapp.com/design-token-format)
* The [Tokens Studio](https://tokens.studio/) plugin installed in your Figma
* A [GitHub](https://github.com/), [JSONBin](https://jsonbin.io/), [GitLab](https://gitlab.com/), or [Azure DevOps](https://dev.azure.com/) account

Specify automatically fetches Tokens Studio design tokens through the JSON file provided by the latter. The best way to keep your design tokens in sync with both tools is to host your JSON file in a repository like GitHub.



### 1. Sync your design tokens from Tokens Studio to a provider

1. Head to your Tokens Studio plugin in Figma
2. Within the settings tab, add a new sync provider.
3. Commit your Tokens Studio JSON file to your repository.

{% hint style="info" %}
You can also manually export your file from Tokens Studio and upload it manually to your code repository. Click on **Tools** on the bottom left of the plugin and **Export to file/folder**. Be careful to tick all the boxes before exporting. We are not supporting multiple files at the moment.
{% endhint %}

###

### 2. Add your JSON file from a provider to your Specify Repository

1. Go to your Specify workspace
2. Click on `Create repository`
3. Choose a name
4. Select `Sync from Figma Variables & Tokens Studio` ([Learn more ↗︎](https://help.specifyapp.com/en/articles/7983267-what-type-of-repository-do-i-need))
5. Click on `Create repository`
6. In the `Source` tab, click on `Create a source`
7. Select `Remote URL`

At this point, you have two ways to sync your JSON file. Either with a public hosting link or a private one. We will go through both options below.

#### **From a public URL**

1. In the `Source` tab, click on `Create a source`
2. Select `Remote URL`
3. Select `Public`
4. Give a `name` to your source
5. Paste your public URL
6. Select the format `Tokens Studio`
7. Let Specify check the connection
8. And _voila!_

Your JSON file is now detected as a source and your design tokens appear within your repository.

#### **From a private URL**

On the opposite of the public URL, Specify will ask you for some additional information so its system is able to fetch your file. Let’s see how to proceed with the main versioning tools:

* [GitHub](tokens-studio.md#github)
* [Azure DevOps](tokens-studio.md#azure-devops)
* [GitLab](tokens-studio.md#gitlab)
* [JSONBin](tokens-studio.md#jsonbin)

#### **GitHub** <a href="#github" id="github"></a>

Requirements:

* Have a GitHub account
* Have a repository created
* Have a JSON file containing design tokens from Tokens Studio

To add a private URL source from GitHub to Specify:

1. In the `Source` tab of your Specify repository, click on `Create a source`
2. Select `Remote URL`
3. Select `Private`
4. Give a name to your source
5. Paste your GitHub file URL such as `https://api.github.com/repo/{owner}/{repo}/contents/{file_path}`\
   [Learn more in the GitHub documentation](https://docs.github.com/en/rest/repos/contents?apiVersion=2022-11-28)
6. Select `Bearer Token` as auth system & paste your `personal access token` from GitHub (Create an [access token here ↗︎](https://github.com/settings/tokens) and be sure to enable **Repo Access**)
7. Select `Tokens Studio Format`
8. Specify will test your JSON
9. And _voila!_

#### **Azure DevOps**

Requirements:

* Have an Azure DevOps account
* Have a Project containing a repository
* Have a JSON file containing design tokens from Tokens Studio

To add a private URL source from Azure DevOps to Specify:

1. In the `Source` tab of your Specify repository, click on `Create a source`
2. Select `Remote URL`
3. Select `Private`
4. Give a `name` to your source
5. Paste your Azure DevOps file URL such as `https://dev.azure.com/{OrgName}/{ProjectName}/_apis/git/repositories/{RepositoryName}/items?path={FilePath}&api-version=7.0&includeContent=true`
   1. [Learn more in the Azure DevOps documentation](https://learn.microsoft.com/en-us/rest/api/azure/devops/git/items/get?view=azure-devops-rest-7.0\&tabs=HTTP)
6. Select `Basic Auth` as auth system & fill in your credentials
7. Select `Tokens Studio Format`
8. Specify will test your JSON
9. And _voila!_

#### **GitLab**

Requirements:

* Have a GitLab account
* Have a repository created
* Have a JSON file containing design tokens from Tokens Studio

To add a private URL source from GitLab to Specify:

1. In the `Source` tab of your Specify repository, click on `Create a source`
2. Select `Remote URL`
3. Select `Private`
4. Give a `name` to your source
5. Paste your GitLab file URL such as `https://gitlab.com/api/v4/projects/{OrgName}%2F{RopositoryName}/repository/files/{FilePath}?ref={branch}`
   1. [Learn more on the GitLab documentation](https://docs.gitlab.com/ee/api/rest/index.html#personalprojectgroup-access-tokens)
6. Select `Header` as auth system
   1. Fill `PRIVATE-TOKEN` in the `key` field
   2. Paste your GitLab personal access token
7. Select `Tokens Studio Format`
8. Specify will test your JSON
9. And _voila!_

#### **JSONBin**

{% hint style="warning" %}
JSONBin only works if you import the JSON manually in JSONBin. If you are using the direct connection to the provider from Tokens Studio settings, it cannot work today.
{% endhint %}

Requirements:

* Have a JSONBin account
* Have a bin with a JSON file containing design tokens from Tokens Studio

To add a private URL source from JSONBin to Specify:

1. In the `Source` tab of your Specify repository, click on `Create a source`
2. Select `Remote URL`
3. Select `Private`
4. Give a `name` to your source
5. Paste your BIN private URL such as `https://api.jsonbin.io/v3/b/{bin_id}`
6. Select `Header` as auth system
7. Depending on your choice, you can use your `master key` or an `access key`. [Head toward this page](https://jsonbin.io/app/app/api-keys) on JSONBin.
   1. Following your choice, fill in the `key` field either with `X-MASTER-KEY` or `X-ACCESS-KEY`
   2. Paste your key in the `value` field
8. Select `Tokens Studio Format`
9. Specify will test your JSON
10. And _voila!_



### 3. How to update your JSON File

After adding your source. All you have to do is to:

1. Go in the `Source` tab of your Specify repository
2. Click on the context menu next to your source
3. Click on `sync`

Your source is now updated!

### 4. Non-supported design token types

Specify is yet not compatible with the following options of Tokens Studio:

* Math
* Composition
* Assets (bitmap & vectors)
* Color manipulation (alpha, darken, lighten & mix)

They will be released in future updates. However, if you have urgent needs for Specify to be compatible with one of them, [feel free to send us feedback](https://feedback.specifyapp.com/beta-program).