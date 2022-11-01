## Ohio Voter Registration Tables

This page contains tables describing the voter registration system of Ohio. A full explanation of the table properties can be found in our paper, [A Systematization of Voter Registration Security]().

Jump to:

- [Jurisdictional Parameters](#jurisdictional-parameters)
- [Access Control Policy](#access-control-policy)
- [System Change Control Policy](#system-change-control-policy)
- [Data Change Control Policy](#data-change-control-policy)
- [Voter Data Use Policy](#voter-data-use-policy)
- [Voter Notification Policy](#voter-notification-policy)
- [Maintenance Policy](#maintenance-policy)
- [Oversight Policy](#oversight-policy)

### Jurisdictional Parameters

| Parameter                                                    | Value                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| $p_{\rm elig}$: the voter eligibility criteria               | You are qualified to register to vote in Ohio if you meet all the following requirements:<br />• You are a citizen of the United States;<br />• You will be at least 18 years old on or before the day of the next general election. (If you will be 18 on or before the general election, you may vote in the primary election to nominate candidates, but you cannot vote on issues or party central committees until you are 18);<br />• You will be a resident of Ohio for at least 30 days immediately before the election in which you want to vote;<br />• You are not incarcerated (in prison or jail) for a felony conviction under the laws of this state, another state, or the United States;<br />• You have not been declared incompetent for voting purposes by a probate court; and<br />• You have not been permanently disenfranchised for violating the election laws. |
| $p_{\rm reg-acts}$: Required actions from the voter in order to register | Submit voter registration application                        |
| $p_{\rm reg-methods}$: List of registration methods          | Online, mail, in person                                      |
| $p_{\rm voter-info}$: Types of voter information that are collected and stored | See Access Control Policy Table                              |
| $p_{\rm freeze-reg}$: Period before election during which new registrations are not allowed | 30 days before election                                      |
| $p_{\rm freeze-db}$: Period before election during which systemic registration removals or other maintenance are not allowed | 90 days                                                      |
| $p_{\rm keep-logs}$: Period after an election for which a snapshot and activity logs of the VRDB for that election are kept | Registration cards retained permanently, pollbooks retained for at least 2 years |
| $p_{\rm elig}$: Voter authentication criteria: How voters are authenticated for various stages of the VRDB process (registering to vote, updating voter registration record, checking in at a pollbook) | Updating record: DoB, driver's license number or SSN last 4, signature<br/>Looking up record online: First name, last name, county<br /> Checking in at pollbook: 1 form of ID<br /> Absentee ballot: signature<br /> First time absentee request: photocopy of ID |

Sources:

<https://www.ohiosos.gov/elections/voters/register/#deadline>

https://www.ohiosos.gov/globalassets/elections/directives/2019/dir2019-11_eom.pdf

https://codes.ohio.gov/ohio-revised-code/section-3503.15

https://www.ohiosos.gov/globalassets/elections/eoresources/general/retentionschedule.pdf

### Access Control Policy

The access control policy determines which entities can access certain fields. We represent the access control policy as a table that maps entities to registration fields, with binary values in each cell denoting whether the entity in that row is allowed to view the data point in that column, for any voter.

\*: hidden for address confidentiality program and confidential voters

†: only accessible by designated address confidentiality program election staff

‡: hashed before sending to ERIC

| Category         | Entity                                      | Name | Home address | Mailing address | Full Date of birth | Tel num | Email address | Driver's license / ID card number | SSN last 4 digits | Political Party affiliation | Date of affiliation | Signature | Voting activity history |
| ---------------- | ------------------------------------------- | ---- | ------------ | --------------- | ------------------ | ------- | ------------- | --------------------------------- | ----------------- | --------------------------- | ------------------- | --------- | ----------------------- |
| REGISTER/UPDATE  | Voter being registered                      | ✓    | ✓            | ✓               | ✓                  | ✓       | ✓             | ✓                                 | ✓                 | ✓                           | ✓                   | ✓         | ✓                       |
|                  | VRDB                                        | ✓    | ✓            | ✓               | ✓                  | ✓       | ✓             | ✓                                 | ✓                 | ✓                           | ✓                   | ✓         | ✓                       |
|                  | Online registration/update portal           | ✓    | ✓\*          | ✓\*             | ✓                  | ✓\*     | ✓             | ✓                                 | ✓                 | ✓                           | ✓                   | ✓         | ✓                       |
|                  | BMV (when registering)                      | ✓    | ✓            | ✓               | ✓                  | ✓       | ✓             | ✓                                 | ✓                 | ✓                           | ✓                   | ✓         | ✓                       |
|                  | County Board of Elections (BOE) Director    | ✓    | ✓\*          | ✓\*             | ✓                  | ✓\*     | ✓             | ✓                                 | ✓                 | ✓                           | ✓                   | ✓         | ✓                       |
| USE REG TO VOTE  | County official at polling place            | ✓    | ✓†           | ✓†              | ✓                  | ✓†      | X             | ✓                                 | ✓                 | ✓                           | ✓                   | ✓         | X                       |
|                  | County official processing absentee ballots | ✓    | ✓†           | ✓†              | ✓                  | ✓†      | X             | ✓                                 | ✓                 | ✓                           | ✓                   | ✓         | X                       |
| LIST MAINTENANCE | NCOA                                        | X    | X            | X               | X                  | X       | X             | X                                 | X                 | X                           | X                   | X         | X                       |
|                  | ERIC                                        | ✓    | ✓            | ✓               | ✓‡                 | ✓       | ✓             | ✓‡                                | ✓‡                | X                           | X                   | X         | ✓                       |
| TRANSPARENCY     | The public                                  | ✓    | ✓\*          | ✓\*             | ✓                  | X       | X             | X                                 | X                 | ✓                           | ✓                   | X         | ✓                       |

Sources:

https://www.ncsl.org/research/elections-and-campaigns/access-to-and-use-of-voter-registration-lists.aspx

https://codes.ohio.gov/ohio-revised-code/section-3503.15

https://www.bmv.ohio.gov/dl-other-living-will.aspx
https://codes.ohio.gov/ohio-revised-code/section-3503.21

https://codes.ohio.gov/ohio-revised-code/section-111.42

https://nnedv.org/?mdocs-file=2925

### System Change Control Policy

Ohio does not publish information related to the system change control policy. See [here](template.md#system-change-control-policy) for a template table.

### Data Change Control Policy

The data change control policy includes information about the entities involved in updating the VRDB or associated policies. We represent the data change
control policy as a table that specifies the entities allowed to authorize/start updates, trigger updates (send updated data to election officials), and execute the update (directly modify the data inside
the VRDB). In this table, we map these entities to the type of data they update, and if there is a notification involved in this type of update.

| Category      | Entity                              | Type of Data                            |
| ------------- | ----------------------------------- | --------------------------------------- |
| Authorization | Voter                               | Personal data                           |
|               | State and county election officials | Data from list maintenance update       |
| Trigger       | Online update portal                | Data from voter who started update      |
|               | Mail                                | Data from voter who started update      |
|               | ERIC                                | Data of voters in other states          |
|               | Bureau of Motor Vehicles            | Data of new/updated license             |
|               | NCOA                                | Data of voter move                      |
|               | Ohio Department of Health           | Data of death                           |
|               | State probate judges                | Individuals adjudicated incompetent     |
|               | Clerks of courts of common          | Voters who have been convicted of crime |
| Execution     | State election officials            |                                         |
|               | County election officials           |

### Voter Data Use Policy

The voter data use policy specifies limitations on how (and by whom) the data can be used.

| Category             | Value                                              |
| -------------------- | -------------------------------------------------- |
| Prohibited uses      | Commercial purposes                                |
| Approved entities    | Public                                             |
| Information released | See access control policy table                    |
| Opt out policy       | Address Confidentiality Program (ACP) participants |

Sources:

https://www.ncsl.org/research/elections-and-campaigns/access-to-and-use-of-voter-registration-lists.aspx

### Voter Notification Policy

The voter notification policy governs how jurisidictions notify voters of various changes to their records. We represent the voter notification policies as a table mapping notification reasons to notification protocols and methods.
| Notification reason                   | Notification protocol                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Notification methods |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------- |
| Incomplete or ineligable registration | Send notice via notification methods                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Mail                 |
| New registration                      | Send acknowledgement notice via notification methods by non-forwardable mail. If returned as undeliverable, mark voter as "Inactive".                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Mail                 |
| Inactive registration                 | Send confirmation notice via notification methods to voters who have not voted or filled out a registration form in the past two years. Mark voters who do not respond or whose notice is returned as undeliverable as inactive. Cancel voter's registration four years after the notice was mailed if voter continues to be inactive.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Mail                 |
| Address change                        | Send 10-S-2 confirmation notice by forwardable mail. If the elector provides a new address within the same county, update the address. If the elector provides a new address in another Ohio county by mail, the county board of elections mails the record to the new county board of elections. If the elector provides a new address via the online voter registration system in a new county, the board of elections in the new county must accept the elector into their voter registration system. If the elector returns the confirmation notice with a new state, cancel the elector's registration. If the elector does not return the confirmation notice, and the NCOA change is out of county, mark the voter as "active-confirmation". If the USPS returns that the mail is undeliverable, issue form 10-S-1 confirmation notice to voter by forwardable mail. If USPS does not have a forwarding address, record that in the comments of the elector's record and keep the undeliverable confirmation notice for four years. | Mail                 |
| Cancelled registration                | Send notice via notification methods to address of deceased elector. If a response is received that the registration was canceled in error, restore the record.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Mail                 |

Sources:

https://www.ohiosos.gov/globalassets/elections/directives/2021/dir2021-03-ch03.pdf

https://www.ohiosecretaryofstate.gov/globalassets/elections/directives/2021/dir2021-19.pdf

### Maintenance Policy

The maintenence policy governs how jurisdictions keep their VRDB accurate and up-to-date. We represent the voter maintenance policy as a table mapping maintenance reasons and their associated data sources to maintenance thresholds and actions.

| Reason                               | Data source                | Threshold                                     | Action                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------ | -------------------------- | --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Moved in state                       | NCOA                       | Address changes in state                      | Update address, if new county send registration to new county                                                                                                                                                                                                                                                                          |
| Moved out of state                   | NCOA / ERIC                | Address changes out of state                  | Mark inactive -- NCOA                                                                                                                                                                                                                                                                                                                  |
| Undeliverable acknowledgement notice | County                     | Acknowledgement notice could not be delivered | If unable to verify current address, mark inactive                                                                                                                                                                                                                                                                                     |
| Voter inactivity                     | VRDB                       | Lack of activity for two years                | Send confirmation notice via notification methods to voters who have not voted or filled out a registration form in the past two years. Mark voters who do not respond or whose notice is returned as undeliverable as inactive. Cancel voter's registration four years after the notice was mailed if voter continues to be inactive. |
| Death                                | Ohio Department of Health  | Voter dies                                    | Cancel registration - deceased                                                                                                                                                                                                                                                                                                         |
| Crime                                | Clerks of courts of common | Voter convicted of crime                      | Cancel registration - convicted felon                                                                                                                                                                                                                                                                                                  |
| Incompetent                          | State probate judges       | Voter adjudicated incompetent                 | Cancel registration                                                                                                                                                                                                                                                                                                                    |

Sources:

https://www.ohiosos.gov/globalassets/elections/directives/2021/dir2021-03-ch03.pdf

https://www.ncsl.org/research/elections-and-campaigns/voter-list-accuracy.aspx

### Oversight Policy

The oversight policy governs how third parties can review information in the VRDB. We represent the oversight policy as a table mapping oversight entities to the type of voter data and other information they can access, along with time periods for oversight.

| Designated auditor     | Voter data                                              | VRDB logs | VRDB code | Interactive access | Time periods                  |
| ---------------------- | ------------------------------------------------------- | --------- | --------- | ------------------ | ----------------------------- |
| Nonprofit              | Yes, as public in accordance with access control policy | No        | No        | No                 | Continuously                  |
| Political organization | Yes, as public in accordance with access control policy | No        | No        | No                 | Continuously                  |
| Third party pentester  | No                                                      | Yes       | Yes       | Yes                | Not specified |
| VoteShield             | Yes, as public in accordance with access control policy | No        | No        | No                 | Continuously                  |
| Secretary of State     | Yes                                                     | Yes       | N/A       | N/A                | Continuously                  |