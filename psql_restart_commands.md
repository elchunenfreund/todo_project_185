````markdown
# Quick PostgreSQL Restart Commands (macOS + Homebrew)

Keep this cheat sheet handy for restarting your Postgres server under your user account without losing data.

---

## 1. Stop any running instances

```bash
# Stop the Homebrew service
brew services stop postgresql@14

# Kill stray processes (if needed)
killall -9 postgres || true
````

## 2. Clean up stale state

```bash
# Remove stale lock file
rm "$(brew --prefix)/var/postgresql@14/postmaster.pid" || true

# Prune old service entries
brew services cleanup
```

## 3. (Re)install service definition

```bash
# Reinstall PostgreSQL to restore plist
brew reinstall postgresql@14
```

## 4. Start the service under your user

```bash
brew services start postgresql@14
```

## 5. Manual start alternative

If `brew services` gives errors, start Postgres manually:

```bash
pg_ctl -D "$(brew --prefix)/var/postgresql@14" start
```

## 6. Verify status

```bash
# List services
brew services list

# Confirm processes
ps aux | grep '[p]ostgres'

# Check socket
ls /tmp/.s.PGSQL.5432

# List databases
psql -l
```

---

> **Tip:** Never use `sudo` with `brew services`. Always run as your normal user to keep plists and sockets consistent.

```
```
