---
slug: dotnet
title: How  to set up secrets using dotnet
authors: [luisjasso]
tags: [dotnet, mac, c#]
---

To set up credential on Mac or Windows, you can do it with dotnet

Below the steps;

**1 - Create a new file whereever on your pc**

```
~/settingApp.json
```

**2 - Use this command**

```
cat ~/settingApp.json | dotnet user-secrets set
```

Successfully saved 10 secrets to the secret store.

**3 - Whereever you run the secrets will be set, so run the below command to see the parameters set**

```
dotnet user-secrets list
```
