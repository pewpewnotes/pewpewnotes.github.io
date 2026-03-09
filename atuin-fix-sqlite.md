# Atuin SQLite Database Recovery Guide

This document describes how to recover an **Atuin history database** when SQLite reports:

```
database disk image is malformed
```

This usually means the SQLite database was corrupted due to:
- system crash
- suspend/resume interruption
- process killed during write
- disk or filesystem issues

The goal is to **salvage as much history as possible**.

---

# 1. Locate the Atuin Database

Atuin stores its databases here:

```
~/.local/share/atuin/
```

Typical contents:

```
history.db
history.db-wal
history.db-shm
recovery.db
```

Where:

| File | Purpose |
|-----|------|
| history.db | main history database |
| history.db-wal | write-ahead log containing recent commits |
| history.db-shm | shared memory file for WAL |
| recovery.db | temporary DB used by atuin |

---

# 2. Disable Atuin Temporarily

Atuin hooks into your shell and will trigger errors every command.

Start a clean shell:

### bash
```
bash --norc
```

### zsh
```
zsh -f
```

Then navigate to the database directory:

```
cd ~/.local/share/atuin
```

---

# 3. Remove Broken Temporary Database

`recovery.db` is safe to delete.

```
rm recovery.db
```

Atuin will recreate it automatically.

---

# 4. Check Database Integrity

Run:

```
sqlite3 history.db "PRAGMA integrity_check;"
```

Expected result:

```
ok
```

If you see errors, the database is corrupted.

---

# 5. Attempt Standard SQLite Recovery

SQLite provides a recovery command that scans raw pages.

```
sqlite3 history.db ".recover" > recovered.sql
```

Then rebuild a new database:

```
sqlite3 rebuilt.db < recovered.sql
```

Replace the old database:

```
mv history.db history.db.broken
mv rebuilt.db history.db
```

---

# 6. Recover WAL Transactions

If the following files exist:

```
history.db-wal
history.db-shm
```

SQLite may still have recent commands stored in the WAL.

Force SQLite to merge them:

```
sqlite3 history.db "PRAGMA wal_checkpoint(FULL);"
```

---

# 7. Dump the Database

If the database opens but has minor corruption:

```
sqlite3 history.db ".dump" > dump.sql
```

Rebuild:

```
sqlite3 rebuilt.db < dump.sql
```

Replace the old file.

---

# 8. Raw Command Extraction (Last Resort)

If the database is severely corrupted, commands may still exist as plain text.

Extract them using:

```
strings history.db | grep -E '.{10,}' > possible_history.txt
```

This will not preserve timestamps but may recover commands.

---

# 9. Restart Atuin

After recovery:

```
atuin search
```

or

```
atuin sync
```

If using sync, the server may restore missing history.

---

# 10. Prevent Future Corruption

SQLite corruption often occurs when a process is interrupted during writes.

Common causes:

- laptop suspend
- sudden shutdown
- shell exiting during writes

Possible mitigations:

- ensure proper system suspend handling
- avoid killing shell processes abruptly
- keep backups of the Atuin directory

Backup example:

```
cp -r ~/.local/share/atuin ~/atuin-backup
```

---

# End