+++
title = 'Git Submodules'
date = 2024-12-19T19:13:57+05:30
draft = false
description = "Information on Git Submodules"
+++

# Submodule with only specific path from the submodule

```sh
git submodule add "Git URL" <path to submodule desired output>
cd .git/modules/<Path choosen above>
#Double check the URL of the submodule:
git config --get remote.origin.url
echo "docs/devel" >> .git/info/sparse-checkout
cd <Path to your repo>
#delete the submodule folder
git submodule update
git submodule sync
```

# References

1. [Add specific folder with submodule to a repository : git](https://www.reddit.com/r/git/comments/sme7k4/add_specific_folder_with_submodule_to_a_repository/)
