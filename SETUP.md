# Supabase + GitHub Pages Setup

## 1. Create a Supabase project

1. Go to [supabase.com](https://supabase.com) and sign in
2. Click **New project**, pick a name, set a database password, choose a region
3. Wait ~2 minutes for it to provision

## 2. Get your credentials

1. In your project go to **Settings → API**
2. Copy the **Project URL** and the **anon public** key
3. Open `index.html` and replace the two placeholders near the top of the `<script>` block:

```js
const SUPABASE_URL = 'https://xxxxxxxxxxxx.supabase.co';
const SUPABASE_ANON_KEY = 'eyJ...';
```

The anon key is safe to commit — it's designed to be public. Row Level Security keeps each user's data private.

## 3. Create the database table

In your Supabase project go to **SQL Editor → New query**, paste and run:

```sql
CREATE TABLE logs (
  id          text PRIMARY KEY,
  user_id     uuid REFERENCES auth.users ON DELETE CASCADE NOT NULL,
  meal_name   text NOT NULL,
  meal_time   timestamptz,
  discomfort  int DEFAULT 0,
  symptoms    text[],
  source      text,
  triggers    text[],
  meal_type   text,
  notes       text,
  timing      text,
  bowel       text,
  stress      text,
  created_at  timestamptz DEFAULT now()
);

ALTER TABLE logs ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Users manage own logs" ON logs
  FOR ALL
  USING (auth.uid() = user_id)
  WITH CHECK (auth.uid() = user_id);
```

## 4. Configure authentication

### Disable email confirmation (recommended for friends)

By default Supabase requires users to click a confirmation email before they can log in. For a private friend group you can skip this:

1. Go to **Authentication → Settings**
2. Turn off **Enable email confirmations**

### Set your site URL (required for GitHub Pages)

1. Go to **Authentication → URL Configuration**
2. Set **Site URL** to your GitHub Pages URL, e.g. `https://yourusername.github.io/Gut-Feeling/`
3. Add the same URL to **Redirect URLs**

## 5. Deploy to GitHub Pages

1. Make sure `index.html` is at the root of your repo (it already is)
2. Push to GitHub
3. In your repo go to **Settings → Pages**
4. Set Source to **Deploy from a branch**, choose `main`, folder `/` (root)
5. Your app will be live at `https://yourusername.github.io/Gut-Feeling/`

## 6. Share with friends

Send them the GitHub Pages URL. They can sign up with any email and password — their data is completely separate from yours.
