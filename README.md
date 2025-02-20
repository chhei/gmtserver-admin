# GMT Data Server Administration

Cache data and scripts for managing the GMT data server

Current master server is: **gmtserver.soest.hawaii.edu**, in directory `/export/gmtserver/gmt/data`

The actual URL is: **www.soest.hawaii.edu/gmt/data** [you cannot browse there]

Master data server URL: **https://oceania.generic-mapping-tools.org**

To clone this repo you can run

```
git clone https://github.com/GenericMappingTools/gmtserver-admin
```

## Cache files

GMT Core developers can add, modify or remove cache files from their working copy
of the gmtserver-admin repo, and after merging the gmt server will automatically
update its working copy via the crontab script, and if there are changes the key
`gmt_hash_server.txt` and `gmt_data_server.txt` files will be rebuilt as needed.

## Global grids

For now, the earth_relief_xxy.grd files are maintained and updated manually.
Changes to these need to be followed by a manual run of `srv_update_sha256.sh`.
The production of global grids are based on recipes in the recipes folder.
These recipes are given to script `srv_downsampler.sh` which produces a new
set of grids in the staging directory.  If these are satisfactory they can
be moved to the top data directory.

## Crontab

The working directory on the gmtserver is updated once an hour via a
crontab script running under local account pwessel with this crontab entry:

```
0 * * * *      /export/gmtserver/gmt/gmtserver-admin/scripts/srv_git_update.sh > /export/gmtserver/gmt/LOGS/git_update.cron.log 2>&1
```
