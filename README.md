create table group_messages (
  id uuid default gen_random_uuid() primary key,
  created_at timestamptz default now(),
  group_id text not null,
  content text not null,
  user_id uuid references auth.users(id),
  display_name text
);
alter table group_messages enable row level security;
create policy "Groupe authentifiés" on group_messages for all to authenticated using (true) with check (true);
alter publication supabase_realtime add table group_messages;
