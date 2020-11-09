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
