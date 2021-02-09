1.cls- to clear the screen

2.ECHO
This batch command displays messages, or turns command echoing on or off.
Syntax: ECHO “string”

@echo off- is to off the display so that command will not be shown when executed

By default, a batch file will display its command as it runs. The purpose of this first command is to turn off this display. The command "echo off" turns off the display for the whole script, except for the "echo off" command itself. The "at" sign "@" in front makes the command apply to itself as well.

3.MD
This batch command creates a new directory in the current location.
Syntax: md [new directory name]

4.MOVE/COPY/COMP
This batch command moves/copy/comp files or directories between directories.
Syntax: move/copy/comp [source] [destination]

5.PATH
This batch command displays or sets the path variable.
Syntax: PATH
Example:
@echo off 
Echo %PATH% - always use %path% for diaplying the path

6.PAUSE
This batch command prompts the user and waits for a line of input to be entered.
Syntax: Pause
Example:
@echo off 
pause
Output:
The command prompt will show the message “Press any key to continue….” to the user and wait for the user’s input.

7.RD
This batch command removes directories, but the directories need to be empty before they can be removed.
Syntax: rd [directoryname]
- Removes the directory Dir1 including all the files and subdirectories in it rd /s Dir1
- Removes the directory Dir1 including all the files and subdirectories in it but asks for a user confirmation first.
rd /q /s Dir1

8.REN
Renames files and directories
Syntax: ren [oldfile/dirname] [newfile/dirname]

9.REM
This batch command is used for remarks in batch files, preventing the content of the remark from being executed. USED FOR COMMENTING
Syntax: REM description

OR WE CAN USE :: FOR COMMENTS

10.START
This batch command starts a program in new window, or opens a document.
Syntax: start notepad.exe

11.TYPE
This batch command prints the content of a file or files to the output.
Syntax:TYPE [filename]

12.VOL
This batch command displays the volume labels.
Syntax:VOL

13.ATTRIB
Displays or sets the attributes of the files in the current directory
Syntax: attrib

Example:
The following example shows the different variants of the attrib command.

@echo off
Rem Displays the attribites of the file in the current directory
Attrib

Rem Displays the attributes of the file lists.txt
attrib C:\tp\lists.txt

Rem Adds the "Read-only" attribute to the file.
attrib +r C:\tp\lists.txt
Attrib C:\tp\lists.txt

Rem Removes the "Archived" attribute from the file
attrib -a C:\tp\lists.txt
Attrib C:\tp\lists.txt

14.CHKDSK
This batch command checks the disk for any problems.
Syntax: chkdsk

15.DRIVERQUERY
This batch command shows all installed device drivers and their properties.
Syntax: driverquery

16.EXPAND
This batch command extracts files from compressed .cab cabinet files.
Syntax: EXPAND [cabinetfilename]

17.FIND
This batch command searches for a string in files or input, outputting matching lines.
Syntax: FIND [text] [destination]
Where text is the string which needs to be searched for and destination is the source in which the search needs to take place.

Example:
@echo off 
FIND "Application" C:\tp\lists.txt

18.TASKLIST
This batch command lists tasks, including task name and process id (PID).
Syntax: Tasklist

USE JPS to list the task with proecssid

19.TASKKILL
used to kill the task
Syntax: taskkill -f /PID processid

20.SET 
This is used to set the variable
Syntax: SET xyz=c:\projects

to display:
echo %xyz%



Batch Script - Variables

- There are two types of variables in batch files. One is for parameters which can be passed when the batch file is called and the other is done via the set command.

1.Command Line Arguments
 - arguments can be passed to the batch file when invoked. 
 - EX: create a file test.bat with following command
	@echo off 
	echo %1 
	echo %2 
	echo %3
 -  run the batch as test.bat 1 2 3 
	its take 3 parameter

2.SET Coammand
 - Synatx:
	@echo off 
	set message=Hello World //assign variable
	echo %message%	//print the value

 - Working with Numeric Values
	In batch script, it is also possible to define a variable to hold a numeric value. This can be done by using the /A switch.
 - Syntax:
	@echo off 
	SET /A a = 5 //assignvalue
	SET /A b = 10 
	SET /A c = %a% + %b% //operation 
	echo %c%  //result

IF WE WANT TO PRINT THE VALUE OF A VARIAVLE THEN USE %VARIABLE%

 - GLOBAL N LOCAL VARIABLE
  -Syntax:
	@echo off 
	set globalvar = 5
	SETLOCAL
	set var = 13145
	set /A var = %var% + 5
	echo %var%
	echo %globalvar%
	ENDLOCAL
  -O/P:
	13150
	5


ARRARYS

1.Creating n accessing arrary
 - EXAMPLE:
     1.	@echo off 
	set list = 1 2 3 4 
	(for %%a in (%list%) do ( 
	   echo %%a 
	))

     2.	set arr[0] = 1 
	set arr[1] = 2 
	set arr[2] = 3 
	echo The first element of the array is %arr[0]% 
	echo The second element of the array is %arr[1]% 
	echo The third element of the array is %arr[2]%
IF:
The first decision-making statement is the ‘if’ statement. The general form of this statement in Batch Script is as follows −

Syntax: if(condition) do_something
EX:
SET /A a = 5 
SET /A b = 10 
SET /A c = %a% + %b% 
if %c%==15 echo "The value of variable c is 15" 
if %c%==10 echo "The value of variable c is 10"

OPERATORS:

Operator	Description	Example
EQU	Tests the equality between two objects	2 EQU 2 will give true
NEQ	Tests the difference between two objects	3 NEQ 2 will give true
LSS	Checks to see if the left object is less than the right operand	2 LSS 3 will give true
LEQ	Checks to see if the left object is less than or equal to the right operand	2 LEQ 3 will give true
GTR	Checks to see if the left object is greater than the right operand	3 GTR 2 will give true
GEQ	Checks to see if the left object is greater than or equal to the right operand	3 GEQ 2 will give true

LOOPING:

1.WHILE:
- Syntax:
Set counters
:label
If (expression) (
   Do_something
   Increment counter
   Go back to :label
)

- EX:
@echo off
SET /A "index = 1"
SET /A "count = 5"
:while
if %index% leq %count% (
   echo The value of index is %index%
   SET /A "index = index + 1"
   goto :while
)

2.FOR
- Syntax:
FOR %%variable IN list DO do_something
- EX:
@echo off 
FOR %%F IN (1 2 3 4 5) DO echo %%F

FUNCTIONS:

- Syntax:
	:function_name 
	Do_something 
	EXIT /B 0
- Example:
	:Display 
	SET /A index=2 
	echo The value of index is %index% 
	EXIT /B 0

1.calling a function:
- Syntax:
call :function_name
- Ex:
@echo off 
SETLOCAL 
CALL :Display 
EXIT /B %ERRORLEVEL% 
:Display 
SET /A index=2 
echo The value of index is %index% 
EXIT /B 0

->One key thing to note when defining the main program is to ensure that the statement EXIT /B %ERRORLEVEL% is put in the main program to separate the code of the main program from the function.

2.function with parameter
- Syntax:
Call :function_name parameter1, parameter2… parametern
The parameters can then be accessed from within the function by using the tilde (~) character along with the positional number of the parameter.


- Example:
@echo off
SETLOCAL
CALL :Display 5 , 10
EXIT /B %ERRORLEVEL%
:Display
echo The value of parameter 1 is %~1
echo The value of parameter 2 is %~2
EXIT /B 0

3.function with return values
- Syntax
Call :function_name value1, value2… valuen

- Example:
@echo off
SETLOCAL
CALL :SetValue value1,value2
echo %value1%
echo %value2%
EXIT /B %ERRORLEVEL%
:SetValue
set "%~1 = 5"
set "%~2 = 10"
EXIT /B 0








