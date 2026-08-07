# Mise en place du multi-compte (à faire une fois)

Ces étapes activent la connexion par compte et l'isolation des données.
**Tant qu'elles ne sont pas faites, ne pas mettre le code multi-compte en ligne**
(l'app actuelle sans connexion cesserait de fonctionner une fois RLS activé).

## 1) Auth — désactiver la confirmation d'e-mail
Dashboard Supabase → **Authentication** → **Sign In / Providers** → **Email** →
mettre **« Confirm email » sur OFF** → Save.
(Sinon chaque inscription attend un e-mail de confirmation, peu fiable en offre gratuite.)

## 2) SQL — isolation par utilisateur
**SQL Editor** → coller → **Run** :

```sql
-- ===== GAMES =====
alter table public.games
  add column if not exists user_id uuid references auth.users(id) default auth.uid();

alter table public.games enable row level security;
drop policy if exists games_own on public.games;
create policy games_own on public.games
  for all using (auth.uid() = user_id) with check (auth.uid() = user_id);

-- ===== FLASHCARD_STATUS (clé par utilisateur) =====
alter table public.flashcard_status
  add column if not exists user_id uuid references auth.users(id) default auth.uid();

-- refais la clé primaire sur (user_id, card_id)
alter table public.flashcard_status drop constraint if exists flashcard_status_pkey;
alter table public.flashcard_status add primary key (user_id, card_id);

alter table public.flashcard_status enable row level security;
drop policy if exists fs_own on public.flashcard_status;
create policy fs_own on public.flashcard_status
  for all using (auth.uid() = user_id) with check (auth.uid() = user_id);
```

> Si `flashcard_status` a une clé primaire nommée autrement que
> `flashcard_status_pkey`, adapte le nom (Table editor → la table → Constraints).

## 3) Rattacher TES données existantes à ton compte (optionnel mais recommandé)
1. Inscris-toi d'abord dans l'app (ça crée ton compte).
2. Récupère ton identifiant :
   ```sql
   select id, email from auth.users order by created_at;
   ```
3. Remplace `TON-UUID` puis Run :
   ```sql
   update public.games            set user_id = 'TON-UUID' where user_id is null;
   update public.flashcard_status set user_id = 'TON-UUID' where user_id is null;
   ```

## 4) Backup — ajouter la clé service_role
Une fois RLS activé, la clé anon ne lit plus les tables. Il faut la clé service_role :
- Dashboard → **Project Settings → API** → copie la clé **`service_role`** (secrète).
- GitHub → repo **lab** → **Settings → Secrets and variables → Actions → New repository secret** :
  - **Name** : `SUPABASE_SERVICE_ROLE`
  - **Value** : (la clé service_role)

Le workflow de backup l'utilisera automatiquement (repli sur anon sinon).

## 5) Mise en ligne
Quand 1, 2 (et idéalement 3, 4) sont faits : dis-le-moi, je merge le code multi-compte
et c'est en ligne. On teste ensemble une inscription + connexion.
