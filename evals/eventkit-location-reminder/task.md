# Job-Site Reminder Review

## Problem/Feature Description

A field-service app wants to add a reminder when a technician enters a job site. The draft implementation creates a reminder, tries to attach the site's coordinates directly, adds an empty alarm object, skips authorization because the app already has calendar access, and assumes every device has a default Reminders list.

The job sites are fixed coordinates from the company's dispatch database. A future version may also let the technician use their current location to create an ad hoc job-site reminder.

## Output Specification

Write `answer.md` with the corrected EventKit approach. Include the key checks, privacy notes, and a compact Swift sketch if useful.
