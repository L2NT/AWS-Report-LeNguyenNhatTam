---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
### Week 4 Objectives:

* Automate cleanup of unconfirmed Cognito accounts with Amazon EventBridge.
* Add "Sign in with Google" to **Smart Docs AI**.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon-Tue | - Study Amazon EventBridge Scheduled Rules <br> - Design the mechanism to auto-delete Cognito users stuck in `UNCONFIRMED` status after 5 minutes | 13/07/2026 | 14/07/2026 | |
| Wed | - Implement the EventBridge rule (`rate(1 minute)`) that triggers the Lambda function <br> - Branch the Lambda handler on `event.source == "aws.events"` to run `cleanup_unconfirmed_users()`, using `list_users(Filter=...)`, comparing `UserCreateDate`, and calling `admin_delete_user` | 15/07/2026 | 15/07/2026 | |
| Thu | - Test the cleanup end-to-end (create an unconfirmed user, confirm it's auto-deleted after ~6 minutes) <br> - Check the cost impact (essentially $0, within Free Tier) | 16/07/2026 | 16/07/2026 | |
| Fri | - Research and configure Google as an Identity Provider on the Cognito User Pool <br> - Design the OAuth redirect flow | 17/07/2026 | 17/07/2026 | |
| Sat | - Build the frontend Google login flow (`cognitoOAuth.js`, `GoogleCallbackPage.jsx`): handle the redirect, exchange the authorization code for tokens <br> - Test signing in with Google end-to-end | 18/07/2026 | 18/07/2026 | |


### Week 4 Achievements:

* Shipped an EventBridge Scheduled Rule that auto-cleans up unconfirmed Cognito users after 5 minutes, verified with a real test run; cost impact is essentially $0.
* Added "Sign in with Google" to **Smart Docs AI**, integrating a Cognito Google Identity Provider and the OAuth redirect flow on the frontend.
