## Asir Khan

GIS developer for a Florida county. I write small, single-purpose Python tools for
ArcGIS shops, and most of them exist to refuse something.

Every repository here follows the same shape: one Python file, one README, MIT. Each
one guards a specific production failure I have watched happen. Destructive operations
are dry-run by default. Every tool carries a `--self-test` that runs with no ArcGIS, no
network and no database, so you can check it before you trust it:

```
python <tool>.py --self-test
```

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

### Geodatabase

| | |
|---|---|
| [**safe-republish**](https://github.com/uhsear/safe-republish) | Refuse to truncate a feature class when the staged replacement fails a plausibility check. |
| [**fcload**](https://github.com/uhsear/fcload) | Load a dataset into a geodatabase, refusing the imports that corrupt silently. |
| [**gdbxray**](https://github.com/uhsear/gdbxray) | Print the schema `ogrinfo` will not show you: subtypes, attribute rules, attachment linkage. |
| [**gdbprune**](https://github.com/uhsear/gdbprune) | Delete stale leaf versions from a versioned Enterprise geodatabase, printing the plan first. |
| [**arcade-rule-deploy**](https://github.com/uhsear/arcade-rule-deploy) | Deploy Arcade attribute rules, preflight-checked and idempotent. Resolves every `FeatureSetByName` before writing. |

### Data quality

| | |
|---|---|
| [**geocodesift**](https://github.com/uhsear/geocodesift) | Audit a geocoded batch instead of believing its match rate. A ZIP-centroid fallback still scores 98. |
| [**tzrot**](https://github.com/uhsear/tzrot) | Find date fields reinterpreted as UTC, and count the records whose calendar day moved. |
| [**roadmiles**](https://github.com/uhsear/roadmiles) | Certify centerline mileage and refuse to count the same road twice, including the copy digitized backwards. |
| [**arcpy-nullscan**](https://github.com/uhsear/arcpy-nullscan) | Report NULL and blank values across every layer and standalone table in a map, including null geometry. |

### Developer tooling

| | |
|---|---|
| [**restfake**](https://github.com/uhsear/restfake) | A mock ArcGIS REST server that fails the way ArcGIS actually fails: 200 OK with an error body. |
| [**pytlint**](https://github.com/uhsear/pytlint) | Static analysis for Python toolboxes. Never imports the file it checks. |
| [**cimscan**](https://github.com/uhsear/cimscan) | Report every data source in a tree of `.aprx` and `.lyrx` files with no ArcGIS licence. |
| [**gdbfence**](https://github.com/uhsear/gdbfence) | Refuse the commit that puts a geodatabase, or a shapefile missing its `.prj`, into git. |
| [**jobharness**](https://github.com/uhsear/jobharness) | One import gives a scheduled script logging, retry, resume and a safe unzip. Standard library only. |

### Operations

| | |
|---|---|
| [**svcguard**](https://github.com/uhsear/svcguard) | Guarantee an ArcGIS Server service restarts around risky maintenance, even on failure. |
| [**taskpulse**](https://github.com/uhsear/taskpulse) | Audit every Windows scheduled task and report which ones are silently failing. |

---

**Start here if you are browsing:** [safe-republish](https://github.com/uhsear/safe-republish)
is the shortest example of the idea. It refuses a truncate-and-append when the replacement data
is not believable, because the row count people check first is the one that misses a 37 percent
loss on a large layer.
