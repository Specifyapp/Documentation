---
description: >-
  In this guide, you’ll learn how to sync your Figma Variables and/or Styles to
  a Specify Repository and how to keep them updated.
---

# Figma Variables & Styles

{% embed url="https://www.youtube.com/watch?v=khOpD0BN-Ug" %}
How to sync Figma Variables and Styles to Specify (3min)
{% endembed %}

## Before getting started

To get the most out of this guide, you will need:

* A Specify Account
* A Figma file containing Variables and/or Styles

## 1. Sync your Figma Variables and Styles with a Specify Repository

* Access your Figma file which includes the Variables and/or Styles you would like to sync to Specify
* [Download ↗](https://www.figma.com/community/widget/1182723580740552626/Specify---Sync-Tokens-and-Assets) the Specify Widget in the Figma file which includes your Variables and/or Styles. Or update the widget if you already have it. To update the Specify Widget you have to disconnect it, remove the entire frame in all of your Figma files, and reopen the latest version of the Widget.

## 2. Connect your Specify account

1. Follow the steps in the widget to connect your account. You will need to create a personal access token and you will need to add the link to the Figma file to which the widget is added. [Watch tutorial ↗](https://help.specifyapp.com/en/articles/6837203-how-to-use-the-figma-widget)
2. Click "Connect"
3. Choose **Advanced Repository**

{% hint style="info" %}
Note: the widget can be used for syncing Figma Styles from the **Classic** repositories as well, you can switch between the two by clicking "Switch to".
{% endhint %}

## 3. Create a repository in Specify

1. Go to your Specify workspace
2. Click on "Create repository"
3. Choose a name
4. Select "**Advanced Repository**" ([Learn more ↗︎](https://help.specifyapp.com/en/articles/7983267-what-type-of-repository-do-i-need))
5. Click "Create repository"

<figure><img src="../.gitbook/assets/new-repo-sdtf.jpg" alt=""><figcaption><p>Create a repository in Specify</p></figcaption></figure>

## 4. Connect the Specify Repository in your Widget

1. Go back to your Figma file that includes the Variables and/or Styles
2. Click on "Create Source" in the Specify Widget
3. It will show you the local collections and styles that are detected
4. Select the design tokens format you want to collect from your Figma file. [Learn More ↗︎](https://help.specifyapp.com/en/articles/7947471-when-to-use-figma-styles-frames-or-variables#h\_1e8bde9199)
5. Select the Specify repository you want to sync with. You should be able to see the Repository you have just created in Specify (if not, reload the list).
6. Click "Save to Specify"
7. You will immediately see the repository listed with the latest syncing time

{% hint style="info" %}
Make sure to understand that only Advanced repositories are listed here.
{% endhint %}

<figure><img src="../.gitbook/assets/widget-sdtf-sources.jpg" alt=""><figcaption><p>Create a source in your Specify Widget in your Figma file</p></figcaption></figure>

## 5. Sync updates variables and styles on the fly

Use the `Sync` button to update your Variables and/or Styles with Specify. Now you are ready to [export your design tokens](cli.md)! 🎉&#x20;

<figure><img src="../.gitbook/assets/widget-sdtf-selected.jpg" alt=""><figcaption><p>Use the sync button to update new variables</p></figcaption></figure>



## 6. Check or delete your source inside the Specify interface

* You will see the category of design tokens that are synced on the left-hand side
* In the `Sources` section (left-hand menu), you will see your connection(s) and when the last sync between your Figma file and Specify repository has occurred.
* Delete your source by clicking on the 3 dots option menu in the source card.\
