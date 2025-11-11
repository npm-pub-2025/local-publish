# Publishing Locally

Publishing locally can be **secure**, **reliable**, and **preferred** in many situations, especially for maintainers who want full control over their release process.  
Local publishing ensures:
- Secure 2FA workflows  
- Reliable testing before publishing  
- Customizable pre- and post-publish hooks to handle all the little security details

While setup is straightforward, you should confirm a few important configuration settings first.


## TL;DR

The most important security steps are:
- Enable **2FA** on your npm account  
- Enable **Require 2FA for all write actions** for your account
- Require 2FA for publish on the package settings
- Always **log out** from the npm CLI once you are done with your release(s)


## Prerequisites

Before you begin, make sure you have:
- Node.js and npm installed  
- Access to your npm account with 2FA enabled  
- Proper permissions to publish the package

## Step 1. Enable and Require 2FA

1. Go to your **npm Account Settings**.  
2. If 2FA is not yet enabled, click **Enable 2FA** and follow the setup flow for one of the supported authentication methods.  

   ![Enable 2FA](assets/2fa-disabled.png)

3. If you already have 2FA configured, you’ll see a **Modify 2FA** section.  

   ![Modify 2FA](assets/2fa-setup.png)

4. Scroll to the bottom of the page and enable the setting to **require 2FA for all write actions**.  
   This ensures every publish, tag, or permission change is protected by your second factor.  

   ![Require 2FA](assets/2fa-required.png)

## Step 2. Publish Locally

Like with CI-based publishing, the goal here is to automate the workflow and minimize human error.  
All release steps are defined in the project’s `package.json` scripts.

To run a release, use:

```bash
npm run release [version] [tag]
```
### What this workflow does

1. Runs your test suite  
2. Versions the package (`patch`, `minor`, `major`, or a specific version like `1.0.0`)  
3. Logs in to npm (you should normally stay logged out between releases for security)  
4. Publishes with the provided dist tag  
5. Logs out of npm  
6. Pushes your Git tags  
7. Creates a draft release on GitHub  

## Step 3. Verify the Release

After publishing:
- Check your package on [npmjs.com](https://www.npmjs.com/)  
- Verify your dist tags and version history  
- Confirm the GitHub release draft looks correct, and publish it

## Tips for Secure Local Publishing

- Always log out of npm after publishing.  
- Avoid using long-lived tokens on local machines.  
- Use `.npmrc` carefully; avoid storing secrets or tokens in plain text.  

## This Example Is Opinionated

In this example we made some decisions that are purely illustrative of personal preferences, and not necessarily related to security, such as:
- While in this example we publish the npm release and then make the GitHub release proposal, it is perfectly fine to do the GitHub release first, pull it locally, and then perform the npm publication.  
- While we run the tests locally, this step may be skipped or extended depending on project needs, such as running build processes to generate assets or documentation.

## Next Example

For CI-based publishing, see the companion guide: **[Publishing from CI](https://github.com/npm-pub-2025/ci-publish)**