# Give customer requests in Slack Connect a clear owner

Actionable customer messages in Slack Connect become owned HubSpot tickets, so the team has a clear person responsible for the next step.

Shared Slack channels make customer conversations fast, but a request can vanish inside a thread when each teammate assumes someone else is replying. Copying every message into a ticket system by hand adds more work and leaves gaps.

This example watches one approved customer channel and only messages from the customer user IDs you choose. Automate.ax AI identifies top-level messages that need a person to act, creates a HubSpot ticket with an owner and a link to the original message, and alerts an internal Slack channel. A human still decides how to answer the customer.

## Set it up with a coding agent

Copy the setup prompt from [the article](https://automate.ax/articles/slack-customer-request-ownership) into your coding agent. The agent creates the Automate.ax project, asks for your choices, guides account authorization, checks the automation, and deploys it. You do not need to clone this repository yourself when using the prompt.

You'll choose:

- The one Slack Connect channel and customer participant IDs to watch. The agent can help identify the IDs after you authorize Slack.
- The HubSpot ticket owner, ticket pipeline and starting stage, and an internal Slack channel for new request alerts.
- Account authorization for Slack and HubSpot. Slack requires a paid workspace for the current Automate.ax connection, and its app needs access to both channels.

Automate.ax AI reads messages from the selected customer participants to classify action requests. Confirm that this use of the shared channel matches your customer agreements and internal policy.

## Manual setup

If you prefer to set it up yourself:

```sh
git clone https://github.com/SentsCo/automate-ax-slack-customer-request-ownership.git
cd automate-ax-slack-customer-request-ownership
bun install
bunx automate.ax login
bunx automate.ax init
bun run typecheck
bunx automate.ax deploy
```

Connect the accounts requested by Automate.ax when you deploy. The platform stores credentials outside this repository. Set any project parameters requested by the automation, then review the read and write operations before turning it on.

## Check a run

Post one made-up customer request and one casual message in a test channel. Confirm the request creates one owned HubSpot ticket with a working source link, while the casual message creates none.

## Limits

- This watches top-level messages. Requests added only as thread replies need the separate Slack reply trigger.
- AI can misclassify a message. Review the first tickets and keep the internal alert visible to the owner.
- The example uses one fixed HubSpot owner. Add a reviewed customer-to-owner map before watching several customers.
- Separate actionable top-level messages create separate tickets, even when they concern the same problem. Review duplicates or add a thread-to-ticket map for a busy channel.

The workflow responds to [a real problem described by a customer success team's Slack Connect ownership gap](https://www.reddit.com/r/CustomerSuccess/comments/1s4gvs7). The public report informed the example; it is not an endorsement of this implementation.
