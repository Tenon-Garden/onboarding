# git and GitHub

__TenonGarden Productions__ uses `git` and GitHub (<https://github.com/Tenon-Garden/>) for our Distributed Version Control System (DVCS).

## Anonymity

When you join __TenonGarden Productions__, you should make a new GitHub account using an extant (or new) email account. We recommend that you create an anonymous account that does not reveal any Personally Identifiable Information (PII) that could be used to expose your identity. This is not for any nefarious reason, simply for simplifying your own, and our own, online identity protections.

All GitHub public repositories will show usernames and emails of developers who commit to the repository. If your GitHub account is anonymous, and you have an anonymous email, then your identity behind your commits will inherently be anonymous, unless you reveal it yourself, otherwise.

Using a firstname or nickname in your accounts is reasonable, since a single name is likely to be generally ambiguous.

You are also, of course, free to reference your work on any __TenonGarden Productions__ developments by linking to any of the publically available sites or GitHub accounts associated with __TenonGarden Productions__. Again, the anonymity is not about restricting you, but about encouraging that you do not accidentally reveal too much personal information online. It is considered a general best practice.

Lastly, for example, just to clarify, let's say your name is "Ada Lovelace", and you own and operate `https://www.ada.dev` and `say.hello@ada.dev` for your own personal/professional portfolio and projects. If you were to use `say.hello@ada.dev` in your git commits, then anyone could see that in any commits pushed to a public GitHub repository. That means they could contact you at this email address, or visit the domain and learn about you, or lookup the WHOIS for the domain and potentially see your registered name, phone number, and address if you did not choose private registration.

Even moreso, if you had an email address like `ada.lovelace@gmail.com`, then you've exposed your full name, which again could be used to find other sites or uses of that email address, and get more personal information. Now, in general, that's not a problem, but for any business or public service that gains popularity, having that exposure may not be preferable to you or to your colleagues. Exposing your name and contact info may lead someone to connect you to the __TenonGarden Productions__ team, and allow them to figure out personal information about the other people on the team.

This isn't meant to be (overly) scary, this is just to point out the fact that we're not trying to be malicious or unduly secretive in our development here. Our account names may be anonymous, but that's purely out of caution for our own safety and sanity. We provide a contact site which will have contact information, and you can reach out to the team with any questions, of course. Our anonymity, and encouragement of anonymity is only meant to be a barrier to protect us from maliciousness, not to enable it.

So, if this is your real information:

- Ada Lovelace
- DOB: 1815-12-10
- `https://www.ada.dev`
- `ada.lovelace64@gmail.com`

Then you could anonymise it for __TenonGarden Productions__ by creating/using the following:

- Ada MapleMortise
- DOB: 1980-01-01
- `https://www.spite.dev`
- `ada_maplemrtise@gmail.com`

Sure, it's a shame that you'll have to pretend to be an Aquarius, but that's the price we pay for modern safety.

## SSH Keygen

To use GitHub, you first need to create and register an SSH key, per [these instructions](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

The command is:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Make sure though, that you replace `your_mail@example.com` with the email address you want to associate with the key-pair. For development in __Tenon-Garden Productions__ you should use your anonymous email address that was used to create your anonymous GitHub account. This will keep everything anonymous and coordinated. In this example will use `ada_maplemortise@gmail.com`.

Now that you've created the public and private key-pair, locked by the passphrase (password) that you provided (don't forget this!), you can now configure SSH.

To make it so that your `git config.email` is coordinated with your commits, we recommend creating the following block in your `~/.ssh/config` file:

```
Host github_ada_maplemortise
  Hostname github.com
  AddKeysToAgent yes
  UseKeychain yes
  PreferredAuthentications publickey
  IdentityFile [~]/.ssh/ada_maplemortise_rsa
  IdentitiesOnly yes
```

In the above example, note that we use the `ada_maplemortise_rsa` private key as the `IdentifyFile`. We authenticate by sharing the public-key, and we use `IdentitiesOnly` to confirm that the email address in the public-key matches the email set in `git config user.email`, as mentioned. If you use this setup, you can easily add multiple blocks, like the above, to your `~/.ssh/config` file and have different accounts all on your one system. This is useful if you have a personally identifiable account and a private (anonymous) account, and don't want to accidentally mix the two.

> __Note__ that we used `[~]/.ssh/...` in the above example. This is because we're trying to indicate that your private key will be in your home directory, but SSH may not expand the `~` symbol to be your home directory, depending on your system. On macOS, we've found that you need to use a full, absolute path (like `/Users/home/ada/...`) when referencing the `IdentityFile`, otherwise you'll get a file-not-found error. So be sure to replace `[~]` with a full, absolute path.'

So, now with that configured, we no longer use URLs in the form of `git@github.com:Tenon-Garden/...`, we now will say `git@github_ada_applemortise:Tenon-Garden/...` by using the value we configured as the `Host`, which will get replaced by SSH with the configured `Hostname`, which still _is_ `github.com`. This indirection is what automates the use of the public-key for identity verification, and allows us to use multiple accounts. Like if we also had `Host github_ada_lovelace` as a configuration block, we could separately do `git@github_ada_lovelace:Tenon-Garden/...` without any cross-contamination of accounts. We just need GitHub to be configured to recognize our different key for different accounts.

Once you have your local key-pair configured, you can add the public key to your personal [GitHub Settings](https://github.com/settings/ssh/new) page. Since your personal account has joined the __TenonGarden Productions__ "organization" on GitHub, you just need to be able to make/push commits through SSH with your own account. Any commits you make to __TenonGarden Productions__ repositories will then automatically be attributed to your account.

If your public key is `~/.ssh/github_ada.pub`, then you can get the text to submit into the GitHub Settings page by running:

```bash
cat ~/.ssh/ada_maplemortise_rsa.pub;
```

The output should start with `ssh-rsa` and end with your email (`ada.maplemortise@gmail.com`) that you want to associate with your commits. In the middle of those will be a string of "random" characters, which is the hashed public key. You should not share this publically, but you do need to give it to GitHub to allow commits from your local system through the `git@...` addresses.

Now you're all set to make commits.

## git Initialisation (New Repo)

Here are the steps to create a new repository locally and in GitHub, and then to configure the two together.

First, pick a unique name for your repository by using the GitHub "New" button in the <https://github.com/Tenon-Garden> account.

- Choose a unique name using `train-car-case`.
- Follow the extant naming conventions (`common-...` or `appname-...`) when relevant.
- Fill-out a reasonable but short description, this will be seen only on GitHub, and it's meant for clarifying the short name of the repo for anyone browsing the available repostories.
- __DO NOT__ create a `README` through the GitHub interface.
- __DO NOT__ choose a license through the GitHub interface.
- Most of our development is "source revealed" ("source available") designs and applications, so you usually want to choose for the repository to be "Public". If you're unsure, or you're working on new development that you don't want to reveal, yet, then feel free to make the repository "Private", since it can always be made "Public" later.

The above will create a blank git repository in GitHub, but with the name you've chosen.

Now, go to your development system and go to your development directory (it's usually preferable to create a personally organised path like `~/dev/tenon-garden/` to store things), and create a new directory (`mkdir`) with the name you just used on GitHub.

Go into (`cd`) that new directory and run the following commands, using your (anonymised) name and email:

- `git init` to initialise a git repository.
- `git config user.name "Ada MapleMortise"` to set your visible name in your commits, local to this repository.
- `git config user.email "ada.maplemortise@gmail.com"` to set your visible/registered email for your commits, local to this repository.
- `git checkout -b trunk` to assert that the mainline branch is named `trunk`.
- `touch ./README.md` to create a blank README file, which you can edit later.
- `touch ./.gitignore` to create the ignore config for git, to be able to hide files from the add/commit steps for repo management.
- `git remote add github git@<SSH-CONFIG-NAME>:Tenon-Garden/<REPO-NAME>.git` to set the remote (not yet "upstream") repository that we just created on GitHub.
  - `<SSH-CONFIG-NAME>` is the config block in `~/.ssh/config` associated with your `ada.maplemortise@gmail.com` SSH key that you should've configured above.
  - `<REPO-NAME>` should be the exact name of the new repository created on GitHub
  - Note that the url ends with `.git`, if you forget to do that you'll see a potentially confusing error message.
- `git add .` to add the current files to the pre-commit staging.
- `git commit -m "NEW: First commit for new Repository"` to make your first local commit with the blank README and `.gitignore` files.
- `git push --set-upstream github trunk` to do your first push to GitHub while also configuring the remote branch to be tracked as the upstream for your local trunk branch. This allows you to later do just `git push` and not have to say `github` or `trunk` explicitly. Though, we recommend still doing `git push github` in general, since that'll clarify what you're doing for your own history/sanity.

And now, after those steps, you should see your commits in the GitHub repository associated with your name (_via_ your `"ada.maplemortise@gmail.com"` anonymous account).


## git Setup (Existing Repo)
