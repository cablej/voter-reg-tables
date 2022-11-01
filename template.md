## Template Voter Registration Tables

This page contains template voter registration system tables. A full explanation of the table properties can be found in our paper, [A Systematization of Voter Registration Security]().

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

| Parameter                                                    | Value |
| ------------------------------------------------------------ | ----- |
| $p_{\rm elig}$: the voter eligibility criteria               |       |
| $p_{\rm reg-acts}$: Required actions from the voter in order to register |       |
| $p_{\rm reg-methods}$: List of registration methods          |       |
| $p_{\rm voter-info}$: Types of voter information that are collected and stored |       |
| $p_{\rm freeze-reg}$: Period before election during which new registrations are not allowed |       |
| $p_{\rm freeze-db}$: Period before election during which systemic registration removals or other maintenance are not allowed |       |
| $p_{\rm keep-logs}$: Period after an election for which a snapshot and activity logs of the VRDB for that election are kept |       |
| $p_{\rm elig}$: Voter authentication criteria: How voters are authenticated for various stages of the VRDB process (registering to vote, updating voter registration record, checking in at a pollbook) |       |

### Access Control Policy

The access control policy determines which entities can access certain fields. We represent the access control policy as a table that maps entities to registration fields, with binary values in each cell denoting whether the entity in that row is allowed to view the data point in that column, for any voter.

| Category         | Entity                                         | Name | Home address | Mailing address | Full Date of birth | Telephone number | Email address | Driver's license / ID card number | Social Security Number last 4 digits | Date of affiliation | Signature | Voting activity history |
| ---------------- | ---------------------------------------------- | ---- | ------------ | --------------- | ------------------ | ------- | ------------- | --------------------------------- | ----------------- | ------------------- | --------- | ----------------------- |
| REGISTER/UPDATE  | Voter being registered                         |     |             |                |                   |        |              |                                  |                  |                    |          |                        |
|                  | VRDB                                           |     |             |                |                   |        |              |                                  |                  |                    |          |                        |
|                  | Online registration/update portal      |     |             |                |                   |        |              |                                  |                  |                    |          |                        |
|                  | County clerk  |     |             |                |                   |        |              |                                  |                  |                    |          |                        |
|                  | Other: [enter] |      |              |                 |                    |         |               |                                   |                   |                     |           |                         |
| USE REG TO VOTE  | County official at polling place            |     |            |               |                   |       |            |                                |                |                    |        |                      |
|                  | County official processing absentee ballots |     |            |               |                   |       |            |                                |                |                    |        |                      |
|                  | Other: [enter] |      |              |                 |                    |         |               |                                   |                   |                     |           |                         |
| LIST MAINTENANCE | State agencies for maintenance: [enter]        |   |           |              |                 |      |            |                                |                |                  |        |                      |
|                  | Other third parties for maintenance: [enter] |     |             |                |                  |        |              |                                 |                 |                  |        |                        |
| TRANSPARENCY     | The public                                     |   |           |              |                 |      |            |                                |                |                    |        |                        |
|                  | Other: [enter] |      |              |                 |                    |         |               |                                   |                   |                     |           |                         |

### System Change Control Policy

The system change control policy specifies how election officials may modify the voter registration system.

|             | Description | Planification | Evaluation | Review | Authorization | Execution | Communication | Logging | How often is the system evaluated for these updates |
| ----------- | ----------- | ------------- | ---------- | ------ | ------------- | --------- | ------------- | ------- | --------------------------------------------------- |
| STANDARD    |             |               |            |        |               |           |               |         |                                                     |
| MINOR       |             |               |            |        |               |           |               |         |                                                     |
| MAJOR       |             |               |            |        |               |           |               |         |                                                     |
| SIGNIFICANT |             |               |            |        |               |           |               |         |                                                     |
| EMERGENCY   |             |               |            |        |               |           |               |         |                                                     |

### Data Change Control Policy

The data change control policy includes information about the entities involved in updating the VRDB or associated policies. We represent the data change control policy as a table that specifies the entities allowed to authorize/start updates, trigger updates (send updated data to election officials), and execute the update (directly modify the data inside the VRDB). In this table, we map these entities to the type of data they update, and if there is a notification involved in this type of update.

| Category      | Entity                                                       | Type of Data |
| ------------- | ------------------------------------------------------------ | ------------ |
| Authorization | Voter                                                        |              |
|               | Election officials                                           |              |
| Trigger       | Online update portal                                         |              |
|               | Mail                                                         |              |
|               | State agencies for update (e.g., DMV): [enter]               |              |
|               | List maintenance mechanism (e.g., ERIC): [enter]             |              |
|               | Other: [enter]                                               |              |
| Execution     | State election officials                                     |              |
|               | County election officials                                    |              |

### Voter Data Use Policy

The voter data use policy specifies limitations on how (and by whom) the data can be used.

| Category             | Value |
| -------------------- | ----- |
| Prohibited uses      |       |
| Approved entities    |       |
| Information released |       |
| Opt out policy       |       |

### Voter Notification Policy

The voter notification policy governs how jurisidictions notify voters of various changes to their records. We represent the voter notification policies as a table mapping notification reasons to notification protocols and methods.

| Notification reason                   | Notification protocol | Notification methods |
| ------------------------------------- | --------------------- | -------------------- |
| Incomplete or ineligable registration |                       |                      |
| New registration                      |                       |                      |
| Inactive registration                 |                       |                      |
| Address change                        |                       |                      |
| Deceased voter                        |                       |                      |

### Maintenance Policy

The maintenence policy governs how jurisdictions keep their VRDB accurate and up-to-date. We represent the voter maintenance policy as a table mapping maintenance reasons and their associated data sources to maintenance thresholds and actions.

| Reason             | Data source                                                | Threshold | Action |
| ------------------ | ---------------------------------------------------------- | --------- | ------ |
| Moved in state     | NCOA                                                       |           |        |
| Moved out of state | NCOA, ERIC                                                 |           |        |
| Voter inactivity   | VRDB                                                       |           |        |
| Death              | Registrar of Vital Statistics, Social Security Death Index |           |        |
| Crime              | Department of Corrections                                  |           |        |
| Incompetent        | Circuit Courts                                             |           |        |

### Oversight Policy

The oversight policy governs how third parties can review information in the VRDB. We represent the oversight policy as a table mapping oversight entities to the type of voter data and other information they can access, along with time periods for oversight.

| Designated auditor     | Voter data | VRDB logs | VRDB code | Interactive access | Time periods |
| ---------------------- | ---------- | --------- | --------- | ------------------ | ------------ |
| Nonprofit              |            |           |           |                    |              |
| Political organization |            |           |           |                    |              |
| Third party pentester  |            |           |           |                    |              |
| Other: [enter]         |            |           |           |                    |              |
