---
description: >-
  This guide is intended as a way to help you discover and familiarize with the
  APIs, as opposed to integrating it into your project. For that check out the
  "Quick Start - Integrate" guide.
---

# Quick Start - API Explorer

The best way to get up and running quickly, and able to experiment with the APIs is to run a pre-packaged distributable version of the "full suite" of hREA functionality. How you will run it is similar to how other people in the future may run the application you develop. What you will be accessing is a Graphql Explorer: a system for viewing and running raw Graphql queries without writing any additional code.

Since Holochain is a runtime for local-first software, that is software whose core functions are actually executed 'in the client' and there is no central server, we need to first install that Holochain runtime in the easiest manner possible. Having the runtime will then allow us to install the hREA Graphql Explorer application.

{% hint style="info" %}
The following tutorial is meant for desktop operating systems, not mobile.
{% endhint %}

## Install the Holochain "Launcher"

The Holochain "Launcher" is available for download freely on Github.

[Go here](https://github.com/holochain/launcher/releases/tag/v0.9.0) to access the instructions, and the download, for your operating system. Make sure to note the special instructions for your operating system, as the software is still labeled as "Pre-release" and is not yet optimized for user experience.&#x20;

When you start the Holochain Launcher application it will ask that you set a password, which is used to encrypt your data for security. Make sure you record that password somewhere.

Great, you now are running the Launcher, re-open it anytime you want to continue with this Quick Start guide, or do live experimentation and familiarization with the Graphql API.

## Install hREA-graphql-explorer

[Go here](https://github.com/h-REA/hREA/releases/tag/happ-0.1.2-beta) to download the `hrea.webhapp` file from under the `Assets` heading.

Within the Holochain Launcher, click `Install New App`.

Click `Select App From Filesystem`.

Find the `hrea.webhapp` file on your filesystem, and select it.

In the next popup that appears, `Install App: hrea_suite`, you only need to modify one thing. In the field labeled **`Holochain Version`**, select **`0.1.3`** from the list. Next, click `Install`. Wait while it installs. Once it's done, it should take you back to the main page, and you should see 'hrea\_suite' and it should say 'Running', which is its status. Click `Open` to start using the Graphql Explorer application!

![](<.gitbook/assets/Screen Shot 2022-07-04 at 7.41.58 AM.png>)

{% hint style="info" %}
The Holochain Launcher runtime is capable of running the small pre-packaged bundles of application logic which are known as hApps (holochainApps). Even more specific than a "hApp" is a "webhapp", which is simply a bundle of web-language (HTML/CSS/Javascript) files and a hApp. The Launcher can also install and run these webhapps by serving the user interface files as well.
{% endhint %}

## Make your first requests

What you should now have in front of you is a ["Graphiql" interface](https://github.com/graphql/graphiql/tree/main/packages/graphiql#readme). There are multiple panels. The main left panel is for writing your graphql queries, which are how you make requests to the hREA APIs. The right panel is where you will see the system responses to your requests. There are additional hidden trays which contain useful features and information.

There are some pre-filled queries already in the left panel. Via the big `Play` button in the upper left, you are able to execute any of the queries in the query panel individually.

Let's try the first two, which will first create a profile, and second associate it with yourself. This calls the top-level Graphql "mutation" (data-altering) method `createPerson`. Replace the text `place your name here` with your name.

```graphql
mutation CreatePerson {
  createPerson(person: { name: "Connor" }) {
    agent {
      id
      name
    }
  }
}
```

Next, click the `Play` button, and then click the query named `CreatePerson`, which is just an arbitrary label.

![](<.gitbook/assets/Screen Shot 2022-07-04 at 8.08.08 AM.png>)

In the right panel, you should see something like this

```json
{
  "data": {
    "createPerson": {
      "agent": {
        "id": "uhCEkq8yPJtCDlpM6ZDs__b7lRTDPlMPOy0kZCmp9bcbDxNgmpiIU:uhC0k503kLoDxJNulbKWRjK1J2zxU9PyCZFrAFwmdZZUNrOx4mry2",
        "name": "Connor"
      }
    }
  }
}
```

In Graphql, the shape of the data in the response always matches the shape of the request. There are many other fields that we did not provide or request in our query.

Copy the value of the `data.createPerson.agent.id` property to your clipboard, as it will be needed for the next queries!

Note that having created the profile is not enough to associate with the local authenticated acting user. We have to call one more mutation method. From your clipboard, replace the text `place agent.id here` here.

```graphql
mutation AssociateMyAgent {
  associateMyAgent(agentId: "uhCEkq8yPJtCDlpM6ZDs__b7lRTDPlMPOy0kZCmp9bcbDxNgmpiIU:uhC0k503kLoDxJNulbKWRjK1J2zxU9PyCZFrAFwmdZZUNrOx4mry2")
}
```

{% hint style="info" %}
To understand these functions in more depth, check out the section on [Usign "myAgent"](using-myagent.md).&#x20;
{% endhint %}

## Continue with other queries and exploration

Now that you've made your first requests, and associated a personal profile, you can easily continue with `step 3` from within the graphql explorer, by following the instructions there.

You will be able to access `myAgent` which will be a very useful query for developing applications.

Here are a few other useful tips.

{% hint style="info" %}
Check out [Thinking & Expressing ValueFlows](thinking-and-expressing-valueflows.md) to start learning the vocabulary and creating Economic Events.
{% endhint %}

{% hint style="info" %}
Check out the [GraphQL API Reference](reference/graphql-api-reference/) welcome page in order to view a couple of important details about types of values expected by the API.
{% endhint %}

{% hint style="info" %}
Hover with your mouse over a label in order to see any documentation that may be available about that query.&#x20;

![](<.gitbook/assets/Screen Shot 2022-07-04 at 8.27.12 AM.png>)
{% endhint %}

{% hint style="info" %}
Click on a type like `PersonResponse` to view any other documentation about it, in the expanded 'Docs' panel.

![](<.gitbook/assets/Screen Shot 2022-07-04 at 8.33.52 AM.png>)![](<.gitbook/assets/Screen Shot 2022-07-04 at 8.34.02 AM (1).png>)
{% endhint %}

{% hint style="info" %}
Open the 'Explorer' to easily modify your query inputs and response values

![](<.gitbook/assets/Screen Shot 2022-07-04 at 8.36.26 AM.png>)
{% endhint %}

