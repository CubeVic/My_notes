you may make the alias(es) persistent with the following steps:

1. Create a .bat or .cmd file with your `DOSKEY` commands.
2. Run regedit and go to `HKEY_CURRENT_USER\Software\Microsoft\Command Processor`
3. Add String Value entry with the name AutoRun and the full path of your .bat/.cmd file.

For example, `%USERPROFILE%\alias.cmd`, replacing the initial segment of the path with `%USERPROFILE%` is useful for syncing among multiple machines.

This way, every time cmd is run, the aliases are loaded.

For completeness, here is a template to illustrate the kind of aliases one may find useful.

```Batch
@echo off

:: Temporary system path at cmd startup

:: set PATH=%PATH%;"C:\Program Files\Sublime Text 2\"

:: Add to path by command

:: DOSKEY add_python26=set PATH=%PATH%;"C:\Python26\"
:: DOSKEY add_python33=set PATH=%PATH%;"C:\Python33\"

:: Commands

DOSKEY ls=dir /B
DOSKEY notes = cd Documents/Notes/notes
:: DOSKEY sublime=sublime_text $*  
    ::sublime_text.exe is name of the executable. By adding a temporary entry to system path, we don't have to write the whole directory anymore.
:: DOSKEY gsp="C:\Program Files (x86)\Sketchpad5\GSP505en.exe"
::DOSKEY alias=notepad %USERPROFILE%\Dropbox\alias.cmd

:: Common directories

::DOSKEY dropbox=cd "%USERPROFILE%\Dropbox\$*"
::DOSKEY research=cd %USERPROFILE%\Dropbox\Research\
```