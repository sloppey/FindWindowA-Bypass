# FindWindowA-Bypass
Bypasses ROBLOX's check inside FindWindowA

When calling FindWindowA, roblox shuts you down due to a certain check inside.
This is very easy to bypass, as all they do is something similar to this.

```C++
HWND FindWindowA(LPCSTR, LPCSTR){
//jmp _check

//findwindow
//return hwnd;
}
```

Bypass:
```C++
 void FindWindowA_Bypass(){
	 DWORD old;
	 VirtualProtect((LPVOID)&FindWindowA, 1, PAGE_EXECUTE_READWRITE, &old);
	 *(char*)&FindWindowA = 0x90;
	 VirtualProtect((LPVOID)&FindWindowA, 1, old, &old);
 }
```
this sets the instruction at the address to FindWindowA to a nop.
which makes it look something like
```C++
HWND FindWindowA(LPCSTR, LPCSTR){
//nop
//findwindow
//return hwnd;
}
```




