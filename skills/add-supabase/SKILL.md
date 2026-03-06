---
name: add-supabase
description: "Connects NanoClaw to Supabase for persistent data storage. Creates task tracking, project logs, and skill analytics tables. Auto-generates RLS policies for security. Modifies src/db.ts to add Supabase client alongside existing SQLite. Use when you want persistent cross-device data, analytics dashboards, or to query your agent's activity from anywhere."
---

# add-supabase

Adds Supabase persistent storage to NanoClaw — task tracking, project logs, skill analytics.

## Usage

```
/add-supabase
```

## What Gets Created in Supabase

### Tables (auto-created with RLS)

```sql
-- Task tracking
create table tasks (
  id uuid default gen_random_uuid() primary key,
  group_name text not null,
  task text not null,
  status text default 'pending',
  created_at timestamptz default now(),
  completed_at timestamptz
);

-- Agent activity logs
create table activity_log (
  id uuid default gen_random_uuid() primary key,
  group_name text,
  channel text,
  message_preview text,
  model text,
  tokens_used int,
  cost_usd numeric(10,6),
  created_at timestamptz default now()
);

-- Skill usage analytics
create table skill_usage (
  id uuid default gen_random_uuid() primary key,
  skill_name text not null,
  invocation_count int default 0,
  last_used timestamptz,
  group_name text
);
```

### RLS Policies (auto-applied)
```sql
-- Only your authenticated user can read/write
alter table tasks enable row level security;
create policy "owner only" on tasks
  using (auth.uid() = '${your_user_id}');
```

## Files Modified

```
src/db.ts         # Add Supabase client, export helper functions
src/index.ts      # Log activity to Supabase on each message
package.json      # Add @supabase/supabase-js
.env              # Add SUPABASE_URL, SUPABASE_ANON_KEY
```

## Configuration

```
SUPABASE_URL=https://yourproject.supabase.co
SUPABASE_ANON_KEY=your_anon_key
```

## What You Can Do After

- Query all agent activity from Supabase Studio
- Build dashboards showing cost per group, messages per day
- Track which skills get used most
- Share task lists across devices (your phone + laptop both see same tasks)
- Export logs for analysis
