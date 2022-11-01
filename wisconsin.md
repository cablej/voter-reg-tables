## Wisconsin Voter Registration Tables

This page contains tables describing the voter registration system of Wisconsin. A full explanation of the table properties can be found in our paper, [A Systematization of Voter Registration Security]().

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

| Parameter                                                                                                                                                                                               | Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $p_{\rm elig}$: the voter eligibility criteria                                                                                                                                                          | • At least 18 years old<br />• U.S. citizen<br />• Reside at current address for at least 28 days prior to election<br />• Cannot be serving a felony sentence<br />• Cannot be adjudicated incompetent for voting purposes<br />• Cannot have placed a bet or wager on outcome of the election<br />• Can only vote once                                                                                                                                                                                                                                                                                                               |
| $p_{\rm reg-acts}$: Required actions from the voter in order to register                                                                                                                                | Submit voter registration application with proof of residence documentation, as described in voter authentication criteria                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| $p_{\rm reg-methods}$: List of registration methods                                                                                                                                                     | Online, mail, in person                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| $p_{\rm voter-info}$: Types of voter information that are collected and stored                                                                                                                          | See Access Control Policy table                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| $p_{\rm freeze-reg}$: Period before election during which new registrations are not allowed                                                                                                             | Standard registration:<br />• In-person: 5pm on 3rd Wednesday preceding the election\*<br />• Mail: Postmarked by 3rd Wednesday preceding election\*<br />• Online: 11:59pm on 3rd Wednesday preceding election<br/>Late registration:<br />• In-person: 5pm on Friday preceding the election\*:<br /> \*: excluding same day registrations, which are allowed in-person on election day                                                                                                                                                                                                                                                |
| $p_{\rm freeze-db}$: Period before election during which systemic registration removals or other maintenance are not allowed                                                                            | 90 days                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| $p_{\rm keep-logs}$: Period after an election for which a snapshot and activity logs of the VRDB for that election are kept                                                                             | Poll lists must be kept for at least 22 months after election. Voter registration forms must be kept for at least 4 years after a voter's record is changed to inelgible status.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| $p_{\rm elig}$: Voter authentication criteria: How voters are authenticated for various stages of the VRDB process (registering to vote, updating voter registration record, checking in at a pollbook) | New registration: Driver's license number or SSN last 4, proof of residence document<br />Updating record: DoB, driver's license number or SSN last 4, proof of residence<br />Looking up record online: First name, last name, date of birth<br />Checking in at pollbook: 1 form of photo ID, state name and address\*<br />Absentee ballot: voter signature, witness signature, and address<br />First time absentee request (or if voter moves or changes name): photocopy of photo ID<br />\*: Voters with a confidential listing state their name and present their identification card in lieu of providing their address and ID |

Sources:

https://bringit.wi.gov/sites/bringit/files/3%204%20Voter%20Eligibility-2020%20july%20update.pdf

https://docs.legis.wisconsin.gov/statutes/statutes/6.pdf

https://docs.legis.wisconsin.gov/code/admin_code/el/3.pdf

https://www.wisconsinhistory.org/pdfs/la/locrecsManual/WMRS-Election.pdf

https://docs.legis.wisconsin.gov/statutes/statutes/6/ii/29/2/a

https://docs.legis.wisconsin.gov/statutes/statutes/7.pdf

### Access Control Policy

The access control policy determines which entities can access certain fields. We represent the access control policy as a table that maps entities to registration fields, with binary values in each cell denoting whether the entity in that row is allowed to view the data point in that column, for any voter.

\*: hidden for address confidentiality program and confidential voters

†: only accessible by designated address confidentiality program election staff

‡: hashed before sending to ERIC

| Category         | Entity                                         | Name | Home address | Mailing address | Full Date of birth | Tel num | Email address | Driver's license / ID card number | SSN last 4 digits | Date of affiliation | Signature | Voting activity history |
| ---------------- | ---------------------------------------------- | ---- | ------------ | --------------- | ------------------ | ------- | ------------- | --------------------------------- | ----------------- | ------------------- | --------- | ----------------------- |
| REGISTER/UPDATE  | Voter being registered                         | ✓    | ✓            | ✓               | ✓                  | ✓       | ✓             | ✓                                 | ✓                 | ✓                   | ✓         | ✓                       |
|                  | VRDB                                           | ✓    | ✓            | ✓               | ✓                  | ✓       | ✓             | ✓                                 | ✓                 | ✓                   | ✓         | ✓                       |
|                  | State online registration/update portal‡       | ✓    | ✓            | ✓               | ✓                  | ✓       | ✓             | ✓                                 | ✓                 | ✓                   | ✓         | ✓                       |
|                  | County or municipal clerk                      | ✓    | ✓            | ✓               | ✓                  | ✓       | ✓             | ✓                                 | ✓                 | ✓                   | ✓         | ✓                       |
| USE REG TO VOTE  | Municipal official at polling place            | ✓    | ✓†           | ✓†              | ✓                  | ✓†      | X             | X                                 | X                 | ✓                   | X         | X                       |
|                  | Municipal official processing absentee ballots | ✓    | ✓†           | ✓†              | ✓                  | ✓†      | X             | X                                 | X                 | ✓                   | X         | X                       |
| LIST MAINTENANCE | NCOA                                           | X    | X            | X               | X                  | X       | X             | X                                 | X                 | X                   | X         | X                       |
|                  | ERIC                                           | ✓    | ✓            | ✓               | ✓‡                 | ✓       | ✓             | ✓‡                                | ✓‡                | X                   | X         | ✓                       |
| TRANSPARENCY     | The public                                     | ✓\*  | ✓\*          | ✓\*             | X                  | ✓\*     | ✓\*           | X                                 | X                 | ✓                   | X         | ✓                       |

Sources:

https://www.ncsl.org/research/elections-and-campaigns/access-to-and-use-of-voter-registration-lists.aspx

https://docs.legis.wisconsin.gov/statutes/statutes/6/ii/47

### System Change Control Policy

Wisconsin does not publish information related to the system change control policy. See [here](template.md#system-change-control-policy) for a template table.

### Data Change Control Policy

The data change control policy includes information about the entities involved in updating the VRDB or associated policies. We represent the data change
control policy as a table that specifies the entities allowed to authorize/start updates, trigger updates (send updated data to election officials), and execute the update (directly modify the data inside
the VRDB). In this table, we map these entities to the type of data they update, and if there is a notification involved in this type of update.

| Category      | Entity                                                                        | Type of Data                                                               |
| ------------- | ----------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Authorization | Voter                                                                         | Personal data                                                              |
|               | State, county, and municipal election officials                               | Data from list maintenance update                                          |
| Trigger       | State online update portal                                                    | Data from voter who started update                                         |
|               | Mail                                                                          | Data from voter who started update                                         |
|               | ERIC                                                                          | Data of voters in other states                                             |
|               | Municipal departments and agencies                                            | Data of vote move                                                          |
|               | NCOA                                                                          | Data of voter move                                                         |
|               | Municipal clerk or board of elections (via checking vital statistics reports) | Data of death                                                              |
|               | Wisconsin Circuit Courts                                                      | Individuals declared incompetent                                           |
|               | Wisconsin Department of Corrections                                           | People convicted of a felony and whose civil rights have not been restored |
| Execution     | State election officials                                                      |                                                                            |
|               | County election officials                                                     |                                                                            |
|               | Municipal election officials                                                  |

Sources:

https://www.ncsl.org/research/elections-and-campaigns/voter-list-accuracy.aspx

https://docs.legis.wisconsin.gov/statutes/statutes/6.pdf

https://docs.legis.wisconsin.gov/statutes/statutes/54.pdf

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

| Notification reason                   | Notification protocol                                                                                                                                                                                                                                                                                                                                                                                                                                              | Notification methods | Notes                                                                                                                                                                                                                                    |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Incomplete or ineligable registration | Send notice via notification methods                                                                                                                                                                                                                                                                                                                                                                                                                               | Mail                 |                                                                                                                                                                                                                                          |
| New registration                      | Send acknowledgement notice via notification methods by non-forwardable mail if by mail. If mail is returned as undeliverable, or informed of a different address, mark voter as ineligible.                                                                                                                                                                                                                                                                       | Mail                 | Notification occurs if the voter registered online, by mail, or in person at polling place on election day. Notification is not required if the voter registered in person at the clerk's office.                                        |
| Inactive registration                 | If a voter has not voted within the last 4 years, Wisconsin Election Commission mails a notice to the voter that their registration will be suspended. If the voter does not apply for continuation of registration within 30 days (by mail or in person), mark as ineligible.                                                                                                                                                                                     | Mail                 |                                                                                                                                                                                                                                          |
| Address change                        | If new address is outside of the municipality: Municipal clerk or board of election commissioners sends notice via notification methods. If the elector no longer resides in the municipality or does not apply for continuation of registration within 30 days, mark voter as ineligible.<br>If new address is in the same municipality: Municipal clerk or board of election commissioners change voter's address and notify the voter via notification methods. | Mail                 | Notification is not required if the state learns of the address change from the appropriate election administrative authority of another state, terriritory, or possession that the individual appears on their voter registration list. |
| Deceased voter                        | None                                                                                                                                                                                                                                                                                                                                                                                                                                                               | N/A                  |

Sources:

https://docs.legis.wisconsin.gov/statutes/statutes/6/

https://docs.legis.wisconsin.gov/statutes/statutes/6/ii/50

### Maintenance Policy

The maintenence policy governs how jurisdictions keep their VRDB accurate and up-to-date. We represent the voter maintenance policy as a table mapping maintenance reasons and their associated data sources to maintenance thresholds and actions.

| Reason                    | Data source                                                                   | Threshold                                                                 | Action                                                                                                                      |
| ------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Moved in municipality     | NCOA, municipal departments and agencies                                      | Address changes in municipality                                           | Update address                                                                                                              |
| Moved out of municipality | NCOA, ERIC, municipal departments and agencies                                | Address changes out of municipality                                       | Notify voter; mark ineligible if voter no longer resides in municipality or fails to apply for continuation of registration |
| Voter inactivity          | VRDB                                                                          | Has not voted within previous 4 years                                     | Notify voter; mark ineligible if voter does not respond within 30 days                                                      |
| Death                     | Municipal clerk or board of elections (via checking vital statistics reports) | Voter dies                                                                | Mark ineligible                                                                                                             |
| Crime                     | Wisconsin Department of Corrections                                           | Voter convicted of a felony and whose civil rights have not been restored | Mark ineligible                                                                                                             |
| Incompetent               | Wisconsin Circuit Courts                                                      | Voter declared incompetent                                                | Mark ineligible                                                                                                             |

Sources:

https://docs.legis.wisconsin.gov/statutes/statutes/6/

https://www.ncsl.org/research/elections-and-campaigns/voter-list-accuracy.aspx

### Oversight Policy

The oversight policy governs how third parties can review information in the VRDB. We represent the oversight policy as a table mapping oversight entities to the type of voter data and other information they can access, along with time periods for oversight.

| Designated auditor                     | Voter data                                              | VRDB logs | VRDB code | Interactive access | Time periods |
| -------------------------------------- | ------------------------------------------------------- | --------- | --------- | ------------------ | ------------ |
| Nonprofit                              | Yes, as public in accordance with access control policy | No        | No        | No                 | Continuously |
| Political organization                 | Yes, as public in accordance with access control policy | No        | No        | No                 | Continuously |
| Third party pentester (including CISA) | No                                                      | Yes       | Yes       | Yes                | Not defined  |
| VoteShield                             | Yes, as public in accordance with access control policy | No        | No        | No                 | Continuously |
| Elections Commission                   | Yes                                                     | Yes       | N/A       | N/A                | Continuously |
