# C # Tradecraft 

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Diagnostics;

namespace ClickOnce
{
    class Program
    {
        static void Main(string[] args)
        {

            using var process = new Process();

            process.StartInfo.FileName = "notepad.exe";
            process.StartInfo.Arguments = @"C:\Users\NyaMeeEain\Desktop\acl.txt";
            process.Start();
        }
    }
}
```
```
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Diagnostics;

namespace ClickOnce
{
    class Program
    {
        static void Main(string[] args)
        {

            var si = new ProcessStartInfo
            {
                FileName = @"C:\Windows\System32\notepad.exe",
                Arguments = @"C:\Users\NyaMeeEain\Desktop\test.txt"
            };

            var proc = new Process
            {
                StartInfo = si
            };

            proc.Start();
            proc.WaitForExit();
            proc.Dispose();
        }
    }
}

```
