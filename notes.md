# Notes

![image](https://user-images.githubusercontent.com/9121359/132625710-87c7213e-1846-4d3c-9751-608038252f5b.png)

![image](https://user-images.githubusercontent.com/9121359/132625678-fac85603-f3e6-4e04-97cc-508bc3718a1b.png)

## What you built and what you didn't build

I've focused on building a status page that a CLI developer would feel like they are not missing anything from their beloved CLI. Each param and feature would be translated on the simple dashboard. 

Not only that but I was able to find some edge cases on the Go CLI formatting that were pleasant to implement such as [up arrows showing when an upgrade is happening on some instances](https://github.com/superfly/flyctl/blob/21499c79b62dbd5ef454fd1e24217992affc16c4/cmd/presenters/allocations.go#L31) (image below) or [when to show the deploy on UI](https://github.com/superfly/flyctl/blob/15d32f48b245c04397bd4d116fb449f27b4e051f/cmd/status.go#L126)

![image](https://user-images.githubusercontent.com/9121359/132625268-4656b3a8-ba6a-48d7-b946-66bbded08207.png)

![image](https://user-images.githubusercontent.com/9121359/132625281-2ddb8825-a316-4f61-bccf-a18cc6544ae6.png)

Worth mentioning a simple process loop is what it took to make the UI reflect changes every N seconds. Overall, the task is done.

## What you'd improve or fix if you had more time

First of all, there are a few minor improvement points such as

- Create a common template for those SVGs of success and failure so the code can be easily reused. Perhaps create view helpers to translate booleans into those icons.
- Use the region API to show prettier region names like the CLI does.
- Overall try to make some labels more human-friendly such as "success" to "✅ Success" or other ways to convey the feeling behind the data.

Other than that an improvement I'd love to explore would be using PubSub to handle the real-time aspect of the app. Each live view would subscribe to the topic for that one app and at the possibility of multiple users peeking into the same app, we would broadcast the change to all in a unified way so we could spare some of our GraphQL servers resources although the current solution that feels like long polling works just fine.

## How you'd determine if this feature is successful

As a heavy CLI user myself I feel like this page would need to give a user experience worth getting out of my way from handling everything from the CLI to going to the UI to watch the progress. It's no mystery the CLI (currently) is not real-time updating our status so re-running the status now and then could be a reason to choose to go for the web UI instead but I think we developers should also convince those users to stay.

Not only that the UI should be designed with all users in mind so perhaps let us add some niceties to handle the deployment process and that would greatly improve the lifespan of this page on a developer's toolkit, especially those who fancy using a pretty UI for such tasks.