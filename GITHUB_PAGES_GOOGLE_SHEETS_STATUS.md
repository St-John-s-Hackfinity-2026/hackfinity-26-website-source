# GitHub Pages and Google Sheets Registration Status

## 14 August 2026 deployment

The organization GitHub Pages workflow completed successfully for commit `ab2a343` (`Submit GitHub Pages registrations to Google Sheets`). The public site now keeps the registration form on the Hackfinity page and shows a **Submit registration** button instead of redirecting students to another website.

The public counter remains in its loading state until the Google Apps Script deployment is updated with the new `doGet(e)` count handler documented in `GOOGLE_SHEETS_SETUP.md`. The existing Apps Script URL is configured in `client/src/lib/googleAppsScript.ts`; the organizer must paste the updated script code into the associated Apps Script project and redeploy the existing Web app before the public live count can be verified.

The shared browser remains signed out at the Google Apps Script page, so the script editor cannot yet be inspected or changed from this session. The organizer must complete Google sign-in in the same browser session and open the project linked to the Hackfinity Registration spreadsheet before the script update can be applied.
