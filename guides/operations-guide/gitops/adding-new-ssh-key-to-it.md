---
description: >-
  With SSH keys, you can connect to GitHub without supplying your username and
  personal access token at each visit. You can also use an SSH key to sign
  commits.
---

# Adding new SSH key to it

### Adding new SSH key to your GitHub account:

* Open Your "Command prompt" or "Terminal".
* Type below commands to generate SSH key

```
ssh-keygen
```

* Now a **.ssh** folder is created in your home directory. Go to that directory.

```
cd .ssh
cat id_rsa.pub
```

* copy the SSH key which we get after running the above commands.

<figure><img src="../../../.gitbook/assets/image (241).png" alt=""><figcaption></figcaption></figure>

* open GitHub and add this SSH key as shown below:
* open **Settings** and go to **SSH and** **GPG keys**

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-02 17-05-20.png" alt=""><figcaption></figcaption></figure>

* Click on **New SSH key** and paste it. Click on **Add SSH key**.
* If you want check the private key, use

```
cat id_rsa
```

