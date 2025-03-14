# VOID Dataset

## Inclusion Criteria

Incident reports are included with the following inclusion criteria:

1. Authored by the organization that owns the system that failed (not a third party),
2. Reports on a software system failure (rather than a security incident, say),
3. Includes sufficient detail about action items for our analysis (see below), and
4. Reports on an incident no earlier than 2015.

We will take `data/void_incidents.csv` and generate `./data/void_incidents_fitting_inclusion_criteria.csv` by

1. Filter "Format (primary source)" to "Company post".
2. Filter "Impact category" to remove anything that includes the word Security. This will require additional manual filtering.
3. Remove "Primary Source" that are blank. This will require additional manual filtering.
4. Filter "Date of Incident Column" to only have incidents from January 1st 2010 to April 1st 2023 (different from Data of writeup column)
5. Randomly sort and assigned an increasing IR identifier from 1 to 173

## Manual Exclusion Steps

In some cases, an incident will be detected to not fit our inclusion criteria. This may be because the incident was categorized in VOID incorrectly, or perhaps it does not actually include any action items. In these cases, the procedure will be the following.

1. Mark the report as `#exclude: REASON`
2. Add `[TODO] Needs review for replacement` at the top.

After an independent reviewer agrees that the IR should be excluded, then we will assign the last IR to the id of the IR that is to be replaced. In other words, IR-170 can become IR-12 if IR-12 is to be excluded. We argue this has no methodological consequences because IR ids were randomly assigned and the re-assignment process is not biased in a way that could affect results if we do not complete all the IRs that satisfy our inclusion criteria.

Here are the entries that were selected from VOID, but are not actually incident reports (and therefore were excluded)

**1.yaml | Chef** https://web.archive.org/web/20190923192224/https://blog.chef.io/2019/09/19/chefs-position-on-customer-engagement-in-the-public-and-private-sectors/

- _Decision:_ Not an IR (email from CEO to employees) and not an incident as it was caused deliberately by a disgruntled employee
- Decision:\_ 173 CCP Games (Eve Online) is from pre-2010 and was miscategorized within Void
- _Replaced by:_ 162 Coinbase

**11.yaml | Spotify** # https://community.spotify.com/t5/Ongoing-Issues/Downtime-November-16th-Spotify-website-and-app-down/idi-p/5296183

- _Decision:_ Not an IR (just a status update)
- _Replaced by:_ 172 Cloudflare

**17.yaml | Second Life** https://community.secondlife.com/blogs/entry/2438-unscheduled-ddos-on-10-28-2018/

- _Decision:_ Not an IR (just a message to the community about a DDoS)
- _Replaced by:_ 171 AWS

**22.yaml | Salesforce** https://help.salesforce.com/articleView?id=000358392&type=1&mode=1

- _Decision:_ Links to actions are all broken, and no other details provided
- _Replaced by:_ 170 Cloudflare

**23.yaml | Rogers** https://about.rogers.com/news-ideas/a-message-from-jorge-fernandes-chief-technology-officer-at-rogers/

- _Decision:_ A message from CEO (about an incident) but this is not an IR
- _Decision:_ 169 is a DDOS so we excluded it also https://ns1.com/blog/how-we-responded-to-last-weeks-major-multi-faceted-ddos-attacks
- _Replaced by:_ 168 AWS

**30.yaml | 34sp** https://www.34sp.com/hosting-news/blog/network-outage-june-9th/

- _Decision:_ Not an IR (a report about a DDoS)
- _Replaced by:_ 167 WazirX

**34 | Second Life** https://community.secondlife.com/blogs/entry/2446-grey-avatars-and-clouds/

- _Decision:_ Not an IR (a message from CEO)
- _Replaced by:_ 164 Cloudflare

**40 | Second Life** https://community.secondlife.com/t5/Tools-and-Technology/A-Play-by-Play-Retelling-of-Yesterday-s-Downtime/ba-p/3060170

- _Decision:_ Not an IR (a message from CEO)
- _Replaced by:_ 163 Venafi

**49.yaml | Facebook** https://web.archive.org/web/20150920083346/https://developers.facebook.com/status/issues/393998364112264/

- _Decision:_ Not an IR (a status update)
- _Replaced by:_ 166 Manta

**51.yaml | Instapaper** http://blog.instapaper.com/post/157027537441

- _Decision:_ Not an IR (a status update)
- _Replaced by:_ 165 Cloudflare

**62.yaml | Reddit** https://www.reddit.com/r/RedditEng/comments/o4yjpd/rwallstreetbets_incident_anthology_what_worked/

- _Decision:_ Not an IR (a near miss engineering exposition)
- _Replaced by:_ 161 Buildkite

**63.yaml | Cloudflare** https://blog.cloudflare.com/how-verizon-and-a-bgp-optimizer-knocked-large-parts-of-the-internet-offline-today/

- _Decision:_ Not an IR (report on another company failure that affected them, does not read as if their own IR)
- _Replaced by:_ 159 GitLab

**64.yaml | Secondlife** https://community.secondlife.com/t5/Tools-and-Technology/Someone-had-a-case-of-the-Mondays/ba-p/3094252

- _Decision:_ No IR conducted or reported on
- _Replaced by:_ 158 Travis CI

**65.yaml | AWS** https://aws.amazon.com/message/4372T8/

- _Decision:_ Duplicate IR
- _Replaced by:_ 154 Travis CI

**69.yaml | Secondlife** https://community.secondlife.com/blogs/entry/2167-re-experience-the-fun-of-customizing-your-place-page-a-tale-of-oops-from-ops/

- _Decision:_ Not an IR (a message about an incident)
- _Replaced by:_ 157 Wikimedia Foundation

**73.yaml | Western Digital** https://www.westerndigital.com/support/productsecurity/wdc-21008-recommended-security-measures-wd-mybooklive-wd-mybookliveduo

- _Decision:_ A security incident
- _Replaced by:_ 156 Heroku

**75.yaml | Xero** https://www.xero.com/blog/2018/09/sorry-really-sorry/

- _Decision:_ Not an incident report (just an apology)
- _Replaced by:_ 155 Chef

**3.yaml | Mailchimp** https://mailchimp.com/what-we-learned-from-the-recent-mandrill-outage/

- _Decision:_ No AIs
- _Replaced by:_ 151 DataDog

**28.yaml | Netflix** http://techblog.netflix.com/2012/10/post-mortem-of-october-222012-aws.html

- _Decision:_ No AIs
- _Replaced by:_ 150 Twilio

**32.yaml | Cloudflare** https://blog.cloudflare.com/today-we-mitigated-1-1-1-1/

- _Decision:_ No AIs
- _Decision:_ 149 GitHub is a duplicate of IR-14, so skipping
- _Decision:_ 148 DataDog is a duplicate of IR-3, so skipping
- _Replaced by:_ 147 Yeller

**35.yaml | Allegro** https://allegro.tech/2015/01/allegro-cast-post-mortem.html

- _Decision:_ No AIs
- _Decision:_ 146 Akami is not an IR, so skipping
- _Decision:_ 145 loveholidays unclear if there are AIs or just "solutions", so skipping
- _Decision:_ 144 Akami is not an IR, so skipping
- _Decision:_ 143 Slack has no AIs, so skipping (only a third party one)
- _Replaced by:_ 142 GitHub

**41.yaml | Gov.uk** https://dev.to/xenatisch/cascade-of-doom-jit-and-how-a-postgres-update-led-to-70-failure-on-a-critical-national-service-3f2a

- _Decision:_ No AIs
- _Decision:_ 141 Travis is duplicate of IR-60, so skipping
- _Decision:_ 140 PrometheusKube unclear if there are AIs or just potential "solutions", so skipping
- _Replaced by:_ 139 Microsoft

**45.yaml | Honeycomb** https://www.honeycomb.io/blog/incident-review-shepherd-cache-delays

- _Decision:_ No AIs
- _Replaced by:_ 138 Gandi

**52.yaml | Skyscanner** https://medium.com/@SkyscannerEng/how-a-couple-of-characters-brought-down-our-site-356ccaf1fbc3

- _Decision:_ No AIs
- _Decision:_ 137 Tarsnap No AIs (only LLs), so skipping
- _Replaced by:_ 136 Algolia

**68.yaml | BBC** https://www.bbc.co.uk/blogs/internet/entries/a37b0470-47d4-3991-82bb-a7d5b8803771

- _Decision:_ No AIs
- _Replaced by:_ 135 Sentry

**72.yaml | BBC** https://www.bbc.co.uk/blogs/internet/entries/a37b0470-47d4-3991-82bb-a7d5b8803771

- _Decision:_ No AIs
- _Replaced by:_ 134 Reddit
