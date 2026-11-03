# Test results

Fill this in after deploying to your Developer Edition org. Add a screenshot for each check to `docs/screenshots/` and link it here.

| # | Test | Expected | Result | Screenshot |
|---|---|---|---|---|
| 1 | Create a campaign with Budget `-100` | Save blocked: "Budget cannot be negative." | TODO | `screenshots/01-negative-budget-blocked.png` |
| 2 | Create a campaign with Budget `5000` | Saves normally | TODO | `screenshots/02-valid-budget-saved.png` |
| 3 | Campaign with Status `Scheduled` and Launch Date today | Status becomes `Active` after the scheduled path runs | TODO | `screenshots/03-flow-activated-status.png` |
| 4 | Add two Ad Creatives to a campaign | Both appear in the related list | TODO | `screenshots/04-creatives-related-list.png` |
| 5 | Flow run history | Shows a successful run | TODO | `screenshots/05-flow-run-history.png` |

Tested on: `TODO` (date), Salesforce Developer Edition, API version 60.0
