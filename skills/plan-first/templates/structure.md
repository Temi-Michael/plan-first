<!-- safe-build:plan:start -->
# Structure

> **In plain words:** {{what the app is built with, and how the parts fit together}}
<!-- Keep the summary above for beginner and intermediate users. Delete it for developers. -->

## Stack
| Part | Choice | Why | Rejected options |
|---|---|---|---|
| {{frontend / backend / database / auth / payments / hosting}} | {{choice}} | {{reason}} | {{option: reason}} |

**Sources:** {{official pages checked, each with the date checked, or "not checked against current sources"}}

## External services
| Service | Used for | Expected cost |
|---|---|---|
| {{service}} | {{purpose}} | {{cost at expected scale}} |

## Data model
| Data | Fields | Sensitivity | Who can see | Who can edit |
|---|---|---|---|---|
| {{entity}} | {{fields}} | {{public / personal / sensitive}} | {{roles}} | {{roles}} |

## Access rules
<!-- These rules are what /safe-build:secure-check verifies. Write each one so it can be tested. -->
- {{e.g. Customers only see their own bookings.}}

## Folders
```
{{planned folder layout}}
```

## Architecture
{{How the parts connect: a short description or a simple diagram}}

## Change log
- {{date}}: Plan created.
<!-- safe-build:plan:end -->
