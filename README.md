# K2 phone reminder scheduler

Calls the authenticated reminder dispatcher at `https://app.dietk.pl/api/phone-reminders?action=dispatch` every five minutes. The application stores schedules and sends Web Push notifications. The repository secret `PHONE_REMINDERS_CRON_SECRET` must match the production server environment variable.

Standard GitHub-hosted runners are free for public repositories. No checkout or third-party action is used. The dispatch job has no repository permissions. A separate monthly job updates `scheduler-heartbeat.json` using the repository-scoped GitHub token to keep the schedule active beyond GitHub's 60-day inactivity window.

GitHub may delay or skip scheduled runs during high load. The dispatcher catches up the last 30 minutes and suppresses duplicate reminders. This service is for reminders, not exact-time alarms. Run the workflow manually from Actions to check delivery. No app source, device profiles, or push subscription keys are stored here.
