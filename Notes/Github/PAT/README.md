# Introduction

If you activate two-factor authentication, you can't commit with username / password.

## How to createa a PAT

PAT (Personal Access Token) only accept by **git over https**, not for **git over ssh**. 

You need to create your PAT vis these steps:

1. Get into your account settings

2. Select "Developer settings"

3. Select "Personal access token" to create PAT

You can't get PAT data again; either copy and store it in a file, or use "Regenerate token" to recreate one.

## Using PAT

Everytime you create a new token, you need to re-clone your repositories with this PAT. Here are command to clone git repository with PAT:

```
git clone https://${USERNAME}:${PAT}@${REPOSITORY}
```

${REPOSITORY} doesn't contained prefix "https://"; for example, if I want to clone this repository, I need to use this command:

```
git clone https://ylee067200:${PAT}@github.com/ylee067200/ylee067200.github.io.git
```

