# mtdat
A MATLAB package for saving a structured binary data stream having a fixed record size/layout but unspecified length. MTDAT is intended as a real-time data-stream saved to the disk by the control software of an instrument. Data within the files is written using the low-level fwrite routines, so writing does not require a significant amount of processsing time. Moreover, the record structure is specified when the file is initialized, so the data stream can be interrupted (by a power-outage for example) and the previously written data will be unaffected.
## Including MTDAT in a project
MTDAT should be included in a MATLAB project as a package named "+mtdat". You can add it to an existing git repository using a subtree.
```
...In you git repository directory...
# Create a remote connection to MTDAT
git remote add -f mtdat https://github.com/dkovari/mtdat/

#Merge into local project
git merge -s ours --no-commit --allow-unrelated-histories mtdat/master

# Copy MATextras into project in a directory named +extras
git read-tree --prefix=+mtdat/ -u mtdat/master

# Commit the changes
git commit -m "Subtree merged mtdat to +mtdat"
```
To update the subtree to use the latest commit you need to manually pull changes.
```
git pull -s subtree mtdat master
```
## Usage

