```
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Runtime.InteropServices;
using System.Text;
using System.Threading.Tasks;
namespace DemoAssembly
{
    public class Exports
    {
        [DllExport("Start", CallingConvention = CallingConvention.Cdecl)]
        public static void Start(IntPtr hwnd, IntPtr hinst, string lpszCmdLine, int nCmdShow)
        {
            new DemoClass();
        }
    }
    public class DemoClass
    {
            class Program
        {
            static void Main(string[] args)
            {
                var Execution = new ProcessStartInfo
                {
                    FileName = @"C:\Windows\System32\notepad.exe",
                    Arguments = @"C:\Users\NyaMeeEain\Desktop\test.txt"
                };
                var proc = new Process
                {
                    StartInfo = Execution
                };
                proc.Start();
                proc.WaitForExit();
                proc.Dispose();
            }
        }
    }
}
```
