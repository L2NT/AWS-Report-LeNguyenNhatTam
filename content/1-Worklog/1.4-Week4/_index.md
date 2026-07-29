---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
### Week 4 Objectives:

* Implement the registration/verification flow redesign and the `ensure_user_profile()` self-healing check drafted last week.
* Fix the multi-tenancy data leak, session token mixing, and the other bugs identified last week.
* Automate cleanup of unconfirmed Cognito accounts with Amazon EventBridge.
* Add "Sign in with Google" to **Smart Docs AI**.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon-Tue | - Implement the registration/verification flow redesign: only create the DynamoDB profile **after** the user confirms their email (`sign_up` → `UNCONFIRMED` → `confirm-signup` → `admin_get_user` → create profile) <br> - Add `ensure_user_profile()` as a self-healing check on `GET /api/profile` <br> - Build the profile display + change-password page | 13/07/2026 | 14/07/2026 | |
| Wed | - Fix the multi-tenancy data leak: FAISS vector store path → `vectorstore/{user_id}/...`, S3 path → `uploads/{user_id}/{filename}`, removed the unsafe module-level global state <br> - Fix session tokens mixing across browser tabs (`localStorage` → `sessionStorage`, explicit `Storage` param on `CognitoUser`) <br> - Removed test endpoints and completed local testing infrastructure for all profile endpoints <br> - Drafted Blog 3 ("Lambda Tenant Isolation Mode") while fixing the multi-tenancy bug | 15/07/2026 | 15/07/2026 | |
| Thu | - Fix the profile update 400 error (use email instead of `sub` as the Cognito Username) <br> - Fix CORS masking real 500 errors (added a global `exception_handler(Exception)`), the ignored file filter in Self-RAG/Co-RAG, and chat history duplication on follow-up questions <br> - Study Amazon EventBridge Scheduled Rules and implement the EventBridge rule (`rate(1 minute)`) that triggers the Lambda's `cleanup_unconfirmed_users()`, tested end-to-end (create an unconfirmed user, confirm it's auto-deleted after ~6 minutes; cost impact essentially $0) <br> - Drafted Blog 1 ("EventBridge Scheduler vs Rule") while implementing the cleanup rule | 16/07/2026 | 16/07/2026 | |
| Fri | - Research and configure Google as an Identity Provider on the Cognito User Pool <br> - Design the OAuth redirect flow | 17/07/2026 | 17/07/2026 | |
| Sat | - Build the frontend Google login flow (`cognitoOAuth.js`, `GoogleCallbackPage.jsx`): handle the redirect, exchange the authorization code for tokens <br> - Fix Google account-linking edge cases (email collision with an existing native Cognito user) <br> - Test signing in with Google end-to-end | 18/07/2026 | 18/07/2026 | |


### Week 4 Achievements:

* Shipped the new profile creation flow: DynamoDB only stores a profile after the user verifies their email, avoiding orphaned "unconfirmed" user records, with a self-healing check (`ensure_user_profile`) for race conditions.
* Fully fixed the multi-tenancy data leak between users by properly isolating both the FAISS vector store and S3 by `user_id`, and fixed the cross-tab session token mixing bug.
* Fixed the profile update 400 error, the CORS bug masking real 500 errors, the ignored file filter in Self-RAG/Co-RAG, and the chat history duplication bug on follow-up questions.
* Shipped an EventBridge Scheduled Rule that auto-cleans up unconfirmed Cognito users after 5 minutes, verified with a real test run; cost impact is essentially $0.
* Added "Sign in with Google" to **Smart Docs AI**, integrating a Cognito Google Identity Provider, the OAuth redirect flow on the frontend, and account-linking for matching native/Google accounts.
* Drafted Blog 3 ("Lambda Tenant Isolation Mode: does this new feature solve multi-tenant data leak bugs?") and Blog 1 ("EventBridge Scheduler: when should you 'upgrade' from EventBridge Rule?") - see sections 3.3 and 3.1.
