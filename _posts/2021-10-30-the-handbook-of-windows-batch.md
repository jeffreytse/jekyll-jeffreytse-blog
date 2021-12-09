---
layout: post
title: The handbook of Windows Batch
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - note
---

Batch of Windows' hidden secrets for productivity. With just a bit of work,
you can automate monotonous tasks and never worry about them again. Power
users should learn all about batch scripting (a set of commands) sooner
rather than later.  Here is a easy note for you to quickly learn about it.

## Output

```bat
:: Echo an empty line
echo.
echo,
echo:
echo;
echo=
echo+
echo/
echo[
echo]
echo(
echo\

:: Turn off command echo
echo off

:: Turn off command echo including itself
@echo off

:: Provide a way to display remarks / comments on the screen
rem This is a comment
```

## Assignment

```bat
:: Assign a value
set var=

:: Assign value from input with a prompt
set /p var="Your prompt: "

:: Assign value which is a result of an algorithic expression
set num=2
set /a var=%num%+1
```

Here is an operator table:

|     Operator      |       Function        | Priority |
| :---------------: | :-------------------: | :------: |
|       \( \)       |       Grouping        |    0     |
|       ! ~ -       |    Unary Operator     |    1     |
|      \* / %       |      Arithmetic       |    2     |
|         -         |      Arithmetic       |    3     |
|       << >>       |        Bitwise        |    4     |
|         &         |      Logical AND      |    5     |
|         ^         |      Logical NOT      |    6     |
|        \|         |      Logical OR       |    7     |
| = \*= /= %= += -= | Arithmetic assignment |    8     |
| &= ^= \|= <<= >>= | Arithmetic assignment |    9     |
|         ,         |       Delimiter       |    10    |

## String Operations

```bat
::===================================
:: Replace substring
::===================================

set var="foo bar baz"
echo %var:bar=foo%
foo foo baz

::===================================
:: Retrieve substring
::===================================

set var="foo bar baz"

:: Get
echo %var:~,-4%
foo bar

echo %var:~0,3%
foo

:: Get the last one character
echo %var:~-1%
z

:: Get the
echo %var:~-3,2%
baz
```

## Loop

```bat
:: Iterate items
for %%i in (a b c) do @echo %%i
a
b
c

:: Iterate numbers
for /l %%i in (1, 2, 5) do @echo %%i
1
3
5
7
9

:: Iterate string output
for /f "delims=," %%i in ("ab,cd") do @echo %%i
ab

:: Iterate command output
for /f "delims=" %i in ('echo 123 ^& echo 456') do @echo %i
123
456
```

## Function

```bat
:: Declare a variable as function return value
set retval=

:: Call function
call :my_func "hello" "world"
echo retval=%retval%

:: Define a simple function
:my_func
  echo "args: %1 %2"
  retval=1
goto:eof
```

## Extension Variables

```bat
:: This batch file save as C:\foo\bar.bat

:: The batch full path
echo %0
"C:\foo\bar.bat"

:: The batch file directory
echo %cd%
C:\foo

:: The batch file name
echo %~0
bar.bat

:: The batch file full path
echo %~f0
C:\foo\bar.bat

:: The disk drive of batch file
echo %~d0
C:

:: The relative path of batch file directory
echo %~p0
\foo\

:: The absolute path of batch file directory
echo %~dp0
C:\foo\

:: The batch file basename
echo %~n0
bar

:: The batch file extname
echo %~x0
.bat

:: The batch file fullname (basename + extname)
echo %~nx0

:: The batch file short path
echo %~s0

:: The batch file attributes
echo %~a0

:: The batch file created time
echo %~t0

:: The batch file size
echo %~z0

::============================

:: Current Directory (Working Directory)
echo %cd%

:: Current OS name
echo %os%
Windows_NT

:: System Date (Date format based on system locale)
echo %date%
12/31/2021 Fri

:: System Time (HH:MM:SS.SS)
echo %time%

:: Search path for executable files
echo %path%

:: Extension name list of executable files
echo %pathext%

:: Home path of current user
echo %homepath%
\Users\Administrator

:: User profile
echo %userprofile%
C:\Users\Administrator

:: Windows directory
echo %windir%
C:\windows

:: Random number (0~32767)
echo %random%
34521

:: Last error code (Non-zero)
echo %errorlevel%
-1

:: Computer name
echo %computername%

:: Username
echo %username%
Administrator

:: System Drive
echo %systemdrive%
C:

:: System Root
echo %systemroot%
C:\Windows

:: Home Drive
echo %homedrive%

:: Home Share
echo %homeshare%

:: The number of processors
echo %number_of_processors%
8

:: The level of processor
echo %processor_level%
15

:: Application data directory
echo %appdata%
C:\Documents and Settings\Administrator\Application Data

:: All users profile directory
echo %allusersprofile%
C:\Documents and Settings\All Users

:: The command line of current batch program
echo %cmdcmdline%
cmd /c "C:\Documents and Settings\Administrator\Desktop\foo.bat"

:: The extension version of current command processor
echo %cmdextversion%
2

:: The command interpreter
echo %comspec%
C:\windows\system32\cmd.exe

:: The logon server for DC (Domain Controller) verification
echo %logonserver%
\xxxx

:: Processor architecture (x86 or IA64 based on Itanium x86)
echo %processor_architecture%
AMD64

:: Processor identifier (Detail model specification)
echo %processor_identfier%
Intel64 Family 6 Model 142 Stepping 10, GenuineIntel

:: Processor revision
echo %processor_revision%
4f02

:: Current interpreter command prompt setting
echo %prompt%
$P$G

:: Temp directory
echo %temp%
C:\Users\Administrator\AppData\Local\Temp

:: The same as %tmp%
echo %tmp%
C:\Users\Administrator\AppData\Local\Temp

:: User domain
echo %userdomain%
xxxx
```

## Miscellaneous

### Variable Expansion

To expand variables at execution time rather than at parse time, we should
use the option [Enable Delay Expansion](http://ss64.com/nt/delayedexpansion.html)

```bat
:: Enable delayed expansion of variables (Available in Batch file)
setlocal enabledelayedexpansion

set str="foo bar baz"
set start=0
set len=3
set "var=!str:~%start%,%len%!"
```

### Others

```bat
:: Pause with a prompt
pause

:: Pause without a prompt
pause>nul

:: Exit the batch with exitCode
exit \b 0

:: Standar output redirection
>nul
1>nul

:: Error output redirection
2>nul

:: we should escape in `for` loop
2^>nul

:: Run without any output
del c:\foo.txt 1>nul 2>nul
```

## References

- [An A-Z Index of Windows CMD commands](https://ss64.com/nt/)
- [SetLocal Command](https://ss64.com/nt/setlocal.html)
