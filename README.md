# mtdat
A MATLAB package for saving a structured binary data stream having a fixed record size/layout but unspecified length. MTDAT is intended as a real-time data-stream saved to the disk by the control software of an instrument. Data within the files is written using the low-level fwrite routines, so writing does not require a significant amount of processsing time. Moreover, the record structure is specified when the file is initialized, so the data stream can be interrupted (by a power-outage for example) and the previously written data will be unaffected.
## Including MTDAT in a project
MTDAT should be included in a MATLAB project as a package named "+mtdat".
### Adding as a subtree
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
### Adding as a submodule
```
git submodule add https://github.com/dkovari/mtdat/ +mtdat
#on older versions of git you will also need to pull the updates
git submodule update --init --recursive
```
If you need to update to use the latest version of MATextras then run:
```
git submodule update --init --recursive
```
## Usage
```matlab
%Create a header of file attributes:
my_header.Attribute1 = 'test';
my_header.Attribute2 = 'another test';

%Define record structure:
my_records(1).parameter = 'Field1';
my_records(1).format = 'double';
my_records(1).size = [3,1];

my_records(2).parameter = 'Field2';
my_records(2).format = 'char';
my_records(2).size = [1,10];

%Open the file:
[fid,RecordStruct] = mtdat.writeheader('MyAwesomeFile.mtdat',my_header,my_records);

%Create a record entry:
Record.Field1 = [1.1;2.2;3.3];
Record.Field2 = '0123456789';

mtdat.writerecord(fid,RecordStruct,Record);

%Close the file:
fclose(fid);

%Read the data from the file:
[header,data] = mtdat.read('MyAwesomeFile.mtdat');
```
