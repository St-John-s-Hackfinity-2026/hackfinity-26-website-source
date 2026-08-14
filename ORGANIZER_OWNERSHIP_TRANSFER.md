# Hackfinity ’26 Organization-Control Transfer Runbook

## Objective

Move operational control away from an individual account without interrupting registrations. Keep the current live site active until the school-managed Google Sheet, Apps Script deployment, and organizer accounts have all been tested with one controlled registration.

> **Recommended control model:** use a school Google Workspace account, at least two school GitHub organization owners, and at least two approved site administrators. Avoid relying on any single student or staff member’s personal account.

> **Selected public route, 14 August 2026:** The public Hackfinity website is hosted by the `St-John-s-Hackfinity-2026` GitHub organization on GitHub Pages. The public form stays on that same page, while the organizer-managed Google Sheet and Apps Script web app receive registrations and supply the read-only public squad count. The organizer will manage the school Google and GitHub accounts manually outside this shared session; no personal credentials are stored or requested here.

| Resource | Current operational role | School-managed target |
|---|---|---|
| GitHub organization | Stores source and public Pages website | Two or more school-controlled organization owners |
| Google Sheet | Receives registration rows | A school-owned Sheet or school Shared Drive file |
| Apps Script web app | Accepts the registration webhook | A fresh deployment made by a school Workspace account |
| Live organizer panel | Searches registrations and saves the webhook URL | Two tested school organizer accounts with the `admin` role |

## 1. Establish the school accounts first

Create or nominate a **school-controlled Google Workspace account** and a **school-controlled GitHub account**. Add a second trusted school staff member as a backup administrator. Do not remove the present personal accounts until the replacement accounts have tested access.

For GitHub, an existing organization owner should invite each school GitHub account as an **Organization owner**, rather than only as a repository collaborator. The school owners should be able to access both `hackfinity-26-website-source` and `hackfinity-26-pages-preview`, including the Pages settings and workflow history.

## 2. Move the registration spreadsheet to school control

If the source and target Google accounts are both personal accounts, share the Sheet with the target account as **Editor**, select **Share**, open the recipient’s role menu, choose **Transfer ownership**, and have the target account accept the request. Google requires the file to be shared with the intended owner before the transfer can be requested. [1]

If the current Sheet is personally owned and the target is a school Google Workspace account, **do not expect a direct ownership transfer to work**. Google states that ownership cannot be transferred between a personal Google Account and a work or school account. In that case, the school should create a Shared Drive, temporarily add the present owner with the required access, and move the Sheet into that Shared Drive; alternatively, the school account can make a new copy of the Sheet. The copy route creates a new Sheet ID, so the Apps Script must be configured with the new ID. [1] [3]

Open the resulting school-managed Sheet and confirm that it contains the `Registrations` tab, the header row, and the existing expected columns from **Submitted Date & Time** through **Member 5 Phone Number**. Give both school administrators editor access.

## 3. Recreate and deploy the Apps Script under the school account

The safest handover is to create a **new standalone Apps Script project** while signed into the school Workspace account. Copy the current script template from the live organizer dashboard or `GOOGLE_SHEETS_SETUP.md`, replace `SHEET_ID` with the school-managed Sheet ID if it changed, and deploy it as a Web app. Set **Execute as** to the school account and use the approved access option needed for public registration posts. Copy the resulting production URL ending in `/exec`.

This redeployment is preferable to moving the active web app across accounts or domains. Google documents that web apps deployed in one domain can cease functioning when ownership changes to a Shared Drive or an account in another domain. Apps Script collaborators can edit, version, and deploy a shared project, but a school Shared Drive is the stronger long-term ownership model when it is available. [2]

## 4. Update the live site webhook and test it

Sign in to the live organizer panel at:

```text
https://neonreg-copxxdu4.manus.space/organizer
```

In **Google Sheets connection**, replace the old webhook with the school account’s new `/exec` URL and select **Save webhook**. Submit one controlled registration and verify all of the following before removing any personal-account access:

| Check | Expected outcome |
|---|---|
| Public registration | The form confirms success on the live service. |
| Live counter | The total squad count increases. |
| Organizer dashboard | The controlled registration appears in the secure list. |
| School-managed Sheet | A new row appears in the `Registrations` tab. |
| Sheet sync status | The organizer dashboard reports `synced`. |

After verification, delete or clearly label the controlled test row and retain the prior Sheet as a read-only archive until the event is complete.

## 5. Give school organizers dashboard access

Each school organizer must sign in to the live site once using their own account so a user record is created. The project’s user model supports `user` and `admin` roles. An existing administrator should then promote the verified school organizer records to `admin`. Keep at least two school admins active and test their access at `/organizer` before removing the prior administrator.

## 6. Finalize live-hosting ownership

### Selected route: shared administration of the current live project

The recommended route is to retain the current full-stack deployment and grant control to two school-managed accounts. This preserves the working database, registration API, Google Sheets configuration, live counter, protected organizer panel, and current public service URL. It avoids a high-risk migration immediately before an event.

The present project owner should open the existing live project and use its project sharing or collaborator controls to invite the two approved school accounts. Grant both accounts the level of access required to manage **deployments, database access, environment settings, domain settings, logs, version history, and project sharing**. Repository access alone is not enough because it does not control the running database or the secure service. Each account should confirm that it can view the project, open the organizer panel, inspect deployment status, and access the relevant project settings.

| Handover check | Completion evidence |
|---|---|
| School hosting administrators | Two school-managed accounts appear as project administrators or collaborators with operational access. |
| GitHub organization | The same or equivalent school accounts are organization owners and can manage Pages workflow settings. |
| Google Sheet and Apps Script | The school-owned Sheet receives the controlled registration row from the new `/exec` endpoint. |
| Live organizer access | Each approved organizer signs in and has the `admin` role. |
| Recovery | The school accounts can view versions and restore the last working deployment if necessary. |

Do not revoke the present owner or remove the active deployment until every row in this table is confirmed. Keep the existing service as the rollback point throughout the transfer.

### Alternative route: full external migration

If school policy requires the live server itself to be outside the current hosting project, the team must migrate the full-stack application to a school-controlled platform with a Node.js server and a MySQL-compatible database. This is not a GitHub Pages migration. It requires a new hosting account, a new database, server-side secrets, a compatible sign-in solution, a protected administrator-access process, database export/import and verification, the Apps Script webhook update, DNS/domain cutover, and a rollback plan. The current app also relies on managed authentication, database, and storage integrations, so an external migration needs a dedicated rebuild and test window rather than a simple GitHub deployment.

### Current blocker and next input needed

The GitHub Pages and Apps Script route has been implemented and a controlled registration test completed successfully. The organizer supplied and controls the active Apps Script deployment outside this session. The remaining organizer action is to review and delete the clearly labelled `SYSTEM TEST — DELETE AFTER REVIEW` row in the Hackfinity Registration Sheet, then retain at least two trusted school Google and GitHub administrators for continuity.

## References

[1] [Google Drive Help — Make someone else the owner of your file](https://support.google.com/docs/answer/2494892?hl=en-GB&co=GENIE.Platform%3DDesktop)

[2] [Google Apps Script — Collaborate with other developers](https://developers.google.com/apps-script/guides/collaborating)

[3] [Google Workspace Admin — Transfer Drive files to a new owner](https://knowledge.workspace.google.com/admin/drive/transfer-drive-files-to-a-new-owner-as-an-admin)
