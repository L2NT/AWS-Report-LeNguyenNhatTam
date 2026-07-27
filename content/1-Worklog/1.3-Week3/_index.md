---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
### Week 3 Objectives:

* Build a proper user profile creation flow tied to email verification, avoiding leftover data for unconfirmed accounts.
* Track down and fix a batch of bugs in the RAG pipeline and profile handling in **Smart Docs AI**.
* Attend the "Cloud Architect x Meet Up" community event.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon-Tue | - Redesign the registration/verification flow: only create the DynamoDB profile **after** the user confirms their email (`sign_up` → `UNCONFIRMED` → `confirm-signup` → `admin_get_user` → create profile) <br> - Add `ensure_user_profile()` as a self-healing check on `GET /api/profile` | 06/07/2026 | 07/07/2026 | |
| Wed | - Fix the multi-tenancy data leak: FAISS vector store path → `vectorstore/{user_id}/...`, S3 path → `uploads/{user_id}/{filename}`, removed the unsafe module-level global state | 08/07/2026 | 08/07/2026 | |
| Thu | - Fix session tokens mixing across browser tabs (`localStorage` → `sessionStorage`, explicit `Storage` param on `CognitoUser`) <br> - Fix duplicate FAISS document IDs on the 2nd+ file upload (reset ids to `None` before `FAISS.from_documents()`) | 09/07/2026 | 09/07/2026 | |
| Fri | - Fix CORS masking real 500 errors (added a global `exception_handler(Exception)`) <br> - Fix the file filter being ignored in Self-RAG/Co-RAG (added a `file_filter` param) <br> - Fix chat history duplication on follow-up questions | 10/07/2026 | 10/07/2026 | |
| Sat | - Fix the profile update 400 error (use email instead of `sub` as the Cognito Username) <br> - Attend the "Cloud Architect x Meet Up" event | 11/07/2026 | 11/07/2026 | |


### Week 3 Achievements:

* Shipped the new profile creation flow: DynamoDB only stores a profile after the user verifies their email, avoiding orphaned "unconfirmed" user records, with a self-healing check (`ensure_user_profile`) for race conditions.
* Fully fixed the multi-tenancy data leak between users by properly isolating both the FAISS vector store and S3 by `user_id`.
* Fixed the cross-tab session token mixing bug and the duplicate document ID bug on multi-file uploads.
* Fixed CORS masking real 500 errors, making backend debugging far easier.
* Fixed the ignored file filter in Self-RAG/Co-RAG and the chat history duplication bug on follow-up questions.
* Fixed the profile update 400 error caused by using the wrong user identifier.
* Attended the "Cloud Architect x Meet Up" event (11/07/2026) - see section 4.1 for details.
