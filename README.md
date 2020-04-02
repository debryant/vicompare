vicompare
================
### This repository and any materials provided by NI therein are provided AS IS. NI DISCLAIMS ANY AND ALL LIABILITIES FOR AND MAKES NO WARRANTIES, EITHER EXPRESS OR IMPLIED, INCLUDING WITHOUT LIMITATION ANY WARRANTIES OF MERCHANTABILITY, FITNESS FOR  PARTICULAR PURPOSE, OR NON-INFRINGEMENT OF INTELLECTUAL PROPERTY. NI shall have no liability for any direct, indirect, incidental, punitive, special, or consequential damages for your use of the repository or any materials contained therein. 
================

This is a tool used to perform diff and merge on LabVIEW VIs using git. Git is at present difficult to configure and use, and the paths require significant processing to make them work on windows with LabVIEW's diff tool. This attempts to bridge the gap by adding that processing in a LV executable.

Instructions are to:

1. open vicompare.lvproj
2. Build the executables, diffmain and mergemain
3. Build the source distribution, actions
4. Build the installer
5. Run the installer


If you need to add additional processing steps, all actions performed are called by <project>/diffmergetool/action/performaction. First it determines what to do--diff or merge. This string is automatically inserted as an argument by the main exe (diff or merge executables). It then calls the "fix paths" function, which is responsible for performing all operations on the arguments, which are assumed to be paths at this point. Then, diff or merge is called. Diff and merge are black boxes (private methods), but all the necessary items are exposed as parameters.


Configuring for sourcetree is as follows: 
(Note: The asterics must be escaped by preceeding them with a backslash.)

- Difftool: Custom
- Path: C:\viscc\vidiff.exe
- Args: \"$LOCAL\" \"$REMOTE\"	<< to diff against the previous commit of the file, if any in this Pull Request, else against master
- Args: \"$LOCAL\" \"$MERGED\"	<< to diff against master

- Mergetool: Custom
- Path: C:\viscc\vimerge.exe
- Args: \"$BASE\" \"$REMOTE\" \"$LOCAL\" \"$MERGED\"


Additional args:
- -lv or -version specifies the labview version to use
- -lvpath specifies the path to the labview exe, including the exe file name

- You can also use any of the standard LV Diff commands:
    - -noattr
    - -nofp
    - -nofppos
    - -nobd
    - -nobdcosm
    - -nobdpos


