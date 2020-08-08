**Days.csv**

Location: root/data

Defines 

###Usage

| DAY       | 1                                                                                                                                                                                                                              | 2                        | 3                                             | 4                                                       | 5            | 6                                      | 7                               | 8                     | 9     | 10            | 100      |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------------------------------------------|---------------------------------------------------------|--------------|----------------------------------------|---------------------------------|-----------------------|-------|---------------|----------|
| DESC      | Arstotzkans   only      No inspection      No errors                                                                                                                                                                           | Inspection   intro       | EntryTicket   intro      Missing papers intro | EntryPermit/IdCard   intro      Fingerprint intro       | Detain intro | WorkPermit   intro      Suicide bomber | Search   intro      Bribe intro | Forgery   intro       |       | Sniping intro | Test day |
| RULES     | RuleNeedPassport      RuleArstotzkaOnly                                                                                                                                                                                        | *                        | *                                             | *                                                       | *            | *                                      | *                               | *                     | *     | *             | *        |
| COUNT     | 5                                                                                                                                                                                                                              | 7                        | 8                                             | 9                                                       | 9            | 100                                    | 9                               | 9                     | 8     | 8             | 8        |
| TRAVELERS | FINALLY_RETURN_HOME      SMALL_CHECKPOINT      WAITED_FOREVER      FIRST_DAY      KOLECHIAN_HATER      FIRST_DAY                                                                                                               | *                        | *                                             | *                                                       | *            | *                                      | *                               | *                     | *     | *             | *        |
| FEATURES  | FREEDENIAL                                                                                                                                                                                                                     | *                        | *                                             | *                                                       | *            | *                                      | *                               | *                     | *     | *             | *        |
| NEWS      | T   Grestin Border Checkpoint Opens At Last!      S After 6 Long Years. Can the Ministry of Admission Keep Us Safe?      --      T Families To Reunite      --      S The Weather                                              | *                        | *                                             | *                                                       | *            | *                                      | *                               | *                     | *     | *             | *        |
| BULLETIN  | Welcome   to your new position at Grestin Border Checkpoint.            Stamp passport ENTRY VISA and return documents to entrant.            Entry is restricted to Arstotzkan citizens only.            Deny all foreigners. | *                        | *                                             | *                                                       | *            | *                                      | *                               | *                     | *     | *             | *        |
| BPAGES   | passporttut boothtut                                                                                                                                                                                                           | correlatetut boothtut    | missingtut boothtut                           | boothtut                                                | boothtut     |                                        | ruletut                         |                       |       |               |          |
| DURATION  | 2                                                                                                                                                                                                                              | 4                        | 6                                             | 7                                                       | 7            | 7                                      | 7                               | 7                     | 5     | 5             | 500      |
| RUNNER    |                                                                                                                                                                                                                                | YES                      |                                               |                                                         |              |                                        |                                 |                       |       |               |          |
| LAMP      | 1                                                                                                                                                                                                                              | 1                        | 1                                             | 1                                                       | 1            | 1                                      | 1                               | 1                     | 1     | 1             | 1        |
| GUARD     | 3                                                                                                                                                                                                                              | 3                        | 12340                                         | 12340                                                   | 12340        | 12340                                  | 12340                           | 12340                 | 12340 | 12340         | 12340    |
| PAPERS    |                                                                                                                                                                                                                                |                          |                                               |                                                         |              |                                        |                                 |                       |       |               |          |

*For brevity, only the first day's values are shown for these rows.

* DAY: The number of the day, used for determining what modifiers should apply to what day.
* DESC: A description of the day, used for documentation purposes.
* RULES: What rules, referenced in Facts.xml, are in place on the day.
* COUNT: 
* TRAVELERS: What travellers, found in Travelers.txt, appear on this day.
* FEATURES: What features are in place on the day.
  * FREEDENIAL: Allows denials of entrants without interrogating first.
  * INPSECT: Allows inspection of documents.
  * FINGERPRINT: Allows fingerprinting as an interrogation possibility.
  * DETAIN: Allows detention of suspicious entrants.
  * SEARCH: Allows searching as an interrogation possibility.
  * SNIPING: (Unused, untestested in functionality) Allows weapons to be used for stopping terrorist attacks.
* NEWS: *T Title S Sub-heading* The headlines that appear in the newspaper at the start of the day.
* BULLETIN: The text displayed in the bulletin.
* BPAGES: The pageid of the Bulletin tutorials, found in Papers.xml, to be displayed after the first page.
* DURATION:
* RUNNER: Whether there will be a 'runner' (climber) terrorist attack that day.
* LAMP:
* GUARD: What guards will appear on that day, by their position.
* PAPERS: (Unused)
