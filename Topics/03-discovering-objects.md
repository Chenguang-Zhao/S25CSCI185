---
description: You don't have to be a developer to understand and use objects, properties, and methods.
ms.custom: Contributor-mikefrobbins
ms.date: 08/19/2024
ms.reviewer: mirobb
title: Discovering objects, properties, and methods
---

# Chapter 3 - Discovering objects, properties, and methods

PowerShell is an object-oriented scripting language. It represents data and system states using
structured objects derived from .NET classes defined in the .NET Framework. By leveraging the .NET
Framework, PowerShell offers access to various system capabilities, including file system, registry,
and Windows Management Instrumentation (WMI) classes. PowerShell also has access to the .NET
Framework class library, which contains a vast collection of classes that you can use to develop
robust PowerShell scripts.

In PowerShell, each item or state is an instance of an object that can be explored and manipulated.
The `Get-Member` cmdlet is one of the primary tools provided by PowerShell for object discovery,
which reveals an object's characteristics. This chapter explores how PowerShell leverages objects
and how you can discover and manipulate these objects to streamline your scripts and manage your
systems more efficiently.



## Get-Member

`Get-Member` provides insight into the objects, properties, and methods associated with PowerShell
commands. You can pipe any PowerShell command that produces object-based output to `Get-Member`.
When you pipe the output of a command to `Get-Member`, it reveals the structure of the object
returned by the command, detailing its properties and methods.

- **Properties**: The attributes of an object.
- **Methods**: The actions you can perform on an object.

To illustrate this concept, consider a driver's license as an analogy. Like any object, a driver's
license has properties, such as **eye color**, which typically includes `blue` and `brown` values.
In contrast, methods represent actions you can perform on the object. For instance, **Revoke** is a
method that the Department of Motor Vehicles can perform on a driver's license.

### Properties

To retrieve details about the Windows Time service on your system using PowerShell, use the
`Get-Service` cmdlet.

```powershell
Get-Service -Name w32time
```

The results include the **Status**, **Name**, and **DisplayName** properties. The **Status**
property indicates that the service is `Running`. The value for the **Name** property is `w32time`,
and the value for the **DisplayName** property is `Windows Time`.

```Output
Status   Name               DisplayName
------   ----               -----------
Running  w32time            Windows Time
```

To list all available properties and methods for `Get-Service`, pipe it to `Get-Member`.

```powershell
Get-Service -Name w32time | Get-Member
```

The results show the first line contains one piece of significant information. **TypeName**
identifies the type of object returned, which in this example is a
**System.ServiceProcess.ServiceController** object. This name is often abbreviated to the last part
of the **TypeName**, such as **ServiceController**, in this example.

```Output
   TypeName: System.ServiceProcess.ServiceController

Name                      MemberType    Definition
----                      ----------    ----------
Name                      AliasProperty Name = ServiceName
RequiredServices          AliasProperty RequiredServices = ServicesDepend...
Disposed                  Event         System.EventHandler Disposed(Syst...
Close                     Method        void Close()
Continue                  Method        void Continue()
CreateObjRef              Method        System.Runtime.Remoting.ObjRef Cr...
Dispose                   Method        void Dispose(), void IDisposable....
Equals                    Method        bool Equals(System.Object obj)
ExecuteCommand            Method        void ExecuteCommand(int command)
GetHashCode               Method        int GetHashCode()
GetLifetimeService        Method        System.Object GetLifetimeService()
GetType                   Method        type GetType()
InitializeLifetimeService Method        System.Object InitializeLifetimeS...
Pause                     Method        void Pause()
Refresh                   Method        void Refresh()
Start                     Method        void Start(), void Start(string[]...
Stop                      Method        void Stop()
WaitForStatus             Method        void WaitForStatus(System.Service...
CanPauseAndContinue       Property      bool CanPauseAndContinue {get;}
CanShutdown               Property      bool CanShutdown {get;}
CanStop                   Property      bool CanStop {get;}
Container                 Property      System.ComponentModel.IContainer ...
DependentServices         Property      System.ServiceProcess.ServiceCont...
DisplayName               Property      string DisplayName {get;set;}
MachineName               Property      string MachineName {get;set;}
ServiceHandle             Property      System.Runtime.InteropServices.Sa...
ServiceName               Property      string ServiceName {get;set;}
ServicesDependedOn        Property      System.ServiceProcess.ServiceCont...
ServiceType               Property      System.ServiceProcess.ServiceType...
Site                      Property      System.ComponentModel.ISite Site ...
StartType                 Property      System.ServiceProcess.ServiceStar...
Status                    Property      System.ServiceProcess.ServiceCont...
ToString                  ScriptMethod  System.Object ToString();
```

Notice when you piped `Get-Service` to `Get-Member`, there are more properties than are displayed by
default. Although these additional properties aren't shown by default, you can select them by piping
to `Select-Object` and using the **Property** parameter. The following example selects all
properties by piping the results of `Get-Service` to `Select-Object` and specifying the `*` wildcard
character as the value for the **Property** parameter.

```powershell
Get-Service -Name w32time | Select-Object -Property *
```

By default, PowerShell returns four properties as a table and five or more as a list. However, some
commands apply custom formatting to override the default number of properties displayed in a table.
You can use `Format-Table` and `Format-List` to override these defaults manually.

```Output
Name                : w32time
RequiredServices    : {}
CanPauseAndContinue : False
CanShutdown         : True
CanStop             : True
DisplayName         : Windows Time
DependentServices   : {}
MachineName         : .
ServiceName         : w32time
ServicesDependedOn  : {}
ServiceHandle       :
Status              : Running
ServiceType         : Win32OwnProcess, Win32ShareProcess
StartType           : Manual
Site                :
Container           :
```

Specific properties can also be selected using a comma-separated list as the value of the
**Property** parameter.

```powershell
Get-Service -Name w32time |
    Select-Object -Property Status, Name, DisplayName, ServiceType
```

```Output
 Status Name    DisplayName                         ServiceType
 ------ ----    -----------                         -----------
Running w32time Windows Time Win32OwnProcess, Win32ShareProcess
```

You can use wildcard characters when specifying property names with `Select-Object`.

In the following example, use `Can*` as one of the values for the **Property** parameter to return
all the properties that start with `Can`. These include **CanPauseAndContinue**, **CanShutdown**,
and **CanStop**.

```powershell
Get-Service -Name w32time |
    Select-Object -Property Status, DisplayName, Can*
```

Notice there are more properties listed than are displayed by default.

```Output
Status              : Running
DisplayName         : Windows Time
CanPauseAndContinue : False
CanShutdown         : True
CanStop             : True
```

### Methods

Methods are actions you can perform on an object. Use the **MemberType** parameter to narrow down
the results of `Get-Member` to display only the methods for `Get-Service`.

```powershell
Get-Service -Name w32time | Get-Member -MemberType Method
```

As you can see, there are several methods.

```Output
   TypeName: System.ServiceProcess.ServiceController

Name                      MemberType Definition
----                      ---------- ----------
Close                     Method     void Close()
Continue                  Method     void Continue()
CreateObjRef              Method     System.Runtime.Remoting.ObjRef Creat...
Dispose                   Method     void Dispose(), void IDisposable.Dis...
Equals                    Method     bool Equals(System.Object obj)
ExecuteCommand            Method     void ExecuteCommand(int command)
GetHashCode               Method     int GetHashCode()
GetLifetimeService        Method     System.Object GetLifetimeService()
GetType                   Method     type GetType()
InitializeLifetimeService Method     System.Object InitializeLifetimeServ...
Pause                     Method     void Pause()
Refresh                   Method     void Refresh()
Start                     Method     void Start(), void Start(string[] args)
Stop                      Method     void Stop()
WaitForStatus             Method     void WaitForStatus(System.ServicePro...
```

You can use the **Stop** method to stop a Windows service. You must run this command from an
elevated PowerShell session.

```powershell
(Get-Service -Name w32time).Stop()
```

Query the status of the Windows Time service to confirm it's stopped.

```powershell
Get-Service -Name w32time
```

```Output
Status   Name               DisplayName
------   ----               -----------
Stopped  w32time            Windows Time
```

You might use methods sparingly, but you should be aware of them. Sometimes, you find `Get-*`
commands without a corresponding `Set-*` command. Often, you can find a method to perform a `Set-*`
action in this scenario. The `Get-SqlAgentJob` cmdlet in the **SqlServer** PowerShell module is an
excellent example. No corresponding `Set-*` cmdlet exists, but you can use a method to complete the
same task. For more information about the **SqlServer** PowerShell module and installation
instructions, see the [SQL Server PowerShell overview][sql-server-powershell].

Another reason to be aware of methods is some PowerShell users assume you can't make destructive
changes with `Get-*` commands, but they can actually cause severe problems if misused.

A better option is to use a dedicated cmdlet if one exists to perform an action. For example, use
the `Start-Service` cmdlet to start the Windows Time service.

By default, `Start-Service`, like the **Start** method of `Get-Service`, doesn't return any results.
However, one of the benefits of using a cmdlet is that it often provides additional capabilities
that aren't available with a method.

In the following example, use the **PassThru** parameter, which causes a cmdlet that doesn't
typically produce output to generate output.

Since PowerShell doesn't participate in User Access Control (UAC), you must run commands that
require elevation, such as `Start-Service`, from an elevated PowerShell session.

```powershell
Get-Service -Name w32time | Start-Service -PassThru
```

```Output
Status   Name               DisplayName
------   ----               -----------
Running  w32time            Windows Time
```

> [!NOTE]
> When working with PowerShell cmdlets, it's important to avoid making assumptions about their
> output.

To retrieve information about the PowerShell process running on your lab environment computer, use
the `Get-Process` cmdlet.

```powershell
Get-Process -Name PowerShell
```

```Output
Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    710      31    55692      70580       0.72   9436   2 powershell
```

To determine the available properties, pipe `Get-Process` to `Get-Member`.

```powershell
Get-Process -Name PowerShell | Get-Member
```

When using the `Get-Process` command, you might notice that some properties displayed by default are
missing when you view the results of `Get-Member`. This behavior is because several of the values
shown by default, such as `NPM(K)`, `PM(K)`, `WS(K)`, and `CPU(s)`, are calculated properties. You
must pipe commands to `Get-Member` to determine their actual property names.

```Output
   TypeName: System.Diagnostics.Process

Name                       MemberType     Definition
----                       ----------     ----------
Handles                    AliasProperty  Handles = Handlecount
Name                       AliasProperty  Name = ProcessName
NPM                        AliasProperty  NPM = NonpagedSystemMemorySize64
PM                         AliasProperty  PM = PagedMemorySize64
SI                         AliasProperty  SI = SessionId
VM                         AliasProperty  VM = VirtualMemorySize64
WS                         AliasProperty  WS = WorkingSet64
Disposed                   Event          System.EventHandler Disposed(Sy...
ErrorDataReceived          Event          System.Diagnostics.DataReceived...
Exited                     Event          System.EventHandler Exited(Syst...
OutputDataReceived         Event          System.Diagnostics.DataReceived...
BeginErrorReadLine         Method         void BeginErrorReadLine()
BeginOutputReadLine        Method         void BeginOutputReadLine()
CancelErrorRead            Method         void CancelErrorRead()
CancelOutputRead           Method         void CancelOutputRead()
Close                      Method         void Close()
CloseMainWindow            Method         bool CloseMainWindow()
CreateObjRef               Method         System.Runtime.Remoting.ObjRef ...
Dispose                    Method         void Dispose(), void IDisposabl...
Equals                     Method         bool Equals(System.Object obj)
GetHashCode                Method         int GetHashCode()
GetLifetimeService         Method         System.Object GetLifetimeService()
GetType                    Method         type GetType()
InitializeLifetimeService  Method         System.Object InitializeLifetim...
Kill                       Method         void Kill()
Refresh                    Method         void Refresh()
Start                      Method         bool Start()
ToString                   Method         string ToString()
WaitForExit                Method         bool WaitForExit(int millisecon...
WaitForInputIdle           Method         bool WaitForInputIdle(int milli...
__NounName                 NoteProperty   string __NounName=Process
BasePriority               Property       int BasePriority {get;}
Container                  Property       System.ComponentModel.IContaine...
EnableRaisingEvents        Property       bool EnableRaisingEvents {get;s...
ExitCode                   Property       int ExitCode {get;}
ExitTime                   Property       datetime ExitTime {get;}
Handle                     Property       System.IntPtr Handle {get;}
HandleCount                Property       int HandleCount {get;}
HasExited                  Property       bool HasExited {get;}
Id                         Property       int Id {get;}
MachineName                Property       string MachineName {get;}
MainModule                 Property       System.Diagnostics.ProcessModul...
MainWindowHandle           Property       System.IntPtr MainWindowHandle ...
MainWindowTitle            Property       string MainWindowTitle {get;}
MaxWorkingSet              Property       System.IntPtr MaxWorkingSet {ge...
MinWorkingSet              Property       System.IntPtr MinWorkingSet {ge...
Modules                    Property       System.Diagnostics.ProcessModul...
NonpagedSystemMemorySize   Property       int NonpagedSystemMemorySize {g...
NonpagedSystemMemorySize64 Property       long NonpagedSystemMemorySize64...
PagedMemorySize            Property       int PagedMemorySize {get;}
PagedMemorySize64          Property       long PagedMemorySize64 {get;}
PagedSystemMemorySize      Property       int PagedSystemMemorySize {get;}
PagedSystemMemorySize64    Property       long PagedSystemMemorySize64 {g...
PeakPagedMemorySize        Property       int PeakPagedMemorySize {get;}
PeakPagedMemorySize64      Property       long PeakPagedMemorySize64 {get;}
PeakVirtualMemorySize      Property       int PeakVirtualMemorySize {get;}
PeakVirtualMemorySize64    Property       long PeakVirtualMemorySize64 {g...
PeakWorkingSet             Property       int PeakWorkingSet {get;}
PeakWorkingSet64           Property       long PeakWorkingSet64 {get;}
PriorityBoostEnabled       Property       bool PriorityBoostEnabled {get;...
PriorityClass              Property       System.Diagnostics.ProcessPrior...
PrivateMemorySize          Property       int PrivateMemorySize {get;}
PrivateMemorySize64        Property       long PrivateMemorySize64 {get;}
PrivilegedProcessorTime    Property       timespan PrivilegedProcessorTim...
ProcessName                Property       string ProcessName {get;}
ProcessorAffinity          Property       System.IntPtr ProcessorAffinity...
Responding                 Property       bool Responding {get;}
SafeHandle                 Property       Microsoft.Win32.SafeHandles.Saf...
SessionId                  Property       int SessionId {get;}
Site                       Property       System.ComponentModel.ISite Sit...
StandardError              Property       System.IO.StreamReader Standard...
StandardInput              Property       System.IO.StreamWriter Standard...
StandardOutput             Property       System.IO.StreamReader Standard...
StartInfo                  Property       System.Diagnostics.ProcessStart...
StartTime                  Property       datetime StartTime {get;}
SynchronizingObject        Property       System.ComponentModel.ISynchron...
Threads                    Property       System.Diagnostics.ProcessThrea...
TotalProcessorTime         Property       timespan TotalProcessorTime {get;}
UserProcessorTime          Property       timespan UserProcessorTime {get;}
VirtualMemorySize          Property       int VirtualMemorySize {get;}
VirtualMemorySize64        Property       long VirtualMemorySize64 {get;}
WorkingSet                 Property       int WorkingSet {get;}
WorkingSet64               Property       long WorkingSet64 {get;}
PSConfiguration            PropertySet    PSConfiguration {Name, Id, Prio...
PSResources                PropertySet    PSResources {Name, Id, Handleco...
Company                    ScriptProperty System.Object Company {get=$thi...
CPU                        ScriptProperty System.Object CPU {get=$this.To...
Description                ScriptProperty System.Object Description {get=...
FileVersion                ScriptProperty System.Object FileVersion {get=...
Path                       ScriptProperty System.Object Path {get=$this.M...
Product                    ScriptProperty System.Object Product {get=$thi...
ProductVersion             ScriptProperty System.Object ProductVersion {g...
```

You can't pipe a command to `Get-Member` that doesn't generate output. Because `Start-Service`
doesn't produce output by default, attempting to pipe it to `Get-Member` results in an error.

```powershell
Start-Service -Name w32time | Get-Member
```

> [!NOTE]
> To be piped to `Get-Member`, a command must produce object-based output.

```Output
Get-Member : You must specify an object for the Get-Member cmdlet.
At line:1 char:31
+ Start-Service -Name w32time | Get-Member
+                               ~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Get-Member], InvalidOperation
   Exception
    + FullyQualifiedErrorId : NoObjectInGetMember,Microsoft.PowerShell.Comma
   nds.GetMemberCommand
```

To avoid this error, specify the **PassThru** parameter with `Start-Service`. As previously
mentioned, adding the **PassThru** parameter causes a cmdlet that doesn't usually produce output to
generate output.

```powershell
Start-Service -Name w32time -PassThru | Get-Member
```

```Output
   TypeName: System.ServiceProcess.ServiceController

Name                      MemberType    Definition
----                      ----------    ----------
Name                      AliasProperty Name = ServiceName
RequiredServices          AliasProperty RequiredServices = ServicesDepend...
Disposed                  Event         System.EventHandler Disposed(Syst...
Close                     Method        void Close()
Continue                  Method        void Continue()
CreateObjRef              Method        System.Runtime.Remoting.ObjRef Cr...
Dispose                   Method        void Dispose(), void IDisposable....
Equals                    Method        bool Equals(System.Object obj)
ExecuteCommand            Method        void ExecuteCommand(int command)
GetHashCode               Method        int GetHashCode()
GetLifetimeService        Method        System.Object GetLifetimeService()
GetType                   Method        type GetType()
InitializeLifetimeService Method        System.Object InitializeLifetimeS...
Pause                     Method        void Pause()
Refresh                   Method        void Refresh()
Start                     Method        void Start(), void Start(string[]...
Stop                      Method        void Stop()
WaitForStatus             Method        void WaitForStatus(System.Service...
CanPauseAndContinue       Property      bool CanPauseAndContinue {get;}
CanShutdown               Property      bool CanShutdown {get;}
CanStop                   Property      bool CanStop {get;}
Container                 Property      System.ComponentModel.IContainer ...
DependentServices         Property      System.ServiceProcess.ServiceCont...
DisplayName               Property      string DisplayName {get;set;}
MachineName               Property      string MachineName {get;set;}
ServiceHandle             Property      System.Runtime.InteropServices.Sa...
ServiceName               Property      string ServiceName {get;set;}
ServicesDependedOn        Property      System.ServiceProcess.ServiceCont...
ServiceType               Property      System.ServiceProcess.ServiceType...
Site                      Property      System.ComponentModel.ISite Site ...
StartType                 Property      System.ServiceProcess.ServiceStar...
Status                    Property      System.ServiceProcess.ServiceCont...
ToString                  ScriptMethod  System.Object ToString();
```

`Out-Host` is designed to show output directly in the PowerShell host and doesn't produce
object-based output. As a result, you can't pipe its output to `Get-Member`, which requires
object-based input.

```powershell
Get-Service -Name w32time | Out-Host | Get-Member
```

```Output
Status   Name               DisplayName
------   ----               -----------
Running  w32time            Windows Time

Get-Member : You must specify an object for the Get-Member cmdlet.
At line:1 char:40
+ Get-Service -Name w32time | Out-Host | Get-Member
+                                        ~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Get-Member], InvalidOperation
   Exception
    + FullyQualifiedErrorId : NoObjectInGetMember,Microsoft.PowerShell.Comma
   nds.GetMemberCommand
```

## Get-Command

Knowing the type of object a command produces allows you to search for commands that accept that
type of object as input.

```powershell
Get-Command -ParameterType ServiceController
```

The following commands accept a **ServiceController** object via pipeline or parameter input.

```Output
CommandType     Name                                               Version
-----------     ----                                               -------
Cmdlet          Get-Service                                        3.1.0.0
Cmdlet          Restart-Service                                    3.1.0.0
Cmdlet          Resume-Service                                     3.1.0.0
Cmdlet          Set-Service                                        3.1.0.0
Cmdlet          Start-Service                                      3.1.0.0
Cmdlet          Stop-Service                                       3.1.0.0
Cmdlet          Suspend-Service                                    3.1.0.0
```



## Summary

In this chapter, you learned how to determine what type of object a command produces, what
properties and methods are available for a command, and how to work with commands that limit the
properties returned by default.

## Review

1. What type of object does the `Get-Process` cmdlet produce?
1. How do you determine what the available properties are for a command?
1. What should you check for if a command exists to get something but not to set the same thing?
1. How can some commands that don't return output by default be made to generate output?
1. What should you consider doing when prototyping a command that produces a large amount of output?

## References

- [Get-Member][get-member]
- [Viewing Object Structure (Get-Member)][viewing-object-structure]
- [about_Objects][about-objects]
- [about_Properties][about-properties]
- [about_Methods][about-methods]
- [No PowerShell Cmdlet to Start or Stop Something? Don't Forget to Check for Methods on the Get Cmdlets][use-methods]

## Next steps

In the next chapter, you'll learn about one-liners and the pipeline.

<!-- link references -->

[rsat-windows]: /troubleshoot/windows-server/system-management-components/remote-server-administration-tools
[windows-management-modules]: /powershell/scripting/whats-new/module-compatibility#windows-management-modules
[sql-server-powershell]: /sql/powershell/download-sql-server-ps-module
[get-member]: /powershell/module/microsoft.powershell.utility/get-member
[viewing-object-structure]: /powershell/scripting/samples/viewing-object-structure--get-member-
[about-objects]: /powershell/module/microsoft.powershell.core/about/about_objects
[about-properties]: /powershell/module/microsoft.powershell.core/about/about_properties
[about-methods]: /powershell/module/microsoft.powershell.core/about/about_methods
[use-methods]: https://mikefrobbins.com/2016/12/15/no-powershell-cmdlet-to-start-or-stop-something-dont-forget-to-check-for-methods-on-the-get-cmdlets/
