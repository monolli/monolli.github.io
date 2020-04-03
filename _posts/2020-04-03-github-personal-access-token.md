---
title: "How to use the GNOME Keyring to secure a GitHub Personal Access Token?"
excerpt: "This is a tutorial that shows how to properly store the token after configuring the two-factor authentication."
date: 2020-04-03T01:20:00-00:00
categories:
  - Blog
---

Yesterday a finally configured the multi-factor authentication (MFA) for my GitHub account, "better late than never", and as soon as tried to push some code I received an "authentication failed" message. And it makes sense, I added a second authentication step.

Long story short, in order to continue using Git on the command line they suggest the usage of a "GitHub Personal Access Token" in place of the password. The problem then is that it should be treated as a password and you don't want to memorize a 40-byte token. It sounds tricky, but don't worry, there is a light at the end of this non-SSH tunnel (we will use HTTPS).

1. First of all, **this tutorial is for Linux systems**. If you are not using one, that's the problem, go get one.

2. If you already configured the two-factor authentication (2FA) and still don't have a token, follow [these instructions](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line){:target="\_blank"} and come back.

3. Now, be sure that you have the GNOME Keyring installed in your Linux. Use the package manager of your preference.

4. You will also need to install the libsecret package. It is going to be used to communicate with your Git when trying to push your code over HTTPS. Use the package manager of your preference.

5. The installation steps are over, time to configure the communication between your Git and your keyring, to do so, use the following command:

    ```sh
    git config --global credential.helper /usr/lib/git-core/git-credential-libsecret
    ```

6. The first time you perform an action that requires authentication, pushing some code for example, you will be asked the Personal Access Token, use it so the keyring can read it and store it. Do it now before you lose your token :) .

7. Try to push your code again, and now use your username and your **system password**, the password used to unlock the keyring.

That's it, from now on you will only need your system password.

Have a safe push.
