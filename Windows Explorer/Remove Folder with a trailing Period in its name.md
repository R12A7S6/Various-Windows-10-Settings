There are rare situations where a folder can be named with a trailing period. Through details of Windows' internal that I am unsure of, but possibly due to the period symbol denotes a proceeding file extension or that a number of symbols are forbidden in folder names, a trailing period could introduce unexpected behaviours, such as not being deletable.   

Example folder that cannot be removed:
    C:\User\Test\Desktop\Annoying Folder.

The following is one of the solutions that I have tried and worked.

Run Command Prompt as Administrator:

1. Enter: rd /s "\\?\C:\User\Test\Desktop\Annoying Folder."