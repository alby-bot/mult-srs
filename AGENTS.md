# MultRace — Agent & Developer Notes

## ⚠️ Read this before making any changes

### Repo structure
- **Single file app**: all code lives in `index.html` — no build tools, no npm, no dependencies
- **Supabase backend**: leaderboard + score submission (see constants at top of JS)

### Branches & Deployment

| Branch | Deploys to | URL |
|--------|-----------|-----|
| `main` | GitHub Pages root | https://alby-bot.github.io/mult-srs/ ← **PRODUCTION** |
| `dev`  | GitHub Pages `/dev/` subfolder | https://alby-bot.github.io/mult-srs/dev/ ← **STAGING** |

**NEVER push untested changes directly to `main`.**

### Workflow
1. All new development goes on the `dev` branch
2. Test at the staging URL before merging
3. When stable: open a PR `dev → main`, merge → auto-deploys to production
4. GitHub Actions handles deployment automatically on every push to either branch
   - Workflow file: `.github/workflows/deploy.yml`

### One-time GitHub Pages setup (already done)
Pages source must be set to **"GitHub Actions"** (not "Deploy from branch") in:
`https://github.com/alby-bot/mult-srs/settings/pages`

### iOS 9 Compatibility Rules (MANDATORY)
The app must run on iPad mini 1st gen (iOS 9.3.5). These are hard constraints:
- ❌ No `async/await` — use callback-based patterns (`setTimeout` chains, XHR.onreadystatechange)
- ❌ No CSS `clamp()` without a px pixel fallback before it
- ❌ No CSS `min()` function
- ❌ No CSS `inset` shorthand — use explicit `top/right/bottom/left`
- ❌ No spread operator (`...arr`) — use `.concat()` or loops
- ❌ No `Math.min(...array)` — use a loop
- ❌ No flexbox `gap` — use `margin` instead
- ✅ Always add `touch-action: manipulation` to interactive elements
- ✅ `user-scalable=no` in viewport meta

### Testing before pushing
Run the Node.js smoke test to catch JS syntax errors and boot crashes:
```bash
node -e "
var fs=require('fs'),html=fs.readFileSync('index.html','utf8');
var s=html.match(/<script>([\s\S]*?)<\/script>/g).pop().replace(/<\/?script>/g,'');
try{new Function(s);console.log('✅ Syntax OK');}catch(e){console.log('❌',e.message);}
"
```

### Storage keys
- `multrace-profiles` — array of player profiles
- `multrace-active-id` — active profile UUID
- Old keys (`multrace-token`, `mult-srs-data`, `mult-srs-cfg`) — legacy, migrated on first boot

### Supabase
- URL: `https://usdwpcgxjlfmaipdcylt.supabase.co`
- RPC: `submit_score()` — token is primary identity (not name)
- Table: `leaderboard`
- Admin access: use service_role key (retrieve via management API with PAT)
