# GitHub Pages and Google Sheets Registration Status

## 14 August 2026 deployment

The organization GitHub Pages workflow completed successfully for commit `ab2a343` (`Submit GitHub Pages registrations to Google Sheets`). The public site now keeps the registration form on the Hackfinity page and shows a **Submit registration** button instead of redirecting students to another website.

The public counter remains in its loading state until the Google Apps Script deployment is updated with the new `doGet(e)` count handler documented in `GOOGLE_SHEETS_SETUP.md`. The existing Apps Script URL is configured in `client/src/lib/googleAppsScript.ts`; the organizer must paste the updated script code into the associated Apps Script project and redeploy the existing Web app before the public live count can be verified.

The shared browser remains signed out at the Google Apps Script page, so the script editor cannot yet be inspected or changed from this session. The organizer must complete Google sign-in in the same browser session and open the project linked to the Hackfinity Registration spreadsheet before the script update can be applied.

## New endpoint check

On 14 August 2026, the organizer supplied a new `/exec` URL. A direct count request to that endpoint timed out with no response through the command-line check, and the browser navigation did not yield a usable JSON response. The GitHub Pages client should not be republished with this endpoint until the Apps Script web app returns the documented `doGet(e)` count response reliably.

The endpoint was subsequently verified using the same browser JSONP callback method as the public website. It returned the non-sensitive payload `{ "ok": true, "count": 2 }`. The organization Pages deployment for commit `12b47e0` was then published successfully with this school Apps Script endpoint.

The published GitHub Pages website was then checked with a cache-busting release URL and displayed **02 Squads registered** while retaining the on-page **Submit registration** form. A controlled registration should be submitted only after organizer confirmation, so the new public submission row can be reviewed in the Google Sheet without polluting the organizer records unexpectedly.
