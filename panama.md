## Panama Voter Registration Tables

This page contains tables describing the voter registration system of Panama. A full explanation of the table properties can be found in our paper, [A Systematization of Voter Registration Security]().

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

| Parameter | Value |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $p_{\rm elig}$: the voter eligibility criteria                                                                                                                                                              | Panamanian adult citizen who has not: renounced their citizenship explicitly or implicitly (by acquiring another citizenship to which they did not have claim to by birth), served an enemy state, , nor .
| $p_{\rm reg-acts}$: Required actions from the voter in order to register                                                                                                                                    | Submit national identity card application; enroll for remote-voting appropriate, as specified in Article 12 of the CE.                                                                                                                                                                                                                                                                                                                                |
| $p_{\rm reg-methods}$: List of registration methods                                                                                                                                                            | In person; online for remote-voting (may involve virtual interview).                                                                                                                                                                                                                                                                                                                                 |
| $p_{\rm voter-info}$: Types of voter information that are collected and stored                                                                                                                                | A minimum of name(s), last name(s), birth place, sex, picture, blood type, signature, dates of issue and expiry of the national identity card.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| $p_{\rm freeze-reg}$: Period before election during which new registrations are not allowed                                                                                                                   |  Citizens can get added to the voter rolls only if they request their identity cards by July 5th of the year before the general elections (see Article 22 of the CE for information on how underage citizens, who will be 18+ by the time the general elections occur, are handled).                                                                                                                                                                                                                                                                                                                                                    |
| $p_{\rm freeze-db}$: Period before election during which systemic registration removals or other maintenance are not allowed                                                                                          | The final list of voters is published three months before the general elections at the latest.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| $p_{\rm keep-logs}$: Period after an election for which a snapshot and activity logs of the VRDB for that election are kept                                                                                  | Not specified                                                                                                                                                                                                                                                                                                                                                                                                              |
| $p_{\rm elig}$: Voter authentication criteria: How voters are authenticated for various stages of the VRDB process (registering to vote, updating voter registration record, checking in at a pollbook) | National identity card.                                                                                                                                                                                           |

Sources:

https://www.tribunal-electoral.gob.pa/publicaciones/codigo-electoral/

### Access Control Policy

The access control policy determines which entities can access certain fields. We represent the access control policy as a table that maps entities to registration fields, with binary values in each cell denoting whether the entity in that row is allowed to view the data point in that column, for any voter.

| Category         | Entity                                                     | Name                                                  | Home address | Birth Place | Full Date of birth | Email | Phone Number | National ID card number | Dates of issue and expiry of the national ID card | Signature | Gender | Blood Type | Photograph | National ID card of parents | Passport Information |
| ---------------- | ---------------------------------------------------------- | ----------------------------------------------------- | ------------ | ----------- | ------------------ | ----- | ------------ | ----------------------- | ------------------------------------------------- | --------- | ------ | ---------- | ---------- | --------------------------- | -------------------- |
| REGISTER/UPDATE  | Voter being registered                                     | ✓                                                     | ✓            | ✓           | ✓                  | ✓     | ✓            | ✓                       | ✓                                                 | ✓         | ✓      | ✓          | ✓          | ✓                           | ✓                    |
|                  | VRDB                                                       | ✓                                                     | ✓            | ✓           | ✓                  | X     | X            | ✓                       | ✓                                                 | ✓         | ✓      | ✓          | ✓          | X                           | X                    |
|                  | Online registration/update portal                          | ✓                                                     | ✓\*          |             | ✓                  | ✓     | ✓            | ✓                       | X                                                 | X         | X      | X          | ✓          | X                           | ✓                    |
|                  | Tribunal Electoral Officials                               | ✓                                                     | ✓            | ✓           | ✓                  | ✓     | ✓            | ✓                       | ✓                                                 | ✓         | X      | X          | X          | ✓                           | ✓                    |
|                  | Designated Registration Office                             | ✓                                                     | ✓            | ✓           | ✓                  | X     | X            | ✓                       | ✓                                                 | ✓         | ✓      | ✓          | ✓          | X                           | X                    |
|                  |                                                            |                                                       |              |             |                    |       |              |                         |                                                   |           |        |            |            |                             |                      |
| USE REG TO VOTE  | Official at polling place                                  | ✓                                                     | ✓            | ✓           | ✓                  | X     | X            | ✓                       | ✓                                                 | ✓         | ✓      | ✓          | ✓          | X                           | X                    |
|                  |                                                            |                                                       |              |             |                    |       |              |                         |                                                   |           |        |            |            |                             |                      |
| LIST MAINTENANCE | Instituto Nacional de Estadística y Censo                  | X                                                     | ✓            | X           | X                  | X     | X            | X                       | X                                                 | X         | X      | X          | X          | X                           | X                    |
|                  | Public institutions, businesses and private entities       | Varies by institution, but a minimum of home address. |
|                  | Tribunal Electoral                                         | ✓                                                     | ✓            | ✓           | ✓                  |       |              | ✓                       | ✓                                                 | ✓         | ✓      | ✓          | ✓          | X                           | X                    |
|                  | Courts                                                     | Varies by court, but a minimum of home address.       |
|                  |                                                            |                                                       |              |             |                    |       |              |                         |                                                   |           |        |            |            |                             |                      |
| TRANSPARENCY     | The public upon publication of the preliminary voter rolls | ✓                                                     | ✓            | X           | X                  | X     | X            | ✓                       | X                                                 | X         | X      | X          | X          | X                           | X                    |

Sources:

https://www.cepal.org/es/temas/censos-de-poblacion-y-vivienda/enlaces-institutos-nacionales-estadistica-america-latina-caribe
https://www.tribunal-electoral.gob.pa/tramite-de-cedula-por-primera-vez/	
https://tribunalcontigo.com/	
https://www.tribunal-electoral.gob.pa/publicaciones/codigo-electoral/	


### System Change Control Policy

Panama has public documentation outlining the specific steps that must be followed to make system changes, the most notable of which are the procedure manuals of the Infrastructure Management and the Information Security Management. Thus, this represents their specific implementation of the system change control policy. We omitted an independent construction of the corresponding table for Panama, because it is covered by these documents.

Sources:

https://www.tribunal-electoral.gob.pa/wp-content/uploads/2020/07/Proc.-Gral.-Gesti%C3%B3n-de-Infraestructura.pdf
https://www.tribunal-electoral.gob.pa/wp-content/uploads/2021/11/Proc.-Gral.-Gestio%CC%81n-para-la-Seguridad-Informatica-Enero-2021.pdf

### Data Change Control Policy

The data change control policy includes information about the entities involved in updating the VRDB or associated policies. We represent the data change control policy as a table that specifies the entities allowed to authorize/start updates, trigger updates (send updated data to election officials), and execute the update (directly modify the data inside the VRDB). In this table, we map these entities to the type of data they update, and if there is a notification involved in this type of update.

| Category      | Entity                                                                   | Type of Data                       |
| ------------- | ------------------------------------------------------------------------ | ---------------------------------- |
| Authorization | Voter                                                                    | Personal data.                      |
|               | Tribunal Electoral officials                                             | Updated data from national census or other maintenance activities.  |
| Trigger       | Online update portal                                                     | Data from voter who started update. |
|               | Instituto Nacional de Estadística y Censo                                                                                      | Updated data after census. |
|               | Public institutions, businesses and private entities                                                                                   | Updated data after declaration of residence for use of service.     |
|               | Tribunal Electoral officials                                             | Data of new/updated national identity card.        |
|               | Courts                                                                   | Legal documents denoting removal or addition from voter rolls (e.g., lose of citizenship, prison sentence, etc).                 |
| Execution     | Tribunal Electoral officials                                                 |                                    |

Sources:

https://www.inec.gob.pa/
https://www.tribunal-electoral.gob.pa/publicaciones/codigo-electoral/

### Voter Data Use Policy

The voter data use policy specifies limitations on how (and by whom) the data can be used.

| Category | Value |
|----------------------|-------------------------------------------------------------------------------------------|
| Prohibited uses      | The preliminary voter rolls published before an election can only be used for voters to verify their information, and nothing else.                                                                           |
| Approved entities    | Only those approved to use the Identity Verification Service (SVI).                                                                                    |
| Information released | Names, national identity card number, day and place of birth, and names of parents. Public documentation on SVI claims that, as of August 2017, signature and photographs will also be available via this service ``in the near future''. It is unclear if this has been implemented yet or not.                                                         |
| Opt out policy       | Not specified. |

Sources:

https://www.tribunal-electoral.gob.pa/direccion-superior/secretaria-general/servicio-verificacion-identidad-svi/
https://www.tribunal-electoral.gob.pa/publicaciones/codigo-electoral/

### Voter Notification Policy

The voter notification policy governs how jurisidictions notify voters of various changes to their records. We represent the voter notification policies as a table mapping notification reasons to notification protocols and methods.

| Notification reason     | Notification protocol                                                                                                                                                                                               | Notification methods    |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| Voter inactivity (fail to vote in three consecutive general elections or do not participate in any processes (related to voting or not) through the Tribunal Electoral) | Publish list in the Tribunal Electoral's website.                                                                                                                                                                                | Online. |
| Eligibility for an election       | Publication of preliminary and final voter rolls, at dedicated times before an election, either through the Tribunal Electoral's website or through offices of lower jurisdictional levels.                                                                                                                             | Online and through other government offices. |

Sources:

https://www.tribunal-electoral.gob.pa/publicaciones/codigo-electoral/

### Maintenance Policy

The maintenence policy governs how jurisdictions keep their VRDB accurate and up-to-date. We represent the voter maintenance policy as a table mapping maintenance reasons and their associated data sources to maintenance thresholds and actions.

In Panama, most updates to voter data come directly from the voters themselves, so maintenance activities are fairly limited in scope.

| Reason                                  | Data source                                                              | Threshold                                            | Action                                                      |
| --------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------------------- | ----------------------------------------------------------- |
| Updated data after census | Instituto Nacional de Estadística y Censo                                                    | Updated voter data              | Update existing record.                    |
| Change of address.                          | Public institutions, businesses and private entities                                                                    | Updated data after declaration of residence for use of service.                             | Update address.                                              |
| Voter inactivity                        | Tribunal Electoral                                                                     | After notification, if they fail to vote in three consecutive general elections or do not participate in any processes (related to voting or not) through the Tribunal Electoral.                  | Mark inactive. |
| Cime                                   | Courts | Voter currently incarcerated for a felony. conviction                                           | Delete or add to voter rolls (due to e.g., lose of citizenship, prison sentence, etc).                              |

Sources:
https://www.inec.gob.pa/
https://www.tribunal-electoral.gob.pa/publicaciones/codigo-electoral/

### Oversight Policy

The oversight policy governs how third parties can review information in the VRDB. We represent the oversight policy as a table mapping oversight entities to the type of voter data and other information they can access, along with time periods for oversight.

| Designated auditor     | Voter data                                              | VRDB logs | VRDB code | Interactive access | Time periods                 |
| ---------------------- | ------------------------------------------------------- | --------- | --------- | ------------------ | ---------------------------- |
| Voters              | Yes, as public in accordance with access control policy | No        | No        | Yes                 | Upon publication of preliminary voter rolls, up to publication of final voter rolls (three months before the general elections at the latest).               |

Sources:

https://www.tribunal-electoral.gob.pa/publicaciones/codigo-electoral/
