Inevitably you will find yourself needing to access multiple GitHub accounts, like when you start working for a [kickass company](https://github.com/Allied-Steel-Buildings) as I did.  The thought occurred to me, why not automate this process with a simple alias that can be run from the command line so that we need not ever have to re-research and re-read dry, often overly-opinionated user generated walkthroughs.

This walkthrough assumes you have already setup your SSH credentials for your personal GitHub account [as instructed here](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).


# One Line to Rule them All...
Here is the final line of code we will ultimately be running to accomplish this goal.
Note that you will need to replace my username with your own (obs).

```
git addnewaccount
```

Beautiful, isn't it?

# Let's Get Started
Switching between accounts require two things:

1. Changing the `ssh` key,
2. And changing the git `user.email` setting.

## Generate SSH Keys

No surprise here - we'll need to generate a unique SSH key for our second GitHub account.

```
ssh-keygen -t rsa -C "your-email-associated-with-the-second-account"
```

We do not want to over-write our existing key that is attached to our personal account.  So this is where our path with divert from the standard SSH setup as outlined on the GitHub help pages.  Instead, when prompted, explicitly save the file like so - replacing "COMPANY" with the name of your second account:

```
~/.ssh/id_rsa_COMPANY
```

## Attach the New Key

Next, login to your second GitHub account, browse to "Account Overview," and attach the new key, within the "SSH Public Keys" section. To retrieve and copy the value of the key that you just created, return to the Terminal, and type:

```
pbcopy ~/.ssh/id_rsa_COMPANY.pub
```

Next, because we saved our key with a unique name, we need to explicitly convey that name to the SSH. Within the Terminal, type:

```
ssh-add ~/.ssh/id_rsa_COMPANY
```

If successful, you'll see a response of "Identity Added."

## Create a Config File

We've done the bulk of the workload; but now we need a way to specify when we wish to push to our personal account, and when we should instead push to our company account. To do so, create a config file and open that file in our editor of choice.

```
touch ~/.ssh/config
atom ~/.ssh/config
```

## Automate SSH Key Additions

In the config file, insert the code snippet below:

```
# Default Personal GitHub
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa

# Second github alias
Host github_COMPANY
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_COMPANY
```

Notice that we're able to attach an identity file to the host and add another one for the second "COMPANY" account. Save and exit the config file.

Now we can access and update repos in our second account by running standard porcelain commands with the newly defined custom host `github_COMPANY` like so:

```
git remote add origin git@github_COMPANY:hkdeven/GitHub-InDepth.git
```

#U pdate Git user.email

Navigate and open the `~/.gitconfig` file.

```
atom ~/.gitconfig
```

Copy and paste the code below under alias making sure to update the applicable fields.

```
[alias]
  changeremotehost = !sh -c \"git remote -v | grep '$1.*fetch' | sed s/..fetch.// | sed s/$1/$2/ | xargs git remote set-url\"
  setnewaccountemail = "config user.email 'your-email-associated-with-the-second-account'"
  addnewaccount = !sh -c \"git changeremotehost github.com github_COMPANY && git changeremotehost && git setnewaccountemail\"
```

This allows us to change all remotes from one host to another (the alias).

## Execute

Now we can simply run a command similar to this:

```
git clone git@github.com:COMPANY/project.git
cd project
git addnewaccount
```

Additional GitHub accounts can be added in the future by simply generating a new SSH key, saving it to an explicit path, and updating the `/.gitconfig` file accordingly - as outlined above.

Enjoy.  :)
