## Asir Khan

GIS developer for a Florida county. I write scripts and tools for everyone to use, and
increasingly for people working within the GIS community.

They are single-file Python, MIT licensed. Each one guards a specific production
failure I have watched happen, and the README opens by describing that failure rather
than the feature list. Anything destructive is dry-run by default and needs `--apply`.

Most carry a `--self-test` you can run before trusting the tool:

```
python <tool>.py --self-test
```

**Thirteen need an Esri library to run** (`arcpy` or the `arcgis` Python API): agol-relink,
arcade-rule-deploy, arcpy-nullscan, fcload, fcpatch, fullpull, gdbprune, hostedreap,
safe-republish, sightline, svcdrift, whowrites, xydrift.

Three of them also have a read-only mode that needs no Esri library: `fcload check`
reads a shapefile's header and `.prj`, `gdbprune --from-versions` reads an exported version
list, and `xydrift --from-geojson` reads GeoJSON.

Ten of those thirteen still run their self-test without one, because the import is deferred
until the tool actually reaches a geodatabase or a portal. Three do not: `fullpull` and
`sightline` need their library present even to self-test, and `arcpy-nullscan` is an
older script with no self-test at all.

The other fifty-five are standard library only and run anywhere Python 3 does. That
includes two that read Esri formats without Esri software: `cimscan` parses `.aprx` and
`.lyrx` with no ArcGIS installed, and `gdbxray` reads a geodatabase schema through GDAL.

---

### ArcGIS Online and Enterprise

| | |
|---|---|
| [**itemcensus**](https://github.com/uhsear/itemcensus) | Inventory every item in an organization, and refuse to report a total the server cannot prove is complete. Search counts accurately only to 10,000. |
| [**sharewatch**](https://github.com/uhsear/sharewatch) | Diff your sharing posture against yesterday, because the platform keeps no audit log. Read-only. |
| [**sightline**](https://github.com/uhsear/sightline) | Audit web maps for layers their viewers cannot see. Broken sharing, dead services, public maps pointing at secured data. |
| [**agol-relink**](https://github.com/uhsear/agol-relink) | Bulk-replace REST service URLs across Portal content, including the StoryMap and Experience Builder drafts other tools miss. |
| [**hostedreap**](https://github.com/uhsear/hostedreap) | Delete hosted feature layer rows that no longer exist in your source. Backup first, dry run by default. |
| [**fullpull**](https://github.com/uhsear/fullpull) | Download every layer of a REST service into a File Geodatabase, verified against the server's own record count. |
| [**whobreaks**](https://github.com/uhsear/whobreaks) | Every item referencing the one you are about to delete, including the Experience Builder drafts a dependency graph never opens. |
| [**deadwidget**](https://github.com/uhsear/deadwidget) | Find the Experience Builder widgets bound to a layer that no longer exists. The app loads fine and the widget does nothing. |
| [**ghostsvc**](https://github.com/uhsear/ghostsvc) | Services the server runs but the portal never registered. They answer anonymously and appear in no sharing report. |
| [**itemvault**](https://github.com/uhsear/itemvault) | Restore an item's configuration from a snapshot, and refuse to overwrite an edit that no snapshot holds. |
| [**sdcheck**](https://github.com/uhsear/sdcheck) | Read a staged service definition before you publish it, and flag a raw host name or a copied dataset inside it. |
| [**locdiff**](https://github.com/uhsear/locdiff) | Diff two locator files and fail when the rebuild lost a matching setting, such as "Match with no zones". |
| [**exbtwin**](https://github.com/uhsear/exbtwin) | Write an Experience Builder fix to both of the app's config surfaces, refuse when either is not what you expect, and read both back. |
| [**rendergap**](https://github.com/uhsear/rendergap) | Count the rows a unique-value renderer draws with a `<Null>` class, or with no class and no default symbol. |
| [**formwatch**](https://github.com/uhsear/formwatch) | Tell a broken Survey123 form from a quiet one. Refuses to judge a seasonal form in its first year. |
| [**stalled**](https://github.com/uhsear/stalled) | Count the days since a scheduled notebook or webhook last succeeded, and say so when the count is too high. |

### Geodatabase

| | |
|---|---|
| [**safe-republish**](https://github.com/uhsear/safe-republish) | Refuse to truncate a feature class when the staged replacement fails a plausibility check. |
| [**fcload**](https://github.com/uhsear/fcload) | Load a dataset into a geodatabase, refusing the imports that corrupt silently. |
| [**gdbxray**](https://github.com/uhsear/gdbxray) | Print the schema `ogrinfo` will not show you: subtypes, attribute rules, attachment linkage. |
| [**gdbprune**](https://github.com/uhsear/gdbprune) | Delete stale leaf versions from a versioned Enterprise geodatabase, printing the plan first. |
| [**compressfloor**](https://github.com/uhsear/compressfloor) | Name what holds a geodatabase's compress floor: a detached replica, a stalled replica, a pinned version or an orphaned state. |
| [**arcade-rule-deploy**](https://github.com/uhsear/arcade-rule-deploy) | Deploy Arcade attribute rules, preflight-checked and idempotent. Resolves every `FeatureSetByName` before writing. |
| [**arcadecheck**](https://github.com/uhsear/arcadecheck) | Inventory every Arcade expression you own and say which ones can leave with you. |
| [**replicakeep**](https://github.com/uhsear/replicakeep) | Plan, then repair under `--apply`, an idle replica that may hold the compress floor. Compress still exits 0. |
| [**reconverify**](https://github.com/uhsear/reconverify) | Verify a no-post reconcile from a fresh read of the state tree, never from the process that ran it. |
| [**xwddiff**](https://github.com/uhsear/xwddiff) | Classify the diff between two XML workspace documents as BREAKING, WIDENING or COSMETIC. |
| [**spidxcheck**](https://github.com/uhsear/spidxcheck) | Compare the spatial index box, the stored extent and the real data envelope, and say which one is wrong. |

### SQL Server behind the geodatabase

These read exported catalog rows, `msdb` rows or script files. Only sqldeploy connects to a server, and only under `--apply`.

| | |
|---|---|
| [**evwlint**](https://github.com/uhsear/evwlint) | Flag the views, procedures, triggers and Agent job steps that read a versioned base table instead of its `_evw` view. |
| [**sdeindex**](https://github.com/uhsear/sdeindex) | Plan or audit an index cleanup. Refuses to drop both copies of an identical pair, or half of an adds and deletes twin. |
| [**bkpbase**](https://github.com/uhsear/bkpbase) | Say whether a restorable full backup exists, refusing snapshot and copy-only rows. |
| [**stepflow**](https://github.com/uhsear/stepflow) | Flag Agent job steps that can never run, watchdogs that find their job by name, and runs far past their normal length. |
| [**sessorigin**](https://github.com/uhsear/sessorigin) | Give a verdict after a database alias flip, and never report MIGRATED while a node still holds old sessions. |
| [**sqlmove**](https://github.com/uhsear/sqlmove) | One read-only verdict on a geodatabase moved to another instance: orphaned users, ownerless jobs, names that no longer resolve. |
| [**wmguard**](https://github.com/uhsear/wmguard) | Flag a sync watermark taken from a table whose MAX froze, or moved past rows nobody applied. |
| [**txnlint**](https://github.com/uhsear/txnlint) | Find the T-SQL transaction mistakes that only show when you read a script across its `GO` batches. |
| [**sqldeploy**](https://github.com/uhsear/sqldeploy) | Preview a T-SQL deploy script one `GO` batch at a time, and run it only on `--apply` after every batch parsed. |

### Data quality

| | |
|---|---|
| [**geocodesift**](https://github.com/uhsear/geocodesift) | Audit a geocoded batch instead of believing its match rate. A ZIP-centroid fallback still scores 98. |
| [**tzrot**](https://github.com/uhsear/tzrot) | Find date fields reinterpreted as UTC, and count the records whose calendar day moved. |
| [**roadmiles**](https://github.com/uhsear/roadmiles) | Certify centerline mileage and refuse to count the same road twice, including the copy digitized backwards. |
| [**arcpy-nullscan**](https://github.com/uhsear/arcpy-nullscan) | Report NULL and blank values across every layer and standalone table in a map, including null geometry. |
| [**ringwind**](https://github.com/uhsear/ringwind) | Name every GeoJSON ring wound against your declared convention. A backwards ring makes point-in-polygon answer backwards. |
| [**sidestamp**](https://github.com/uhsear/sidestamp) | Check what is stamped on each side of a centerline against the polygon that side fronts, and prove the sides are not reversed. |
| [**pl94**](https://github.com/uhsear/pl94) | Read the Census PL 94-171 file for any US county, refusing a block extract that does not reconcile to the county total. |
| [**fcpatch**](https://github.com/uhsear/fcpatch) | Apply reviewed attribute corrections, refusing any row whose current value is no longer the value that was reviewed. |
| [**nalmatch**](https://github.com/uhsear/nalmatch) | Reconcile a parcel layer against the tax roll. Refuses any ID rule that would merge two parcels into one key. |
| [**idreuse**](https://github.com/uhsear/idreuse) | Measure how far apart two rows sharing an ID actually are. A key that matches is not evidence they are the same object. |
| [**xydrift**](https://github.com/uhsear/xydrift) | Name the rows whose stored coordinate columns disagree with their own geometry, and resync only those. |
| [**feedstamp**](https://github.com/uhsear/feedstamp) | Refuse to run the pipeline when the delivery is not a new, complete one. Yesterday's file is still a file. |
| [**svcdrift**](https://github.com/uhsear/svcdrift) | Diff a published service against the dataset it came from, rather than calling two different schemas the same. |
| [**sliverkeep**](https://github.com/uhsear/sliverkeep) | Drop the sliver parts of a polygon layer, but keep every part that holds an address point. |

### Developer tooling

| | |
|---|---|
| [**restfake**](https://github.com/uhsear/restfake) | A mock ArcGIS REST server that fails the way ArcGIS actually fails: 200 OK with an error body. |
| [**pytlint**](https://github.com/uhsear/pytlint) | Static analysis for Python toolboxes. Never imports the file it checks. |
| [**cimscan**](https://github.com/uhsear/cimscan) | Report every data source in a tree of `.aprx` and `.lyrx` files with no ArcGIS licence. |
| [**gdbfence**](https://github.com/uhsear/gdbfence) | Refuse the commit that puts a geodatabase, or a shapefile missing its `.prj`, into git. |
| [**clonedrift**](https://github.com/uhsear/clonedrift) | Name every script on a share that exists in more than one version, and say what the versions disagree about. |
| [**alwayszero**](https://github.com/uhsear/alwayszero) | Name every unattended script that cannot report failure. Task Scheduler has said 0x0 for four years. |
| [**whowrites**](https://github.com/uhsear/whowrites) | Name every script that empties a feature class, and never name a reader as the thing that destroyed it. |
| [**jobharness**](https://github.com/uhsear/jobharness) | One import gives a scheduled script logging, retry, resume and a safe unzip. Standard library only. |
| [**logsift**](https://github.com/uhsear/logsift) | Mine a scheduled job's own logs into metrics, refusing the number that is really a timestamp. |
| [**litswap**](https://github.com/uhsear/litswap) | Rename a string constant across a tree of scripts without touching one comment or docstring. |

### Operations

| | |
|---|---|
| [**svcguard**](https://github.com/uhsear/svcguard) | Guarantee an ArcGIS Server service restarts around risky maintenance, even on failure. |
| [**taskpulse**](https://github.com/uhsear/taskpulse) | Audit every Windows scheduled task and report which ones are silently failing. |
| [**stalehost**](https://github.com/uhsear/stalehost) | Find every file still naming the host you are retiring, and never call a tree clean it could not finish reading. |
| [**svcsource**](https://github.com/uhsear/svcsource) | Report what is behind every service on an ArcGIS Server site, and say which ones it could not resolve. |
| [**prostall**](https://github.com/uhsear/prostall) | Diagnose why ArcGIS Pro is slow here, measure every answer, and never record a crashed probe as a finding. |
| [**nodecheck**](https://github.com/uhsear/nodecheck) | Check install prerequisites from a node table. A requirement nobody could check is UNVERIFIED, never PASS. |
| [**svcparity**](https://github.com/uhsear/svcparity) | Put a service's pool, instance and maxRecordCount settings back after an overwrite publish, and say when it cannot. |
| [**svcsmoke**](https://github.com/uhsear/svcsmoke) | Sample every service repeatedly, state the chance the sampling missed a fault, and pass only on real features or image bytes. |

---

**Start here if you are browsing:** [safe-republish](https://github.com/uhsear/safe-republish)
is the shortest example of the idea. It refuses a truncate-and-append when the replacement data
is not believable, because the row count people check first is the one that misses a 37 percent
loss on a large layer.
