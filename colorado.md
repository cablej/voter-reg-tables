## Colorado Voter Registration Tables

This page contains tables describing the voter registration system of Colorado. A full explanation of the table properties can be found in our paper, [A Systematization of Voter Registration Security]().

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

| Parameter                                                                                                                                                                                               | Value                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $p_{\rm elig}$: the voter eligibility criteria                                                                                                                                                          | To be eligible to vote, you must be:<br><br>• A U.S. Citizen<br>• 16 years of age, but you must be at least 17 years old to vote in a primary election if you will be 18 years old or older before the next General election.<br>• 16 years of age, but you must be at least 18 years old to vote in any other election<br>• A Colorado resident for at least 22 days before an election<br>• Not serving a sentence for a felony conviction |
| $p_{\rm reg-acts}$: Required actions from the voter in order to register                                                                                                                                | None (for automatic voter registration), otherwise submit voter registration application                                                                                                                                                                                                                                                                                                                                                     |
| $p_{\rm reg-methods}$: List of registration methods                                                                                                                                                     | Online, email, fax, mail, in person                                                                                                                                                                                                                                                                                                                                                                                                          |
| $p_{\rm voter-info}$: Types of voter information that are collected and stored                                                                                                                          | See Access Control Policy Table                                                                                                                                                                                                                                                                                                                                                                                                              |
| $p_{\rm freeze-reg}$: Period before election during which new registrations are not allowed                                                                                                             | 8 days before election (mail/online), up to and on election day (in person). County election officials may choose to process registrations submitted later than 8 days.                                                                                                                                                                                                                                                                      |
| $p_{\rm freeze-db}$: Period before election during which systemic registration removals or other maintenance are not allowed                                                                            | 90 days                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| $p_{\rm keep-logs}$: Period after an election for which a snapshot and activity logs of the VRDB for that election are kept                                                                             | At least 2 years                                                                                                                                                                                                                                                                                                                                                                                                                             |
| $p_{\rm elig}$: Voter authentication criteria: How voters are authenticated for various stages of the VRDB process (registering to vote, updating voter registration record, checking in at a pollbook) | Updating record: Date of birth/driver's license number or last 4 digits of social security number, signature<br>Looking up record online: Name, zip code, date of birth<br>Checking in at pollbook: 1 form of ID<br>Vote by mail: signature, if first time may need to provide copy of ID                                                                                                                                                    |

Sources:

https://www.sos.state.co.us/pubs/rule_making/files/2021/20210617ElectionRules8CCR1505-1.pdf

https://casetext.com/statute/colorado-revised-statutes/title-1-elections/general-primary-recall-and-congressional-vacancy-elections/article-2-qualifications-and-registration-of-electors/part-5-mail-registration-and-registrationat-voter-registration-agencies/section-1-2-510-public-disclosure-of-voter-registration-activities

### Access Control Policy

The access control policy determines which entities can access certain fields. We represent the access control policy as a table that maps entities to registration fields, with binary values in each cell denoting whether the entity in that row is allowed to view the data point in that column, for any voter.

\*: hidden for address confidentiality program and confidential voters

†: only accessible by designated address confidentiality program election staff

‡: hashed before sending to ERIC

| Category         | Entity                                     | Name | Home address | Mailing address | Year of birth | Full Date of birth | Telephone number | Email address | Driver's license / ID card number | Full SSN | SSN last 4 digits | Political Party affiliation | Date of affiliation | Gender identity | Signature | Voting activity history |
| ---------------- | ------------------------------------------ | ---- | ------------ | --------------- | ------------- | ------------------ | ---------------- | ------------- | --------------------------------- | -------- | ----------------- | --------------------------- | ------------------- | --------------- | --------- | ----------------------- |
| REGISTER/UPDATE  | Voter being registered                     | ✓    | ✓            | ✓               | ✓             | ✓                  | ✓                | ✓             | ✓                                 | X        | ✓                 | ✓                           | ✓                   | ✓               | ✓         | ✓                       |
|                  | VRDB                                       | ✓    | ✓            | ✓               | ✓             | ✓                  | ✓                | ✓             | ✓                                 | X        | ✓                 | ✓                           | ✓                   | ✓               | ✓         | ✓                       |
|                  | Online registration/update portal          | ✓    | ✓\*          | ✓\*             | ✓             | ✓                  | ✓\*              | ✓             | ✓                                 | X        | ✓                 | ✓                           | ✓                   | ✓               | ✓         | ✓                       |
|                  | DMV (when registering)                     | ✓    | ✓            | ✓               | ✓             | ✓                  | ✓                | ✓             | ✓                                 | X        | ✓                 | ✓                           | ✓                   | ✓               | ✓         | ✓                       |
|                  | County clerk                               | ✓    | ✓†           | ✓†              | ✓             | ✓                  | ✓†               | ✓             | ✓                                 | X        | ✓                 | ✓                           | ✓                   | ✓               | ✓         | ✓                       |
| USE REG TO VOTE  | County official at polling place           | ✓    | ✓†           | ✓†              | ✓             | ✓                  | ✓†               | X             | ✓                                 | X        | X                 | ✓                           | ✓                   | ✓               | ✓         | X                       |
|                  | County official processing mail-in ballots | ✓    | ✓†           | ✓†              | ✓             | ✓                  | ✓†               | X             | ✓                                 | X        | X                 | ✓                           | ✓                   | ✓               | ✓         | X                       |
| LIST MAINTENANCE | NCOA                                       | X    | X            | X               | X             | X                  | X                | X             | X                                 | X        | X                 | X                           | X                   | X               | X         | X                       |
|                  | Department of Revenue                      | X    | X            | X               | X             | X                  | X                | X             | X                                 | X        | X                 | X                           | X                   | X               | X         | X                       |
|                  | ERIC                                       | ✓    | ✓            | ✓‡              | ✓‡            | ✓                  | ✓                | ✓‡            | ✓‡                                | X        | ✓                 | X                           | X                   | X               | X         | ✓                       |
| TRANSPARENCY     | The public                                 | ✓    | ✓\*          | ✓\*             | ✓             | X                  | ✓\*              | X             | X                                 | X        | X                 | ✓                           | ✓                   | ✓               | X         | ✓                       |

Sources:

https://www.ncsl.org/research/elections-and-campaigns/access-to-and-use-of-voter-registration-lists.aspx

https://www.sos.state.co.us/pubs/elections/FAQs/VoterRegistrationData.html

https://www.sos.state.co.us/pubs/elections/vote/VoterRegFormEnglish.pdf

https://www.sos.state.co.us/pubs/elections/LawsRules/committeeFiles/BEAClistMaintenance.pdf

https://www.sos.state.co.us/pubs/elections/FAQs/VoterRegistrationFAQ.html

https://dcs.colorado.gov/acp/about-the-acp

### System Change Control Policy

Colorado does not publish information related to the system change control policy. See [here](example.md#system-change-control-policy) for a template table.

### Data Change Control Policy

The data change control policy includes information about the entities involved in updating the VRDB or associated policies. We represent the data change
control policy as a table that specifies the entities allowed to authorize/start updates, trigger updates (send updated data to election officials), and execute the update (directly modify the data inside
the VRDB). In this table, we map these entities to the type of data they update, and if there is a notification involved in this type of update.

| Category      | Entity                                                                   | Type of Data                       |
| ------------- | ------------------------------------------------------------------------ | ---------------------------------- |
| Authorization | Voter                                                                    | Personal data                      |
|               | State and county election officials                                      | Data from list maintenance update  |
| Trigger       | Online update portal                                                     | Data from voter who started update |
|               | Mail                                                                     | Data from voter who started update |
|               | ERIC                                                                     | Data of voters in other states     |
|               | Department of Revenue (DMV)                                              | Data of new/updated license        |
|               | NCOA                                                                     | Data of voter move                 |
|               | Department of Public Health and Environment, Social Security Death Index | Data of death                      |
|               | Colorado Department of Corrections, Colorado U.S. Attorney's office      | Voters who committed crime         |
| Execution     | State election officials                                                 |                                    |
|               | County election officials                                                |

### Voter Data Use Policy

The voter data use policy specifies limitations on how (and by whom) the data can be used.

| Category             | Value                                                                                     |
| -------------------- | ----------------------------------------------------------------------------------------- |
| Prohibited uses      | Not specified.                                                                            |
| Approved entities    | Public                                                                                    |
| Information released | See access control policy table.                                                          |
| Opt out policy       | Address Confidentiality Program (ACP) participants; confidential voters; pre-registrants. |

### Voter Notification Policy

The voter notification policy governs how jurisidictions notify voters of various changes to their records. We represent the voter notification policies as a
table mapping notification reasons to notification protocols and methods.

| Notification reason     | Notification protocol                                                                                                                                                                                               | Notification methods    |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| Incomplete registration | Send notice via notification methods                                                                                                                                                                                | Mail, Email (by county) |
| New registration        | Send notice via notification methods. If returned as undeliverable, do not register. If not returned as undeliverable, register.                                                                                    | Mail, Email (by county) |
| Inactive registration   | Send elector voter confirmation card at least 60 days before election via notification methods. If not returned or not marked undeliverable, and voter has not voted in two general elections, cancel registration. | Mail, Email (by county) |
| Address change          | Send notice to new address.                                                                                                                                                                                         | Mail, Email (by county) |
| Cancelled registration  | None                                                                                                                                                                                                                | N/A                     |

Sources:

https://casetext.com/statute/colorado-revised-statutes/title-1-elections/general-primary-recall-and-congressional-vacancy-elections/article-2-qualifications-and-registration-of-electors/part-5-mail-registration-and-registrationat-voter-registration-agencies/section-1-2-509-reviewing-voter-registration-applications-notification

https://casetext.com/statute/colorado-revised-statutes/title-1-elections/general-primary-recall-and-congressional-vacancy-elections/article-2-qualifications-and-registration-of-electors/part-5-mail-registration-and-registrationat-voter-registration-agencies

### Maintenance Policy

The maintenence policy governs how jurisdictions keep their VRDB accurate and up-to-date. We represent the voter maintenance policy as a table mapping
maintenance reasons and their associated data sources to maintenance thresholds and actions.

| Reason                                  | Data source                                                              | Threshold                                            | Action                                                      |
| --------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------------------- | ----------------------------------------------------------- |
| New driver's license or updated address | Department of Revenue                                                    | New driver's license or updated address              | Register voter or update existing record                    |
| Moved in state                          | NCOA                                                                     | Address changes in state                             | Update address                                              |
| Moved out of state                      | NCOA / ERIC                                                              | Address changes out of state                         | Mark inactive -- NCOA                                       |
| Returned mail                           | County                                                                   | Returned mail                                        | Mark inactive -- returned mail                              |
| Undeliverable ballot                    | County                                                                   | Ballot could not be delivered                        | Mark inactive -- undeliverable ballot                       |
| Voter inactivity                        | VRDB                                                                     | Has not voted in past two elections                  | Mark inactive; cancel reg after two more inactive elections |
| Death                                   | Department of Public Health and Environment, Social Security Death Index | Voter dies                                           | Cancel registration - deceased                              |
| Crime                                   | Colorado Department of Corrections, Colorado U.S. Attorney's office      | Voter currently incarcerated for a felony conviction | Cancel registration - convicted felon                       |

Sources:

https://www.sos.state.co.us/pubs/elections/LawsRules/committeeFiles/BEAClistMaintenance.pdf

https://www.ncsl.org/research/elections-and-campaigns/voter-list-accuracy.aspx

https://www.sos.state.co.us/pubs/rule_making/files/2021/20210617ElectionRules8CCR1505-1.pdf

### Oversight Policy

The oversight policy governs how third parties can review information in the VRDB. We represent the oversight policy as a table mapping oversight entities to the
type of voter data and other information they can access, along with time periods for oversight.

| Designated auditor     | Voter data                                              | VRDB logs | VRDB code | Interactive access | Time periods                 |
| ---------------------- | ------------------------------------------------------- | --------- | --------- | ------------------ | ---------------------------- |
| Nonprofit              | Yes, as public in accordance with access control policy | No        | No        | No                 | Continuously                 |
| Political organization | Yes, as public in accordance with access control policy | No        | No        | No                 | Continuously                 |
| Third party pentester  | No                                                      | Yes       | Yes       | Yes                | Over 90 days before election |
| VoteShield             | Yes, as public in accordance with access control policy | No        | No        | No                 | Continuously                 |
| Department of State    | Yes                                                     | Yes       | N/A       | N/A                | Continuously                 |
