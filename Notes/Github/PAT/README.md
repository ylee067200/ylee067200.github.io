# Introduction

If you activate two-factor authentication, you can't commit with username / password.

![Two-Factor Authentication](https://user-images.githubusercontent.com/88823828/129824309-cc1c74d7-296c-487c-bc86-4b2e081a7ad7.png)

## How to createa a PAT

PAT (Personal Access Token) only accept by **git over https**, not for **git over ssh**. 

You need to create your PAT vis these steps:

1. Get into your account settings

2. Select "Developer settings"

![Account Settings](https://user-images.githubusercontent.com/88823828/129824334-c9153180-b8a7-42cb-9ebe-4434dffd0b04.png)

3. Select "Personal access token" to create PAT

![PAT](https://user-images.githubusercontent.com/88823828/129824393-2f35dd79-98d9-4d3d-8a1a-bad46761f5d1.png)

You can't get PAT data again; either copy and store it in a file, or use "Regenerate token" to recreate one.

![Regenerate Token](https://user-images.githubusercontent.com/88823828/129824515-99a85b12-c941-4085-bdf0-6124458879b4.png)

## Using PAT

Everytime you create a new token, you need to re-clone your repositories with this PAT. Here are command to clone git repository with PAT:

```
git clone https://${USERNAME}:${PAT}@${REPOSITORY}
```

${REPOSITORY} doesn't contained prefix "https://"; for example, if I want to clone this repository, I need to use this command:

```
git clone https://ylee067200:${PAT}@github.com/ylee067200/ylee067200.github.io.git
```

