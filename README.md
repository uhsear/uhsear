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

**Twelve need an Esri library to run** (`arcpy` or the `arcgis` Python API): agol-relink,
arcade-rule-deploy, arcpy-nullscan, fcload, fcpatch, fullpull, gdbprune, hostedreap,
safe-republish, sightline, svcdrift, whowrites, xydrift.

Ten of those twelve still run their self-test without one, because the import is deferred
until the tool actually reaches a geodatabase or a portal. Three do not: `fullpull` and
`sightline` need their library present even to self-test, and `arcpy-nullscan` is an
older script with no self-test at all.

The other thirty are standard library only and run anywhere Python 3 does. That
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
| [**ghostsvc**](https://github.com/uhsear/ghostsvc) | Services the server runs but the portal never registered. They answer anonymously and appear in no sharing report. |

### Geodatabase

| | |
|---|---|
| [**safe-republish**](https://github.com/uhsear/safe-republish) | Refuse to truncate a feature class when the staged replacement fails a plausibility check. |
| [**fcload**](https://github.com/uhsear/fcload) | Load a dataset into a geodatabase, refusing the imports that corrupt silently. |
| [**gdbxray**](https://github.com/uhsear/gdbxray) | Print the schema `ogrinfo` will not show you: subtypes, attribute rules, attachment linkage. |
| [**gdbprune**](https://github.com/uhsear/gdbprune) | Delete stale leaf versions from a versioned Enterprise geodatabase, printing the plan first. |
| [**arcade-rule-deploy**](https://github.com/uhsear/arcade-rule-deploy) | Deploy Arcade attribute rules, preflight-checked and idempotent. Resolves every `FeatureSetByName` before writing. |
| [**arcadecheck**](https://github.com/uhsear/arcadecheck) | Inventory every Arcade expression you own and say which ones can leave with you. |

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

---

**Start here if you are browsing:** [safe-republish](https://github.com/uhsear/safe-republish)
is the shortest example of the idea. It refuses a truncate-and-append when the replacement data
is not believable, because the row count people check first is the one that misses a 37 percent
loss on a large layer.
