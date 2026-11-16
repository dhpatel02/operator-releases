# Operator

[![Latest release](https://img.shields.io/github/v/release/dhpatel02/operator-releases?label=release)](https://github.com/dhpatel02/operator-releases/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/dhpatel02/operator-releases/total)](https://github.com/dhpatel02/operator-releases/releases)
![Platform: macOS](https://img.shields.io/badge/platform-macOS%20(Apple%20Silicon)-lightgrey)

Operator is a native Mac app for looking into MongoDB and Oracle Autonomous JSON Database
(through Oracle's Database API for MongoDB). Browse databases and collections, query them in a
mongosh-style shell or in SQL, explain queries, and watch what the server is doing. Connections
open read-only.

This repo holds the downloads only. No source code lives here.

- [Download and install](#download-and-install)
- [Quick start](#quick-start)
- [Features](#features)
- [Oracle Autonomous JSON Database](#oracle-autonomous-json-database)
- [Keyboard shortcuts](#keyboard-shortcuts)
- [Your data](#your-data)
- [Updates](#updates)

## Download and install

**Latest version:** https://github.com/dhpatel02/operator-releases/releases/latest

Operator runs on macOS 13 or later, on a Mac with Apple Silicon (M1 or later).

1. Download `Operator-X.Y.Z-arm64.dmg`, open it, and drag **Operator** to **Applications**.
2. The app is not notarized, so macOS blocks the first launch once:
   - **macOS 15 or later:** open Operator and dismiss the warning. Then open
     **System Settings → Privacy & Security**, click **Open Anyway** next to the Operator
     message, and confirm.
   - **macOS 13 and 14:** right-click Operator in Applications, choose **Open**, then **Open**.

After that, Operator opens like any other app and updates itself.

## Quick start

1. Click **+** in the sidebar, or choose **File → New Connection…**.
2. Paste a connection string such as `mongodb://user@db.example.com:27017/app`. Type the
   password in the **Password** field: it is hidden as you type, and Operator fills it into the
   connection string for you. A pasted string with a password in it has the password moved
   there.
3. Click **Connect**. To keep the connection, click **Save**: its connection string goes to
   your Mac's Keychain.
4. Click a collection in the sidebar. Its documents open in a tab, with the query at the top:
   change the `find(…)` and press ⌘⏎ to run it.
5. Press ⌘T for a shell on the connection's database. A SQL shell (**File → New SQL Shell**)
   is there too, for Oracle.

## Features

- **Sidebar:** saved connections in folders, each with a color, and the open connections with
  their databases and collections. ⌘K searches every open connection's collections.
- **Collection tab:**
  - **Documents** as cards, a table, JSON or a key/value tree, paged from the server.
  - **Aggregations:** build a pipeline stage by stage and see each stage's output.
  - **Indexes**, **Schema** (sampled fields and types, with a JSON Schema to save),
    **Explain** (the plan, and whether an index is used), and **Validation** rules.
  - Right-click a value to copy it, or to filter by it.
  - **Export** a collection as JSON or CSV, or the query as Java, Python, Node.js or C# code.
- **Shell:** a mongosh-style JavaScript editor with completions for the shell's methods,
  operators, collection names and field names. ⌘⏎ runs the statement at the caret, ⇧⌘⏎ runs
  them all, and each result gets a tab of its own.
- **Read-only by default:** while a connection is read-only, the shell refuses anything that
  writes before it reaches the server. Change the default in **Settings**.
- **Monitor tab:** what the server is running, its operation counters and storage, and slow
  operations.
- Light and dark appearance, as the system is or as you choose in **Settings**.

## Oracle Autonomous JSON Database

Operator reads AJD through Oracle's Database API for MongoDB. The connection string needs
`authMechanism=PLAIN&authSource=$external&tls=true&loadBalanced=true`. A string with
`$external` in its path (`…/$external?…`), as Oracle's samples give it, works too.

On AJD, Operator adds what the MongoDB API does not show:

- An **Oracle** tab per connection: the database version and your privileges, collections with
  their row counts and sizes, duality views, relational tables and views, vector search, and
  slow SQL from SQL Monitor.
- In a collection: indexes from Oracle's dictionary, the schema from JSON Data Guide, and in
  Explain the SQL Oracle generated, its plan and a SQL Monitor report.
- A **SQL shell**, which runs only `SELECT` queries while the connection is read-only, and a
  **Monitor** tab built on SQL Monitor.

Some features need privileges your database user may not have. The pane then shows Oracle's
error, which names what is missing.

## Keyboard shortcuts

| Shortcut | Action |
|---|---|
| ⌘⏎ | Run the statement at the caret |
| ⇧⌘⏎ | Run every statement |
| ⌘R | Run again |
| Esc | Stop a running query |
| ⌘F / ⌘G | Find in the results / the next match |
| ⌘T | New shell |
| ⌘W | Close the tab |
| ⇧⌘[ / ⇧⌘] | Previous / next tab |
| ⌘1 – ⌘9 | Go to a tab |
| ⌘K | Command bar: find a collection or a tab |

**Settings** lists the shortcuts too.

## Your data

- Connection strings, which hold passwords, are kept in your Mac's **Keychain**, never in a
  file.
- Saved connection names, folders, settings and shell history are in
  `~/Library/Application Support/app.operator.desktop/`.
- Operator connects only to the databases you enter, and to this repo on GitHub to check for
  updates. It has no usage tracking.

## Updates

Operator checks this repo for a newer version once a day and asks before it installs one. To
check now, open **Settings** and click **Check for Updates…**.
