
Powershell Arguments without using powershell.exe
```
using System;
using System.Collections.Generic;
using System.Collections.ObjectModel;
using System.Diagnostics;
using System.Linq;
using System.Management.Automation;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace PS_Argument
{
    class Program
    {
        static void Main(string[] args)
        {

            ProcessStartInfo processInfo = new ProcessStartInfo();
            processInfo.FileName = @"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe";

            processInfo.Arguments = @"&Get-WmiObject -Namespace root\SecurityCenter2 -Class AntiVirusProduct";

            processInfo.RedirectStandardOutput = true;
            processInfo.UseShellExecute = false;



            Process process = new Process();
            process.StartInfo = processInfo;
            process.Start();

            Console.WriteLine("Output - {0}", process.StandardOutput.ReadToEnd());
            MessageBox.Show("Loading Security Services...", "IT Team Security Policy", MessageBoxButtons.YesNo, MessageBoxIcon.Question);




        }
    }
}
```
