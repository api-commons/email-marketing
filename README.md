# Email Marketing

The common email-marketing vocabulary -- the lists and segments an audience is organised into, the subscribers on them, the campaigns sent to them, the automations that send on a trigger and the reports that measure the result -- distilled from the APIs that already exist. Templates belong to the messaging context. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Email Marketing, Marketing Automation, Newsletter, Newsletters, SMS Marketing in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| list | 44 | 39 | name 85%, id 77%, created_at 67%, updated_at 51% | lists 22, list 22, audiences 9, contact_lists 1 |
| subscriber | 29 | 27 | email 78%, id 78%, metadata 70%, created_at 63%, first_name 63%, last_name 63% | contacts 23, contact 8, members 5, profiles 3 |
| segment | 15 | 14 | id 86%, name 71%, created_at 50% | segments 14, segment 3 |
| campaign | 27 | 25 | id 92%, status 72%, created_at 68%, name 64% | campaigns 24, campaign 6, broadcasts 1, broadcast 1 |
| automation | 14 | 12 | id 67%, status 58%, created_at 50%, name 50% | workflows 4, flows 3, journeys 2, automations 2 |
| campaign_report | 11 | 9 |  | stats 6, metrics 3, summary 3, reports 1 |

Cohort: 102 providers with harvested OpenAPI, 51 crosswalks. Of the providers exposing a list: 64% create, 96% list, 61% fetch, 46% update, 46% delete. Generated 2026-11-10 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A subscriber agrees on email, first and last name, custom fields and when they joined -- the merge-field model every email platform inherited.
- A campaign agrees only on id, name, status and created_at: subject, sender and send time are each modelled too differently to share, because a campaign is a draft, a schedule and a send at once.
- Campaign reports agree on nothing. Opens, clicks, bounces and unsubscribes are counted by every platform, each with its own field names and unique-versus-total semantics.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- A list covers audiences, mailing lists and contact lists; a subscriber covers contacts, profiles and list members -- but only at a provider that also exposes lists.
- A campaign covers broadcasts and mailings; a publication-level newsletter (Ghost, Buttondown) is not a send and is excluded.
- An automation covers workflows, flows, journeys, sequences and autoresponders.
- Templates are the messaging context's and are not duplicated here.
- Duplicates merged: Infusionsoft into Keap.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
