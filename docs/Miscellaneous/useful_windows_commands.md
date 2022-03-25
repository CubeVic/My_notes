# Useful windows commands

These are useful windows commands, these commands are to be executed on the CMD terminal

## Display information

### Display content current directory

To display the content of a directory use the  command `dir`

```commandline
dir
```

### Tree style display

To display folder content we can use the `tree` command 

```commandline
tree <foldername>
```

## Delete

### How to delete files

To delete a file we use the command `del` 

```commandline
del <filename.extension>
```

#### Using flag `/f` to force delete a file

```commandline
del /f <filename.extension>
```

### How to delete a folder

The command to be used is `rmdir` there is another option `rd` but I will stay with `rmdir` since is more descriptive and common in other OS.

```commandline
rmdir <name of directory/folder>
```

This process will fail if there are subdirectories, for that we need to add a flag 

####Use flag `/s` with `rmdir`

A flag can be added to delete a folder with sub-folders `/s`. 

```commandline
rmdir /s <name root directory>
```

## Check report or performance of PC

### Check performance and report

```commandline
perfmon /report
```

### System file checker used to fix corrupt or missing files 

```bash
sfc /scannow
```

<aside>
☝🏾 This might take several minutes
</aside>

## Get network information

### Get all macs

```bash
getmac
```