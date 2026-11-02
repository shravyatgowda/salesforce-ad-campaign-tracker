# Salesforce Ad Campaign Tracker

A small Salesforce Developer Edition project for ad operations: track ad campaigns and their creatives, block bad budget data, and automatically flip a campaign to **Active** on its launch date.

> **Status:** metadata is written but must be deployed and tested in your own org. Complete the checklist at the bottom, then update this line with what you verified.

## What it includes

| Component | Purpose |
|---|---|
| `Ad_Campaign__c` object | Campaign record with Budget, Spend, Impressions, Launch Date, Status |
| `Ad_Creative__c` object | Child of a campaign (master-detail) with Format, Spend, Impressions |
| Validation rule `Budget_Cannot_Be_Negative` | Stops a campaign from saving with a negative budget |
| Flow `Activate Ad Campaign On Launch Date` | Record-triggered flow with a scheduled path: sets Status to `Active` on the Launch Date for campaigns marked `Scheduled` |
| Permission set `Ad Campaign Tracker Access` | Gives access to both objects, all fields and tabs |

Status values: `Draft`, `Scheduled`, `Active`, `Completed`.

## Deploy with Salesforce CLI

1. Create a free [Developer Edition org](https://developer.salesforce.com/signup).
2. Install the [Salesforce CLI](https://developer.salesforce.com/tools/salesforcecli) and log in:
   ```bash
   sf org login web --alias adtracker
   ```
3. Deploy:
   ```bash
   sf project deploy start --source-dir force-app --target-org adtracker
   ```
4. Assign access to yourself:
   ```bash
   sf org assign permset --name Ad_Campaign_Tracker_Access --target-org adtracker
   ```
5. In **Setup > Flows**, open *Activate Ad Campaign On Launch Date* and click **Activate** (it deploys as Draft so you can review it first).

If a deploy error appears, fix it from the CLI message, or build the same components by hand in Setup using the table above.

## Load sample data (optional)

`data/sample_campaigns.csv` holds three made-up campaigns for testing. Import them with **Data Import Wizard** (Setup > Data Import Wizard > Custom objects > Ad Campaign).

## Test checklist

- [ ] Create a campaign with Budget `-100`: save is blocked with "Budget cannot be negative."
- [ ] Create a campaign with Budget `5000`: saves normally.
- [ ] Create a campaign with Status `Scheduled` and Launch Date set to today: the scheduled path runs and Status becomes `Active` (it can take a few minutes; check **Setup > Scheduled Jobs**).
- [ ] Add two Ad Creatives to a campaign and confirm they appear in the related list.

## Possible extensions

- Roll-up summary of creative impressions and spend onto the campaign
- A report and dashboard for spend vs budget by status
- A second flow that sets Status to `Completed` after an end date

## License

MIT. See [LICENSE](LICENSE).
