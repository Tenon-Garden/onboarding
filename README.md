# Onboarding with TenonGarden Productions

This is a repository of tutorials, configuration files, and general instructions needed for anyone joining the __TenonGarden Productions__ team.

This is also where we provide the latest info about repo access, organization, and structures. Any preferred best-practices or coding-styles should be here in the onboarding repo, so that they're available to everyone in the team, from day one.

This is a public repository, so no secrets (passwords, urls, whatever...) should ever be committed here, or in any of the tutorials/configs/instructions.

## Secrets and Replacements

All files and processes should use the following syntax to represent user-input or redacted secrets.

For plain-text or code files, use double-braces, but be sure to retain quotations or any other wrapping characters:

```
my_password = "[[PASSWORD GOES HERE]]";
```

If double-braces have meaning already in any source context, then post a comment as close to the top of the file as possible and explain the replacement syntax by providing a description and example.

For any commandline (__bash__) arguments, use the more common angle-bracket (greater-than, less-than) symbols to wrap optional or user-replacement strings. Again, be sure to retain any other braces or quations that are necessary around the replacement. For readability, it's probably preferable to use all-capital-letter (uppercase) text to make the replacement more easily distinguishable:

```
git remote add github git@<SSH-CONFIG-NAME>:<GITHUB-ACCOUNT>/<REPOSITORY-NAME>.git
```

As shown above, whitespace within the replacement text should be avoided, since whitespace is a separator in the bash syntax and has significant meaning. Dashes or underscores are preferable, but using CamelCase is an equally reasonable alternative.

In all cases, note that you as the user are expected to replace not only the replacement text, but the wrapper characters for the replacement text. For example, let's say your password is `badIdea`, and you are presented with a replacement line like:

```python
my_username = "me";
my_password = "[[PASSWORD GOES HERE]]";
```

You should replace `[[PASSWORD GOES HERE]]` with `badIdea` as such:

```python
my_username = "me";
my_password = "badIdea";
```

Again, notice that the `[[` and `]]` characters were replaced along with the inner text. This should be the same process for `<...>` replacement as well -- _i.e._, do not leave the `<` and `>` characters behind after replacement.

