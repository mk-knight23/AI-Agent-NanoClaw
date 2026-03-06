---
name: add-gmail
description: "Transforms NanoClaw to add Gmail monitoring and composition. Installs the googleapis dependency, creates a Gmail channel adapter in src/channels/, adds OAuth2 flow, and registers it at startup. Run /add-gmail when you want to monitor your inbox and compose AI-drafted replies via NanoClaw. Requires Google OAuth2 credentials from Google Cloud Console."
---

# add-gmail

Adds Gmail integration to your NanoClaw fork: inbox monitoring, thread routing, and Claude-drafted reply composition with approval workflow.

## Usage

```
/add-gmail
```

## What This Skill Does To Your Codebase

### Files Created
```
src/channels/gmail.ts           # Gmail channel adapter using googleapis
src/channels/gmail-oauth.ts     # OAuth2 PKCE flow handler
```

### Files Modified
```
src/index.ts                    # Import + register GmailChannel at startup
src/config.ts                   # Add GMAIL_CLIENT_ID, GMAIL_CLIENT_SECRET, GMAIL_REDIRECT_URI
package.json                    # Add 'googleapis' dependency
```

### Environment Variables Added
```
GMAIL_CLIENT_ID=your_client_id
GMAIL_CLIENT_SECRET=your_client_secret
GMAIL_REDIRECT_URI=http://localhost:3000/oauth/callback
GMAIL_REFRESH_TOKEN=obtained_after_first_auth
```

## Step-by-Step What Happens

1. **Create credentials**: Instructions to create OAuth2 app in Google Cloud Console
2. **Install dependency**: `npm install googleapis`
3. **Create OAuth handler**: `src/channels/gmail-oauth.ts` — handles the consent flow and stores refresh token
4. **Create adapter**: `src/channels/gmail.ts` — polls inbox, routes threads to orchestrator, composes replies
5. **Approval workflow**: Claude drafts reply → NanoClaw sends you a preview → you approve/reject before sending
6. **Register at startup**: Adds `new GmailChannel(config.gmail)` in `src/index.ts`

## The Resulting Gmail Adapter

```typescript
// src/channels/gmail.ts (generated)
import { google } from 'googleapis';

export class GmailChannel {
  private gmail;

  constructor(private config: { clientId: string; clientSecret: string; refreshToken: string }) {
    const auth = new google.auth.OAuth2(config.clientId, config.clientSecret);
    auth.setCredentials({ refresh_token: config.refreshToken });
    this.gmail = google.gmail({ version: 'v1', auth });
  }

  async pollInbox(onThread: (subject: string, body: string, reply: (r: string) => Promise<void>) => void) {
    // Poll unread threads, route to Claude, surface drafts for approval
  }
}
```

## Philosophy

Inbox as an async message channel. Every unread thread becomes a task that NanoClaw can reason about, draft a reply for, and send — with your approval.
