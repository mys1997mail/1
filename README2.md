# TTUserSorter
Created new server type "TTS" (TickTrader Server) to UserSorter tool.

# What does it do
TTUserSorter is using for user sorting by required Equity and Traded Volume. It separates users into the groups according the rules, which define by regular expression in configuration file and creates instruction file for MetaManagerScript.

# How do make it work 
All parameters for user sorting are set in configuration file "UserSorter.yml".
 - Open configuration file "UserSorter.yml";
 - Set required Equities and Trade Volumes ranges;
 - Set two regular expressions, which define
 	1) in which groups users should be handled;
	2) group name pattern for handled users;
 - Set TTServer connection
 	1) Address;
	2) Login;
	3) Password;
 - Set SymbolsRules;
 - Set PrefixCommands - strings, which set configuration setting for connection. It will display in result file for further using by MetaManagerScript;
 - Set ScriptRules;
 	1) TimeRange - time range. Only (Current|Last)(Week|Month|Year);
	2) CopyScriptToFolder - path, where should be create result file;
	3) ScriptOutputName - result file name;
	4) ExcludeGroups - regular expressions (can't be blank) which define excluded groups (should not be handled).
 - Save changes in UserSorter.yml;
 
 All parameters set as String.
 - Run TTUserSorter.exe;
 - See result file;
 - Paste the result script inside 'command.sc', and run 'MeraManagerScript.exe';
 

# Examples of configuration file
```
Equities: 
  - 
    Equity: "<300"
    Volumes:
      -
        Range: "<300"
        "Test4" : "1" 
      -
        Range: "300-10000"
        "Test4" : "2" 
      -
        Range: ">10000"
        "Test4" : "4" 
  -
    Equity: "300-10000"
    Volumes:
      -
        Range: "<300"
        "Test4" : "3" 
      -
        Range: "300-10000"
        "Test4" : "6" 
      -
        Range: ">10000"
        "Test4" : "7" 
  -
    Equity: ">10000"
    Volumes:

      -
        Range: "<300"
        "Test4" : "8" 
      -
        Range: "300-10000"
        "Test4" : "9" 
      -
        Range: ">10000"
        "Test4" : "5" 

TTServer:
    Address: "tp.st.soft-fx.eu"
    Login: "72"
    Password: "******"

 
SymbolRules: 
  
PrefixCommands:
  - "// These line was added using PrefixCommands "
  - "Connect {\"ip\":\"tp.st.soft-fx.eu\",\"login\":72,\"password\":\"123qwe!\"}"
 
ScriptRules:
(Current|Last)(Week|Month|Year)
    TimeRange: "CurrentWeek" 
    CopyScriptToFolder: "MetaManagerScript\\InputJob" 
    ScriptOutputName: "command.sc" 
    ExcludeGroup: "Test4*"


```

# Examples of result file
```
// These line was added using PrefixCommands 
Connect {"ip":"tp.st.soft-fx.eu","login":72,"password":"123qwe!"}
EditUser {"Logins":"101034,101035,101036,101037", "Group":"8R2" }
EditUser {"Logins":"101039,101041,101056", "Group":"8R3" }
EditUser {"Logins":"101040", "Group":"3R3" }
EditUser {"Logins":"101042,101043,101044", "Group":"1R4" }
EditUser {"Logins":"101045,101047,101058,101059,101060,101061", "Group":"8R5" }
EditUser {"Logins":"101046", "Group":"3R5" }
EditUser {"Logins":"101048,101049,101050", "Group":"3R6" }
EditUser {"Logins":"101051,101052", "Group":"8R6" }
EditUser {"Logins":"101053,101054,101057", "Group":"8R4" }
EditUser {"Logins":"101055", "Group":"1R6" }

```

# More information
For more information (Equity and Trade Volume values, users do not match regex, users match groups and etc) see Logs file. 

