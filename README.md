# CBT739
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. 
Due to amazing work by Alison Zhang and Jake Choi repos are no longer deleted.

```
//***FILE 739 is from Ron Brown, and contains a package to update   *   FILE 739
//*           your TSO session's ISPF command tables dynamically.   *   FILE 739
//*           This is a heavy-duty package with lots of options     *   FILE 739
//*           and tutorial.  It is a very good idea (and instruc-   *   FILE 739
//*           tive too) to read the tutorials associated with the   *   FILE 739
//*           ISPFCMDS package.                                     *   FILE 739
//*                                                                 *   FILE 739
//*           email:  Ron_Brown@hotmail.com                         *   FILE 739
//*                                                                 *   FILE 739
//*                ISPF Commands Tool (version 7.0)                 *   FILE 739
//*               ----------------------------------                *   FILE 739
//*    This tool enables the user to dynamically display and        *   FILE 739
//*    modify all their ISPF commands, from (almost) any ISPF       *   FILE 739
//*    panel.  It provides easy search facilities and shows         *   FILE 739
//*    command relationships to simplify the management of          *   FILE 739
//*    very large numbers of commands.  That empowers the           *   FILE 739
//*    user to fully exploit the flexibility of commands for        *   FILE 739
//*    invoking all their ISPF activities.  This tool is            *   FILE 739
//*    packaged with an "Enhanced ISPF Configuration Utility"       *   FILE 739
//*    included to make it easier for users to configure            *   FILE 739
//*    their ISPF.                                                  *   FILE 739
//*                                                                 *   FILE 739
//*   Why do you need this tool?                                    *   FILE 739
//*   --------------------------                                    *   FILE 739
//*   It is possible for TSO users to have up to 8 active           *   FILE 739
//*   ISPF command tables, but IBM still provide only the old       *   FILE 739
//*   option 3.9 "Command Table Utility" to display or update       *   FILE 739
//*   them.  Particularly if you are going to use many              *   FILE 739
//*   command tables with a large number of commands you will       *   FILE 739
//*   benefit from a much more sophisticated tool to manage         *   FILE 739
//*   them.  This tool provides all the same functionality          *   FILE 739
//*   (as 3.9) plus much more, including:                           *   FILE 739
//*                                                                 *   FILE 739
//*   1) While in any ISPF application, it can display the          *   FILE 739
//*      full list of available commands from all the command       *   FILE 739
//*      tables active in that application, or you can select       *   FILE 739
//*      just particular tables.  It can also open inactive         *   FILE 739
//*      command tables for display and update.                     *   FILE 739
//*                                                                 *   FILE 739
//*   2) The list of commands is in the standard ISPF order,        *   FILE 739
//*      or you can sort the list into different orders (eg.        *   FILE 739
//*      command name order).                                       *   FILE 739
//*                                                                 *   FILE 739
//*   3) You can list only the commands with names matching a       *   FILE 739
//*      particular mask (eg. listing only commands beginning       *   FILE 739
//*      with "REF").  You can list only the commands with a        *   FILE 739
//*      particular string in their description or action           *   FILE 739
//*      (eg. listing only commands with "KEY").                    *   FILE 739
//*                                                                 *   FILE 739
//*   4) It shows the relationships between commands in all         *   FILE 739
//*      the tables.  It indicates commands which OVERRIDE          *   FILE 739
//*      others (and which are overridden).  It shows the valid     *   FILE 739
//*      TRUNCATIONS allowed for commands.  It tracks command       *   FILE 739
//*      ALIAS chains to show the effective action of such          *   FILE 739
//*      commands.                                                  *   FILE 739
//*                                                                 *   FILE 739
//*   5) It can display which libraries the active command          *   FILE 739
//*      tables are in, plus some table statistics.                 *   FILE 739
//*                                                                 *   FILE 739
//*   6) You can ADD, UPDATE or DELETE the commands in any          *   FILE 739
//*      active command table.  You can also COPY or MOVE           *   FILE 739
//*      commands within or between tables.  All the changes        *   FILE 739
//*      are immediately active, without restarting ISPF.           *   FILE 739
//*      Thus you can temporarily change the commands in any        *   FILE 739
//*      ISPF application while you are actually using it.          *   FILE 739
//*                                                                 *   FILE 739
//*   7) You can permanently SAVE any command changes to            *   FILE 739
//*      disk, except for the ISPCMDS table.                        *   FILE 739
//*                                                                 *   FILE 739
//*   8) It can create new Application-, User- or Site-             *   FILE 739
//*      command tables.                                            *   FILE 739
//*                                                                 *   FILE 739
//*   There are extensive HELP panels detailing the                 *   FILE 739
//*   functionality, plus much information about ISPF command       *   FILE 739
//*   tables and how to configure them.                             *   FILE 739
//*                                                                 *   FILE 739
//*                                                                 *   FILE 739
//*   Installation                                                  *   FILE 739
//*   ------------                                                  *   FILE 739
//*    This version is compatible with all ISPF releases from       *   FILE 739
//*    version 3.4 to version 5.8 (z/OS 1.8).  The included         *   FILE 739
//*    Configuration Utility can get your current ISPF              *   FILE 739
//*    configuration parameters only up to version 5.7, but         *   FILE 739
//*    it will create a usable keyword file which can be used       *   FILE 739
//*    with later versions of ISPF.                                 *   FILE 739
//*                                                                 *   FILE 739
//*    a) Assemble/Link members ISPFCMDL & ISPFCMDO                 *   FILE 739
//*                                                                 *   FILE 739
//*    b) Copy ISPFCMDS member to a library in the SYSEXEC          *   FILE 739
//*       (or SYSPROC) concatenation                                *   FILE 739
//*                                                                 *   FILE 739
//*    c) Copy all other ISPFCMxx members into the ISPPLIB          *   FILE 739
//*       concatenation                                             *   FILE 739
//*                                                                 *   FILE 739
//*    d) Copy all JSPCxxxx members to a library in the             *   FILE 739
//*       SYSEXEC (or SYSPROC) concatenation                        *   FILE 739
//*                                                                 *   FILE 739
//*    e) Copy all JSPPCxxx members into the ISPPLIB                *   FILE 739
//*       concatenation                                             *   FILE 739
//*                                                                 *   FILE 739
//*    Notes:                                                       *   FILE 739
//*    - It is worthwhile to compile the Rexx module                *   FILE 739
//*      ISPFCMDS, to get better performance (mainly because        *   FILE 739
//*      of its size).                                              *   FILE 739
//*                                                                 *   FILE 739
//*    - It is designed to be used from within every other          *   FILE 739
//*      ISPF application, hence it should be in base               *   FILE 739
//*      libraries and not LIBDEF'd.                                *   FILE 739
//*                                                                 *   FILE 739
//*    - This tool is most useful when User & Site command          *   FILE 739
//*      tables have been defined in the ISPF configuration         *   FILE 739
//*      module, hence it is recommended that some are              *   FILE 739
//*      defined.                                                   *   FILE 739
//*                                                                 *   FILE 739
//*    - Control of the updating of the disk copy of any            *   FILE 739
//*      command tables is left to an external security             *   FILE 739
//*      product (eg. RACF).                                        *   FILE 739
//*                                                                 *   FILE 739
//*    - After installation, the product can be quickly             *   FILE 739
//*      checked by following the instructions in the $IVP          *   FILE 739
//*      member of this library.                                    *   FILE 739
//*                                                                 *   FILE 739
//*   Use                                                           *   FILE 739
//*   ---                                                           *   FILE 739
//*    It is invoked by 'TSO %ISPFCMDS' or better yet -             *   FILE 739
//*    create a command like the following:                         *   FILE 739
//*                                                                 *   FILE 739
//*      Verb  . . . : CMDS                                         *   FILE 739
//*      Trunc . . . : 0                                            *   FILE 739
//*      Action  . . : SELECT CMD(%ISPFCMDS &ZPARM) SCRNAME(CMDS)   *   FILE 739
//*      Description : 'ISPF Commands' tool                         *   FILE 739
//*                                                                 *   FILE 739
//*    If ISPFCMDS is compiled use:                                 *   FILE 739
//*  Action : SELECT CMD(ISPFCMDS &ZPARM) SCRNAME(CMDS) LANG(CREX)  *   FILE 739
//*                                                                 *   FILE 739
//*    - It will work with future versions of ISPF by               *   FILE 739
//*      assuming that the names of any tables which are            *   FILE 739
//*      defined but not active, can be found in an ISPF            *   FILE 739
//*      configuration module with the same name and field          *   FILE 739
//*      offsets as for ISPF for z/OS 1.7 (version 5.7).            *   FILE 739
//*      That assumption will probably be true for at least         *   FILE 739
//*      the next few ISPF releases.                                *   FILE 739
//*                                                                 *   FILE 739
//*   Support                                                       *   FILE 739
//*   -------                                                       *   FILE 739
//*    The author, Ron Brown, can be contacted at:                  *   FILE 739
//*    Ron_Brown@hotmail.com                                        *   FILE 739
//*                                                                 *   FILE 739
```
