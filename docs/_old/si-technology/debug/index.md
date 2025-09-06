---
title: "[DEBUG사례] BSOD / nt!ObpCaptureHandleInformation"
date: "No Date"
---

[DEBUG사례] BSOD / nt!ObpCaptureHandleInformation
===============================================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2019년 2월 25일

#### ▶ 실제 사례

1: kd> vertarget  
Windows 7 Kernel Version 7601 (Service Pack 1) MP (4 procs) Free x64  
Product: WinNt, suite: TerminalServer SingleUserTS  
Built by: 7601.24231.amd64fre.win7sp1\_ldr.180810-0600  
Machine Name:”VMOA2024974-01″  
Kernel base = 0xfffff800`01a1f000 PsLoadedModuleList = 0xfffff800`01c59c90  
Debug session time: Thu Jan 17 10:58:58.567 2019 (UTC + 9:00)  
System Uptime: 3 days 0:32:26.132

1: kd> !sysinfo machineid  
Machine ID Information [From Smbios 2.7, DMIVersion 0, Size=10220]  
BiosMajorRelease = 4  
BiosMinorRelease = 6  
FirmwareMajorRelease = 0  
FirmwareMinorRelease = 0  
BiosVendor = Phoenix Technologies LTD  
BiosVersion = 6.00  
BiosReleaseDate = 04/05/2016  
SystemManufacturer = VMware, Inc.  
SystemProductName = VMware Virtual Platform  
SystemVersion = None  
BaseBoardManufacturer = Intel Corporation  
BaseBoardProduct = 440BX Desktop Reference Platform  
BaseBoardVersion = None

1: kd> !cpuinfo  
CP F/M/S Manufacturer MHz PRCB Signature MSR 8B Signature Features  
0 6,79,1 GenuineIntel 2594 0b00002100000000 31193ffe  
1 6,79,1 GenuineIntel 2594 0b00002100000000 31193ffe  
2 6,79,1 GenuineIntel 2593 0b00002100000000 31193ffe  
3 6,79,1 GenuineIntel 2594 0b00002100000000 31193ffe  
Cached Update Signature 0b00002100000000  
Initial Update Signature 0b00002100000000

1: kd> !vm  
\*\*\* Virtual Memory Usage \*\*\*  
Physical Memory: 2097038 ( 8388152 Kb)  
Page File: \??\C:\pagefile.sys  
Current: 8695352 Kb Free Space: 5968068 Kb  
Minimum: 8695352 Kb Maximum: 25164456 Kb  
Unimplemented error for MiSystemVaTypeCount  
Available Pages: 791288 ( 3165152 Kb)  
ResAvail Pages: 1965535 ( 7862140 Kb)  
Locked IO Pages: 0 ( 0 Kb)  
Free System PTEs: 33564273 ( 134257092 Kb)  
Modified Pages: 12771 ( 51084 Kb)  
Modified PF Pages: 12753 ( 51012 Kb)  
NonPagedPool Usage: 29559056 ( 118236224 Kb)  
NonPagedPoolNx Usage: 32908 ( 131632 Kb)  
NonPagedPool Max: 1561080 ( 6244320 Kb)  
\*\*\*\*\*\*\*\*\*\* Excessive NonPaged Pool Usage \*\*\*\*\*  
PagedPool 0 Usage: 58975 ( 235900 Kb)  
PagedPool 1 Usage: 12996 ( 51984 Kb)  
PagedPool 2 Usage: 4998 ( 19992 Kb)  
PagedPool 3 Usage: 4917 ( 19668 Kb)  
PagedPool 4 Usage: 5068 ( 20272 Kb)  
PagedPool Usage: 86954 ( 347816 Kb)  
PagedPool Maximum: 33554432 ( 134217728 Kb)  
Session Commit: 25872 ( 103488 Kb)  
Shared Commit: 604170 ( 2416680 Kb)  
Special Pool: 0 ( 0 Kb)  
Shared Process: 22548 ( 90192 Kb)  
PagedPool Commit: 87018 ( 348072 Kb)  
Driver Commit: 23265 ( 93060 Kb)  
Committed pages: 2062764 ( 8251056 Kb)  
Commit limit: 4270402 ( 17081608 Kb)

1: kd> !analyze -v  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\* \*  
\* Bugcheck Analysis \*  
\* \*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

SYSTEM\_SERVICE\_EXCEPTION (3b)  
An exception happened while executing a system service routine.  
Arguments:  
Arg1: 00000000c0000005, Exception code that caused the bugcheck  
Arg2: fffff80001dc87b8, Address of the instruction which caused the bugcheck  
Arg3: fffff8801b90cc20, Address of the context record for the exception that caused the bugcheck  
Arg4: 0000000000000000, zero.

Debugging Details:  
——————

EXCEPTION\_CODE: (NTSTATUS) 0xc0000005 – 0x%08lx

FAULTING\_IP:  
nt!ObpCaptureHandleInformation+68  
fffff800`01dc87b8 8a4128 mov al,byte ptr [rcx+28h]

CONTEXT: fffff8801b90cc20 — (.cxr 0xfffff8801b90cc20)  
rax=000000000000002d rbx=00000000000004cc rcx=0000000000000000  
rdx=fffff88016992fb0 rsi=fffff8a00ebb0330 rdi=0000000000237578  
rip=fffff80001dc87b8 rsp=fffff8801b90d5f8 rbp=0000000000000000  
r8=fffff8a00ebb0330 r9=fffffa80085e8a50 r10=00000000000d0f88  
r11=fffff8801b90d688 r12=fffff8a00f2fd320 r13=000000000359abd0  
r14=fffff880168c2040 r15=fffff8801b90d6b8  
iopl=0 nv up ei pl zr na po nc  
cs=0010 ss=0018 ds=002b es=002b fs=0053 gs=002b efl=00010246  
nt!ObpCaptureHandleInformation+0x68:  
fffff800`01dc87b8 8a4128 mov al,byte ptr [rcx+28h] ds:002b:00000000`00000028=??  
Resetting default scope

DEFAULT\_BUCKET\_ID: VISTA\_DRIVER\_FAULT

BUGCHECK\_STR: 0x3B

PROCESS\_NAME: MiniCtrl.exe

CURRENT\_IRQL: 0

LAST\_CONTROL\_TRANSFER: from fffff80001e53b8d to fffff80001dc87b8

STACK\_TEXT:  
fffff880`1b90d5f8 fffff800`01e53b8d : 00000000`000004cc fffffa80`0c6d61f0 00000000`00000001 00000000`00000238 : nt!ObpCaptureHandleInformation+0x68  
fffff880`1b90d600 fffff800`01e54267 : fffff880`1b90d730 fffff880`16992fb0 00000000`00237578 00000000`00000001 : nt!ExSnapShotHandleTables+0x10d  
fffff880`1b90d680 fffff800`01edfaf5 : fffff880`1b90d730 00000000`000d0f88 00000000`00237578 00000000`00237578 : nt!ObGetHandleInformation+0x37  
fffff880`1b90d6b0 fffff800`01ef4e5b : 00000000`00000000 fffffa80`0d9a9f00 fffff880`168c2040 fffffa80`0c6d5000 : nt!ExpGetHandleInformation+0x55  
fffff880`1b90d6f0 fffff800`01d6aa25 : 00000000`03970040 00000000`00237578 00000000`03970040 00000000`00023758 : nt!ExpQuerySystemInformation+0x17eb  
fffff880`1b90daa0 fffff800`01ac09d3 : 00000000`00000001 00000000`03970038 00000000`00000001 00000000`00000000 : nt!NtQuerySystemInformation+0x4d  
fffff880`1b90dae0 00000000`77899bea : 00000001`4005708d 00000000`c0000004 00000000`0415c920 00000000`00010000 : nt!KiSystemServiceCopyEnd+0x13  
00000000`0359ab88 00000001`4005708d : 00000000`c0000004 00000000`0415c920 00000000`00010000 00000000`00237578 : ntdll!ZwQuerySystemInformation+0xa  
00000000`0359ab90 00000001`400579f0 : 00000000`00237578 00000000`00000001 00000000`0037f980 00000000`00000000 : MiniCtrl+0x5708d  
00000000`0359abd0 00000001`4003a1c1 : ffffffff`00000fb4 00000000`637b0fe2 00000000`0359f9c8 00000000`00000028 : MiniCtrl+0x579f0  
00000000`0359b0f0 00000001`400264ec : 00000000`0037f980 00000000`0359b1d0 00000000`00000001 00000000`00000000 : MiniCtrl+0x3a1c1  
00000000`0359b130 00000000`00000000 : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000000 : MiniCtrl+0x264ec

FOLLOWUP\_IP:  
nt!ObpCaptureHandleInformation+68  
fffff800`01dc87b8 8a4128 mov al,byte ptr [rcx+28h]

SYMBOL\_STACK\_INDEX: 0

SYMBOL\_NAME: nt!ObpCaptureHandleInformation+68

FOLLOWUP\_NAME: MachineOwner

MODULE\_NAME: nt

IMAGE\_NAME: ntkrnlmp.exe

DEBUG\_FLR\_IMAGE\_TIMESTAMP: 5b6dabb8

STACK\_COMMAND: .cxr 0xfffff8801b90cc20 ; kb

FAILURE\_BUCKET\_ID: X64\_0x3B\_nt!ObpCaptureHandleInformation+68

BUCKET\_ID: X64\_0x3B\_nt!ObpCaptureHandleInformation+68

Followup: MachineOwner

1: kd> !ready  
No ready threads found.

1: kd> !standby  
Process PID Thread Id Pri Base Pri Affinity Next CPU Ideal CPU CSwitches User Kernel State Time Reason  
================ ==== ================ === === ======== ======== ======== ========= ========= ==== ====== ======= ==== =======  
iexplore.exe \*32 1d78 fffffa800b1bab50 8a4 12 8 15 3 1 2623 78ms 94ms Standby 15ms WrQueue

1: kd> !mex.t fffffa800b1bab50  
Process Thread CID TEB UserTime KernelTime ContextSwitches Wait Reason Time State  
iexplore.exe \*32 (fffffa800d848060) fffffa800b1bab50 (E|K|W|R|V) 1d78.8a4 000000007ef5e000 78ms 94ms 2623 WrQueue 15ms Standby on processor 3

1: kd> !tl fffffa800b1bab50  
Warning! Zombie process(es) detected (not displayed). Count: 87 [zombie report]

1: kd> !mex.tl -z -r  
Count Name Ses Thd Obj Handles Obj Pointers  
===== ========================== === === =========== ============  
1 BizRCSvr.exe 1 0 1 2  
1 CubeU.exe 2 0 0 1  
1 CubeU.exe 3 0 0 1  
1 DSH\_Inj64.exe 1 0 1 1  
1 DSU\_LiveUpdate64.exe 1 0 1 2  
1 EXCEL.EXE 1 0 2 2  
1 EXCEL.EXE 1 0 3 3  
1 notepad.exe 1 0 1 1  
1 notepad.exe 1 0 3 3  
1 notepad.exe 1 0 9 9  
1 POWERPNT.EXE 1 0 2 2  
1 software\_reporter\_tool.exe 1 0 0 1  
1 SWClient.exe 1 0 2 4  
1 syscfgdy.exe 1 0 1 2  
1 TDepend.exe 1 0 1 2  
2 CubeU.exe 4 0 0 1  
2 POWERPNT.EXE 1 0 3 3  
2 SWClient.exe 1 0 1 2  
2 V3Exec.exe 1 0 1 1  
3 CubeU.exe 1 0 0 1  
3 iexplore.exe 1 0 1 1  
3 TDepend64.exe 1 0 1 2  
4 CARC.exe 1 0 1 1  
4 CARCHMx32.exe 1 0 1 1  
4 CARCHMx64.exe 1 0 1 1  
4 syscfg64.exe 1 0 1 1  
5 EXCEL.EXE 1 0 1 1  
7 SWClient.exe 1 0 2 3  
27 POWERPNT.EXE 1 0 1 1  
===== ========================== === === =========== ============  
Count Name Ses Thd Obj Handles Obj Pointers  
87

1: kd> !mex.tasklist -z  
PID Address Name Ses Thd Obj Handles Obj Pointers  
============== ================ ========================== === === =========== ============  
0x4ec 0n1260 fffffa800be8f110 SWClient.exe 1 0 2 3  
0xb04 0n2820 fffffa8006d9d350 CubeU.exe 1 0 0 1  
0x9d4 0n2516 fffffa800befd710 SWClient.exe 1 0 2 3  
0xbe8 0n3048 fffffa800be99890 SWClient.exe 1 0 2 3  
0x91c 0n2332 fffffa800bf07b00 SWClient.exe 1 0 2 3  
0xc34 0n3124 fffffa800a2736f0 SWClient.exe 1 0 1 2  
0x1640 0n5696 fffffa800719fb00 SWClient.exe 1 0 1 2  
0x1a8c 0n6796 fffffa80070fbb00 SWClient.exe 1 0 2 3  
0x428 0n1064 fffffa8007f508f0 CARC.exe 1 0 1 1  
0x1af8 0n6904 fffffa8007371b00 CARCHMx64.exe 1 0 1 1  
0x1c84 0n7300 fffffa8007082b00 CARCHMx32.exe 1 0 1 1  
0x1ca0 0n7328 fffffa800752f060 DSH\_Inj64.exe 1 0 1 1  
0x1d00 0n7424 fffffa8007dd3b00 syscfg64.exe 1 0 1 1  
0x20f0 0n8432 fffffa8008d93720 BizRCSvr.exe 1 0 1 2  
0xcc8 0n3272 fffffa80073d2060 DSU\_LiveUpdate64.exe 1 0 1 2  
0x2588 0n9608 fffffa800d3c46a0 notepad.exe 1 0 9 9  
0x2780 0n10112 fffffa800e1e3060 notepad.exe 1 0 3 3  
0x28dc 0n10460 fffffa8008380060 POWERPNT.EXE 1 0 1 1  
0x1f84 0n8068 fffffa800e2c0060 POWERPNT.EXE 1 0 1 1  
0xac8 0n2760 fffffa800e376060 POWERPNT.EXE 1 0 2 2  
0x29a8 0n10664 fffffa800da15b00 EXCEL.EXE 1 0 1 1  
0x2490 0n9360 fffffa800734bb00 EXCEL.EXE 1 0 1 1  
0x26b4 0n9908 fffffa800e212800 POWERPNT.EXE 1 0 1 1  
0x5ac 0n1452 fffffa800e3e3060 EXCEL.EXE 1 0 2 2  
0x23c0 0n9152 fffffa800e499060 EXCEL.EXE 1 0 3 3  
0x2884 0n10372 fffffa800eab5060 SWClient.exe 1 0 2 3  
0x28f8 0n10488 fffffa800cc5fb00 CubeU.exe 2 0 0 1  
0x1b7c 0n7036 fffffa800a1d4680 CARC.exe 1 0 1 1  
0x284c 0n10316 fffffa800abe6b00 CARCHMx64.exe 1 0 1 1  
0x2624 0n9764 fffffa8007120340 CARCHMx32.exe 1 0 1 1  
0x24e0 0n9440 fffffa800cc31350 syscfg64.exe 1 0 1 1  
0x134 0n308 fffffa80083d0460 SWClient.exe 1 0 2 3  
0x2398 0n9112 fffffa800de6b890 CubeU.exe 1 0 0 1  
0x17ac 0n6060 fffffa800975a060 CARC.exe 1 0 1 1  
0x26f0 0n9968 fffffa800ec62060 CARCHMx64.exe 1 0 1 1  
0x900 0n2304 fffffa800a2cd5b0 CARCHMx32.exe 1 0 1 1  
0x27e0 0n10208 fffffa8007019b00 syscfg64.exe 1 0 1 1  
0x2a28 0n10792 fffffa800e518870 EXCEL.EXE 1 0 1 1  
0xe48 0n3656 fffffa800cc07060 POWERPNT.EXE 1 0 1 1  
0x1a74 0n6772 fffffa800e448b00 POWERPNT.EXE 1 0 1 1  
0xfd4 0n4052 fffffa800cf0aa50 POWERPNT.EXE 1 0 1 1  
0x2bd8 0n11224 fffffa800d7e6960 POWERPNT.EXE 1 0 1 1  
0x2a9c 0n10908 fffffa800ce45b00 POWERPNT.EXE 1 0 1 1  
0x16a8 0n5800 fffffa800dd7b700 POWERPNT.EXE 1 0 3 3  
0x2904 0n10500 fffffa800d905b00 POWERPNT.EXE 1 0 1 1  
0x2d58 0n11608 fffffa800747b490 POWERPNT.EXE 1 0 1 1  
0x2a18 0n10776 fffffa8009d93b00 CubeU.exe 3 0 0 1  
0x2ff8 0n12280 fffffa800714c370 SWClient.exe 1 0 2 4  
0x27dc 0n10204 fffffa80080c3b00 CubeU.exe 1 0 0 1  
0x17e8 0n6120 fffffa800db68b00 CARC.exe 1 0 1 1  
0xa48 0n2632 fffffa800cf726b0 CARCHMx64.exe 1 0 1 1  
0xf74 0n3956 fffffa80075d82d0 CARCHMx32.exe 1 0 1 1  
0x1870 0n6256 fffffa800a0dd480 syscfg64.exe 1 0 1 1  
0x884 0n2180 fffffa800824c060 TDepend.exe 1 0 1 2  
0x1b1c 0n6940 fffffa800d386aa0 TDepend64.exe 1 0 1 2  
0x2308 0n8968 fffffa800c4cdb00 TDepend64.exe 1 0 1 2  
0x2440 0n9280 fffffa800e3b5b00 TDepend64.exe 1 0 1 2  
0x2170 0n8560 fffffa8007e9b900 EXCEL.EXE 1 0 1 1  
0x27b0 0n10160 fffffa800d6fab00 notepad.exe 1 0 1 1  
0x2808 0n10248 fffffa800832e060 POWERPNT.EXE 1 0 1 1  
0x31b0 0n12720 fffffa80082645f0 iexplore.exe 1 0 1 1  
0x860 0n2144 fffffa800db47510 POWERPNT.EXE 1 0 1 1  
0x16b4 0n5812 fffffa800a079ad0 POWERPNT.EXE 1 0 1 1  
0x1970 0n6512 fffffa800e158b00 POWERPNT.EXE 1 0 1 1  
0x33b4 0n13236 fffffa800e213b00 POWERPNT.EXE 1 0 1 1  
0x33cc 0n13260 fffffa800ea2c060 POWERPNT.EXE 1 0 1 1  
0x242c 0n9260 fffffa800ad7f060 POWERPNT.EXE 1 0 1 1  
0x2d74 0n11636 fffffa800d2a1940 POWERPNT.EXE 1 0 1 1  
0x147c 0n5244 fffffa800ebd7480 EXCEL.EXE 1 0 1 1  
0x3230 0n12848 fffffa800d8b41b0 POWERPNT.EXE 1 0 1 1  
0x3228 0n12840 fffffa800e4d9b00 POWERPNT.EXE 1 0 1 1  
0x2450 0n9296 fffffa800abd45b0 POWERPNT.EXE 1 0 1 1  
0x1bbc 0n7100 fffffa800b55c9d0 CubeU.exe 4 0 0 1  
0x2f60 0n12128 fffffa800d7c68f0 CubeU.exe 4 0 0 1  
0x100 0n256 fffffa800e5ccb00 syscfgdy.exe 1 0 1 2  
0x3240 0n12864 fffffa800a319720 iexplore.exe 1 0 1 1  
0x2b7c 0n11132 fffffa800e29fb00 iexplore.exe 1 0 1 1  
0x1f10 0n7952 fffffa800e9cdb00 POWERPNT.EXE 1 0 3 3  
0x2fbc 0n12220 fffffa8009d4fb00 POWERPNT.EXE 1 0 1 1  
0x1ec0 0n7872 fffffa800c66b060 POWERPNT.EXE 1 0 1 1  
0x1be4 0n7140 fffffa8007db0b00 POWERPNT.EXE 1 0 1 1  
0xaf4 0n2804 fffffa800ea73b00 POWERPNT.EXE 1 0 1 1  
0x1a58 0n6744 fffffa800df86b00 POWERPNT.EXE 1 0 1 1  
0x23c8 0n9160 fffffa800d6c26f0 POWERPNT.EXE 1 0 1 1  
0x3130 0n12592 fffffa800d910300 software\_reporter\_tool.exe 1 0 0 1  
0x2698 0n9880 fffffa800c652060 V3Exec.exe 1 0 1 1  
0x3774 0n14196 fffffa8008164190 V3Exec.exe 1 0 1 1  
============== ================ ========================== === === =========== ============  
PID Address Name Ses Thd Obj Handles Obj Pointers

Priority:  
Current Base Decrement ForegroundBoost IO Page  
12 8 0 2 0 5

# Child-SP Return Call Site  
0 fffff880147ff6c0 fffff80001a57f32 nt!KiSwapContext+0x7a  
1 fffff880147ff800 fffff80001a592b3 nt!KiCommitThreadWait+0x1d2  
2 fffff880147ff890 fffff80001d0b6bc nt!KeRemoveQueueEx+0x323  
3 fffff880147ff950 fffff80001a5d3c5 nt!IoRemoveIoCompletion+0x5c  
4 fffff880147ff9e0 fffff80001ac09d3 nt!NtWaitForWorkViaWorkerFactory+0x285  
5 fffff880147ffae0 000000007789b18a nt!KiSystemServiceCopyEnd+0x13  
0 000000001015fd98 0000000077a3fa9e ntdll\_779f0000!ZwWaitForWorkViaWorkerFactory+0x12  
1 000000001015fda0 00000000774a343d ntdll\_779f0000!TppWorkerThread+0x209  
2 000000001015fef0 0000000077a29802 kernel32!BaseThreadInitThunk+0xe  
3 000000001015fefc 0000000077a297d5 ntdll\_779f0000!\_\_RtlUserThreadStart+0x70  
4 000000001015ff3c 0000000000000000 ntdll\_779f0000!\_RtlUserThreadStart+0x1b

1: kd> !cpu  
Process PID Thread Id Pri Base Pri Next CPU CSwitches User Kernel State Time Reason  
================ ==== ================ ==== === ======== ======== ========= ============ =============== ======= =============== =============  
Idle 0 fffff80001c141c0 0 16 0 0 553290675 0 2d.09:23:53.324 Running 3d.00:32:26.126 Executive  
MiniCtrl.exe 2924 fffffa800d9a9b50 1474 9 8 1 155 0 31ms Running 0 WrDispatchInt  
iexplore.exe \*32 1d78 fffffa800da30b50 27ac 11 8 2 70840493 2h:38:23.643 37m:26.789 Running 0 WrUserRequest  
Idle 0 fffff8800210b140 0 16 0 3 539279526 0 2d.14:19:12.729 Running 3d.00:32:26.126 Executive

1: kd> !mex.t fffffa800d9a9b50  
Process Thread CID TEB UserTime KernelTime ContextSwitches Wait Reason Time State  
MiniCtrl.exe (fffffa80095ed060) fffffa800d9a9b50 (E|K|W|R|V) 2924.1474 000007fffff7e000 0 31ms 155 WrDispatchInt 0 Running on processor 1

Priority:  
Current Base Decrement ForegroundBoost IO Page  
9 8 0 0 0 5

# Child-SP Return Call Site  
0 fffff8801b90c358 fffff80001ac0d69 nt!KeBugCheckEx  
1 fffff8801b90c360 fffff80001ac047c nt!KiBugCheckDispatch+0x69  
2 fffff8801b90c4a0 fffff80001ab9cdd nt!KiSystemServiceHandler+0x7c  
3 fffff8801b90c4e0 fffff80001a3b445 nt!RtlpExecuteHandlerForException+0xd  
4 fffff8801b90c510 fffff80001b9984e nt!RtlDispatchException+0x415  
5 fffff8801b90cbf0 fffff80001ac0e42 nt!KiDispatchException+0x17e  
6 fffff8801b90d280 fffff80001abeb62 nt!KiExceptionDispatch+0xc2  
7 fffff8801b90d460 fffff80001dc87b8 nt!KiPageFault+0x422  
8 fffff8801b90d5f8 fffff80001e53b8d nt!ObpCaptureHandleInformation+0x68  
9 fffff8801b90d600 fffff80001e54267 nt!ExSnapShotHandleTables+0x10d  
a fffff8801b90d680 fffff80001edfaf5 nt!ObGetHandleInformation+0x37  
b fffff8801b90d6b0 fffff80001ef4e5b nt!ExpGetHandleInformation+0x55  
c fffff8801b90d6f0 fffff80001d6aa25 nt!ExpQuerySystemInformation+0x17eb  
d fffff8801b90daa0 fffff80001ac09d3 nt!NtQuerySystemInformation+0x4d  
e fffff8801b90dae0 0000000077899bea nt!KiSystemServiceCopyEnd+0x13  
f 000000000359ab88 000000014005708d ntdll!ZwQuerySystemInformation+0xa  
10 000000000359ab90 00000001400579f0 MiniCtrl+0x5708d  
11 000000000359abd0 000000014003a1c1 MiniCtrl+0x579f0  
12 000000000359b0f0 00000001400264ec MiniCtrl+0x3a1c1  
13 000000000359b130 0000000000000000 MiniCtrl+0x264ec

1: kd> !mex.p 0xfffffa80095ed060  
Name Address Ses PID Parent PEB Create Time Mods Handle Thrd User Name  
============ ======================== === ============== ============== ================ ========================== ==== ====== ==== ===============  
MiniCtrl.exe fffffa80095ed060 (E|K|O) 1 2924 (0n10532) 2d90 (0n11664) 000007fffffd4000 01-15-2019 07:10:47.095 오후 81 277 24 HYNIXAD\2024974

Command Line: “C:\Windows\system32\MiniCtrl.exe” /L

Memory Details:

VM Peak Work Set Commit Size  
========= ========= ======== ===========  
145.35 MB 172.57 MB 34.88 MB 17.6 MB

0: kd> lmvm minictrl  
start end module name  
00000001`40000000 00000001`405ec000 MiniCtrl (no symbols)  
Loaded symbol image file: MiniCtrl.exe  
Image path: C:\Windows\system32\MiniCtrl.exe  
Image name: MiniCtrl.exe  
Timestamp: Thu Dec 06 10:40:45 2018 (5C087E1D)  
CheckSum: 000EDA25  
ImageSize: 005EC000  
File version: 1.2.0.87  
Product version: 1.2.0.87  
File flags: 0 (Mask 3F)  
File OS: 4 Unknown Win32  
File type: 1.0 App  
File date: 00000000.00000000  
Translations: 0409.04b0  
CompanyName: ITM System  
ProductName: MiniCtrl Application  
InternalName: MiniCtrl  
OriginalFilename: MiniCtrl.EXE  
ProductVersion: 1.2.0.87  
FileVersion: 1.2.0.87  
FileDescription: MiniCtrl MFC Application  
LegalCopyright: Copyright (C) 2011 ITM Syste

```html
<article class="post-576 post type-post status-publish format-standard hentry category-debug"><div class="post-inner group">
<h1 class="post-title entry-title">[DEBUG사례] BSOD / nt!ObpCaptureHandleInformation</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2019년 2월 25일">2019년 2월 25일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<h4 align="left"><span lang="EN-US">▶ </span><span lang="EN-US">실제 사례</span></h4>
<p>1: kd&gt; vertarget<br/>
Windows 7 Kernel Version 7601 (Service Pack 1) MP (4 procs) Free x64<br/>
Product: WinNt, suite: TerminalServer SingleUserTS<br/>
Built by: 7601.24231.amd64fre.win7sp1_ldr.180810-0600<br/>
Machine Name:”VMOA2024974-01″<br/>
Kernel base = 0xfffff800`01a1f000 PsLoadedModuleList = 0xfffff800`01c59c90<br/>
Debug session time: Thu Jan 17 10:58:58.567 2019 (UTC + 9:00)<br/>
System Uptime: 3 days 0:32:26.132</p>
<p>1: kd&gt; !sysinfo machineid<br/>
Machine ID Information [From Smbios 2.7, DMIVersion 0, Size=10220]<br/>
BiosMajorRelease = 4<br/>
BiosMinorRelease = 6<br/>
FirmwareMajorRelease = 0<br/>
FirmwareMinorRelease = 0<br/>
BiosVendor = Phoenix Technologies LTD<br/>
BiosVersion = 6.00<br/>
BiosReleaseDate = 04/05/2016<br/>
SystemManufacturer = VMware, Inc.<br/>
SystemProductName = VMware Virtual Platform<br/>
SystemVersion = None<br/>
BaseBoardManufacturer = Intel Corporation<br/>
BaseBoardProduct = 440BX Desktop Reference Platform<br/>
BaseBoardVersion = None</p>
<p>1: kd&gt; !cpuinfo<br/>
CP F/M/S Manufacturer MHz PRCB Signature MSR 8B Signature Features<br/>
0 6,79,1 GenuineIntel 2594 0b00002100000000 31193ffe<br/>
1 6,79,1 GenuineIntel 2594 0b00002100000000 31193ffe<br/>
2 6,79,1 GenuineIntel 2593 0b00002100000000 31193ffe<br/>
3 6,79,1 GenuineIntel 2594 0b00002100000000 31193ffe<br/>
Cached Update Signature 0b00002100000000<br/>
Initial Update Signature 0b00002100000000</p>
<p>1: kd&gt; !vm<br/>
*** Virtual Memory Usage ***<br/>
Physical Memory: 2097038 ( 8388152 Kb)<br/>
Page File: \??\C:\pagefile.sys<br/>
Current: 8695352 Kb Free Space: 5968068 Kb<br/>
Minimum: 8695352 Kb Maximum: 25164456 Kb<br/>
Unimplemented error for MiSystemVaTypeCount<br/>
Available Pages: 791288 ( 3165152 Kb)<br/>
ResAvail Pages: 1965535 ( 7862140 Kb)<br/>
Locked IO Pages: 0 ( 0 Kb)<br/>
Free System PTEs: 33564273 ( 134257092 Kb)<br/>
Modified Pages: 12771 ( 51084 Kb)<br/>
Modified PF Pages: 12753 ( 51012 Kb)<br/>
NonPagedPool Usage: 29559056 ( 118236224 Kb)<br/>
NonPagedPoolNx Usage: 32908 ( 131632 Kb)<br/>
NonPagedPool Max: 1561080 ( 6244320 Kb)<br/>
********** Excessive NonPaged Pool Usage *****<br/>
PagedPool 0 Usage: 58975 ( 235900 Kb)<br/>
PagedPool 1 Usage: 12996 ( 51984 Kb)<br/>
PagedPool 2 Usage: 4998 ( 19992 Kb)<br/>
PagedPool 3 Usage: 4917 ( 19668 Kb)<br/>
PagedPool 4 Usage: 5068 ( 20272 Kb)<br/>
PagedPool Usage: 86954 ( 347816 Kb)<br/>
PagedPool Maximum: 33554432 ( 134217728 Kb)<br/>
Session Commit: 25872 ( 103488 Kb)<br/>
Shared Commit: 604170 ( 2416680 Kb)<br/>
Special Pool: 0 ( 0 Kb)<br/>
Shared Process: 22548 ( 90192 Kb)<br/>
PagedPool Commit: 87018 ( 348072 Kb)<br/>
Driver Commit: 23265 ( 93060 Kb)<br/>
Committed pages: 2062764 ( 8251056 Kb)<br/>
Commit limit: 4270402 ( 17081608 Kb)</p>
<p>1: kd&gt; !analyze -v<br/>
*******************************************************************************<br/>
* *<br/>
* Bugcheck Analysis *<br/>
* *<br/>
*******************************************************************************</p>
<p>SYSTEM_SERVICE_EXCEPTION (3b)<br/>
An exception happened while executing a system service routine.<br/>
Arguments:<br/>
Arg1: 00000000c0000005, Exception code that caused the bugcheck<br/>
Arg2: fffff80001dc87b8, Address of the instruction which caused the bugcheck<br/>
Arg3: fffff8801b90cc20, Address of the context record for the exception that caused the bugcheck<br/>
Arg4: 0000000000000000, zero.</p>
<p>Debugging Details:<br/>
——————</p>
<p>EXCEPTION_CODE: (NTSTATUS) 0xc0000005 – 0x%08lx</p>
<p>FAULTING_IP:<br/>
nt!ObpCaptureHandleInformation+68<br/>
fffff800`01dc87b8 8a4128 mov al,byte ptr [rcx+28h]</p>
<p>CONTEXT: fffff8801b90cc20 — (.cxr 0xfffff8801b90cc20)<br/>
rax=000000000000002d rbx=00000000000004cc rcx=0000000000000000<br/>
rdx=fffff88016992fb0 rsi=fffff8a00ebb0330 rdi=0000000000237578<br/>
rip=fffff80001dc87b8 rsp=fffff8801b90d5f8 rbp=0000000000000000<br/>
r8=fffff8a00ebb0330 r9=fffffa80085e8a50 r10=00000000000d0f88<br/>
r11=fffff8801b90d688 r12=fffff8a00f2fd320 r13=000000000359abd0<br/>
r14=fffff880168c2040 r15=fffff8801b90d6b8<br/>
iopl=0 nv up ei pl zr na po nc<br/>
cs=0010 ss=0018 ds=002b es=002b fs=0053 gs=002b efl=00010246<br/>
nt!ObpCaptureHandleInformation+0x68:<br/>
fffff800`01dc87b8 8a4128 mov al,byte ptr [rcx+28h] ds:002b:00000000`00000028=??<br/>
Resetting default scope</p>
<p>DEFAULT_BUCKET_ID: VISTA_DRIVER_FAULT</p>
<p>BUGCHECK_STR: 0x3B</p>
<p>PROCESS_NAME: MiniCtrl.exe</p>
<p>CURRENT_IRQL: 0</p>
<p>LAST_CONTROL_TRANSFER: from fffff80001e53b8d to fffff80001dc87b8</p>
<p>STACK_TEXT:<br/>
fffff880`1b90d5f8 fffff800`01e53b8d : 00000000`000004cc fffffa80`0c6d61f0 00000000`00000001 00000000`00000238 : nt!ObpCaptureHandleInformation+0x68<br/>
fffff880`1b90d600 fffff800`01e54267 : fffff880`1b90d730 fffff880`16992fb0 00000000`00237578 00000000`00000001 : nt!ExSnapShotHandleTables+0x10d<br/>
fffff880`1b90d680 fffff800`01edfaf5 : fffff880`1b90d730 00000000`000d0f88 00000000`00237578 00000000`00237578 : nt!ObGetHandleInformation+0x37<br/>
fffff880`1b90d6b0 fffff800`01ef4e5b : 00000000`00000000 fffffa80`0d9a9f00 fffff880`168c2040 fffffa80`0c6d5000 : nt!ExpGetHandleInformation+0x55<br/>
fffff880`1b90d6f0 fffff800`01d6aa25 : 00000000`03970040 00000000`00237578 00000000`03970040 00000000`00023758 : nt!ExpQuerySystemInformation+0x17eb<br/>
fffff880`1b90daa0 fffff800`01ac09d3 : 00000000`00000001 00000000`03970038 00000000`00000001 00000000`00000000 : nt!NtQuerySystemInformation+0x4d<br/>
fffff880`1b90dae0 00000000`77899bea : 00000001`4005708d 00000000`c0000004 00000000`0415c920 00000000`00010000 : nt!KiSystemServiceCopyEnd+0x13<br/>
00000000`0359ab88 00000001`4005708d : 00000000`c0000004 00000000`0415c920 00000000`00010000 00000000`00237578 : ntdll!ZwQuerySystemInformation+0xa<br/>
00000000`0359ab90 00000001`400579f0 : 00000000`00237578 00000000`00000001 00000000`0037f980 00000000`00000000 : MiniCtrl+0x5708d<br/>
00000000`0359abd0 00000001`4003a1c1 : ffffffff`00000fb4 00000000`637b0fe2 00000000`0359f9c8 00000000`00000028 : MiniCtrl+0x579f0<br/>
00000000`0359b0f0 00000001`400264ec : 00000000`0037f980 00000000`0359b1d0 00000000`00000001 00000000`00000000 : MiniCtrl+0x3a1c1<br/>
00000000`0359b130 00000000`00000000 : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000000 : MiniCtrl+0x264ec</p>
<p>FOLLOWUP_IP:<br/>
nt!ObpCaptureHandleInformation+68<br/>
fffff800`01dc87b8 8a4128 mov al,byte ptr [rcx+28h]</p>
<p>SYMBOL_STACK_INDEX: 0</p>
<p>SYMBOL_NAME: nt!ObpCaptureHandleInformation+68</p>
<p>FOLLOWUP_NAME: MachineOwner</p>
<p>MODULE_NAME: nt</p>
<p>IMAGE_NAME: ntkrnlmp.exe</p>
<p>DEBUG_FLR_IMAGE_TIMESTAMP: 5b6dabb8</p>
<p>STACK_COMMAND: .cxr 0xfffff8801b90cc20 ; kb</p>
<p>FAILURE_BUCKET_ID: X64_0x3B_nt!ObpCaptureHandleInformation+68</p>
<p>BUCKET_ID: X64_0x3B_nt!ObpCaptureHandleInformation+68</p>
<p>Followup: MachineOwner</p>
<p>1: kd&gt; !ready<br/>
No ready threads found.</p>
<p>1: kd&gt; !standby<br/>
Process PID Thread Id Pri Base Pri Affinity Next CPU Ideal CPU CSwitches User Kernel State Time Reason<br/>
================ ==== ================ === === ======== ======== ======== ========= ========= ==== ====== ======= ==== =======<br/>
iexplore.exe *32 1d78 fffffa800b1bab50 8a4 12 8 15 3 1 2623 78ms 94ms Standby 15ms WrQueue</p>
<p>1: kd&gt; !mex.t fffffa800b1bab50<br/>
Process Thread CID TEB UserTime KernelTime ContextSwitches Wait Reason Time State<br/>
iexplore.exe *32 (fffffa800d848060) fffffa800b1bab50 (E|K|W|R|V) 1d78.8a4 000000007ef5e000 78ms 94ms 2623 WrQueue 15ms Standby on processor 3</p>
<p>1: kd&gt; !tl fffffa800b1bab50<br/>
Warning! Zombie process(es) detected (not displayed). Count: 87 [zombie report]</p>
<p>1: kd&gt; !mex.tl -z -r<br/>
Count Name Ses Thd Obj Handles Obj Pointers<br/>
===== ========================== === === =========== ============<br/>
1 BizRCSvr.exe 1 0 1 2<br/>
1 CubeU.exe 2 0 0 1<br/>
1 CubeU.exe 3 0 0 1<br/>
1 DSH_Inj64.exe 1 0 1 1<br/>
1 DSU_LiveUpdate64.exe 1 0 1 2<br/>
1 EXCEL.EXE 1 0 2 2<br/>
1 EXCEL.EXE 1 0 3 3<br/>
1 notepad.exe 1 0 1 1<br/>
1 notepad.exe 1 0 3 3<br/>
1 notepad.exe 1 0 9 9<br/>
1 POWERPNT.EXE 1 0 2 2<br/>
1 software_reporter_tool.exe 1 0 0 1<br/>
1 SWClient.exe 1 0 2 4<br/>
1 syscfgdy.exe 1 0 1 2<br/>
1 TDepend.exe 1 0 1 2<br/>
2 CubeU.exe 4 0 0 1<br/>
2 POWERPNT.EXE 1 0 3 3<br/>
2 SWClient.exe 1 0 1 2<br/>
2 V3Exec.exe 1 0 1 1<br/>
3 CubeU.exe 1 0 0 1<br/>
3 iexplore.exe 1 0 1 1<br/>
3 TDepend64.exe 1 0 1 2<br/>
4 CARC.exe 1 0 1 1<br/>
4 CARCHMx32.exe 1 0 1 1<br/>
4 CARCHMx64.exe 1 0 1 1<br/>
4 syscfg64.exe 1 0 1 1<br/>
5 EXCEL.EXE 1 0 1 1<br/>
7 SWClient.exe 1 0 2 3<br/>
27 POWERPNT.EXE 1 0 1 1<br/>
===== ========================== === === =========== ============<br/>
Count Name Ses Thd Obj Handles Obj Pointers<br/>
87</p>
<p>1: kd&gt; !mex.tasklist -z<br/>
PID Address Name Ses Thd Obj Handles Obj Pointers<br/>
============== ================ ========================== === === =========== ============<br/>
0x4ec 0n1260 fffffa800be8f110 SWClient.exe 1 0 2 3<br/>
0xb04 0n2820 fffffa8006d9d350 CubeU.exe 1 0 0 1<br/>
0x9d4 0n2516 fffffa800befd710 SWClient.exe 1 0 2 3<br/>
0xbe8 0n3048 fffffa800be99890 SWClient.exe 1 0 2 3<br/>
0x91c 0n2332 fffffa800bf07b00 SWClient.exe 1 0 2 3<br/>
0xc34 0n3124 fffffa800a2736f0 SWClient.exe 1 0 1 2<br/>
0x1640 0n5696 fffffa800719fb00 SWClient.exe 1 0 1 2<br/>
0x1a8c 0n6796 fffffa80070fbb00 SWClient.exe 1 0 2 3<br/>
0x428 0n1064 fffffa8007f508f0 CARC.exe 1 0 1 1<br/>
0x1af8 0n6904 fffffa8007371b00 CARCHMx64.exe 1 0 1 1<br/>
0x1c84 0n7300 fffffa8007082b00 CARCHMx32.exe 1 0 1 1<br/>
0x1ca0 0n7328 fffffa800752f060 DSH_Inj64.exe 1 0 1 1<br/>
0x1d00 0n7424 fffffa8007dd3b00 syscfg64.exe 1 0 1 1<br/>
0x20f0 0n8432 fffffa8008d93720 BizRCSvr.exe 1 0 1 2<br/>
0xcc8 0n3272 fffffa80073d2060 DSU_LiveUpdate64.exe 1 0 1 2<br/>
0x2588 0n9608 fffffa800d3c46a0 notepad.exe 1 0 9 9<br/>
0x2780 0n10112 fffffa800e1e3060 notepad.exe 1 0 3 3<br/>
0x28dc 0n10460 fffffa8008380060 POWERPNT.EXE 1 0 1 1<br/>
0x1f84 0n8068 fffffa800e2c0060 POWERPNT.EXE 1 0 1 1<br/>
0xac8 0n2760 fffffa800e376060 POWERPNT.EXE 1 0 2 2<br/>
0x29a8 0n10664 fffffa800da15b00 EXCEL.EXE 1 0 1 1<br/>
0x2490 0n9360 fffffa800734bb00 EXCEL.EXE 1 0 1 1<br/>
0x26b4 0n9908 fffffa800e212800 POWERPNT.EXE 1 0 1 1<br/>
0x5ac 0n1452 fffffa800e3e3060 EXCEL.EXE 1 0 2 2<br/>
0x23c0 0n9152 fffffa800e499060 EXCEL.EXE 1 0 3 3<br/>
0x2884 0n10372 fffffa800eab5060 SWClient.exe 1 0 2 3<br/>
0x28f8 0n10488 fffffa800cc5fb00 CubeU.exe 2 0 0 1<br/>
0x1b7c 0n7036 fffffa800a1d4680 CARC.exe 1 0 1 1<br/>
0x284c 0n10316 fffffa800abe6b00 CARCHMx64.exe 1 0 1 1<br/>
0x2624 0n9764 fffffa8007120340 CARCHMx32.exe 1 0 1 1<br/>
0x24e0 0n9440 fffffa800cc31350 syscfg64.exe 1 0 1 1<br/>
0x134 0n308 fffffa80083d0460 SWClient.exe 1 0 2 3<br/>
0x2398 0n9112 fffffa800de6b890 CubeU.exe 1 0 0 1<br/>
0x17ac 0n6060 fffffa800975a060 CARC.exe 1 0 1 1<br/>
0x26f0 0n9968 fffffa800ec62060 CARCHMx64.exe 1 0 1 1<br/>
0x900 0n2304 fffffa800a2cd5b0 CARCHMx32.exe 1 0 1 1<br/>
0x27e0 0n10208 fffffa8007019b00 syscfg64.exe 1 0 1 1<br/>
0x2a28 0n10792 fffffa800e518870 EXCEL.EXE 1 0 1 1<br/>
0xe48 0n3656 fffffa800cc07060 POWERPNT.EXE 1 0 1 1<br/>
0x1a74 0n6772 fffffa800e448b00 POWERPNT.EXE 1 0 1 1<br/>
0xfd4 0n4052 fffffa800cf0aa50 POWERPNT.EXE 1 0 1 1<br/>
0x2bd8 0n11224 fffffa800d7e6960 POWERPNT.EXE 1 0 1 1<br/>
0x2a9c 0n10908 fffffa800ce45b00 POWERPNT.EXE 1 0 1 1<br/>
0x16a8 0n5800 fffffa800dd7b700 POWERPNT.EXE 1 0 3 3<br/>
0x2904 0n10500 fffffa800d905b00 POWERPNT.EXE 1 0 1 1<br/>
0x2d58 0n11608 fffffa800747b490 POWERPNT.EXE 1 0 1 1<br/>
0x2a18 0n10776 fffffa8009d93b00 CubeU.exe 3 0 0 1<br/>
0x2ff8 0n12280 fffffa800714c370 SWClient.exe 1 0 2 4<br/>
0x27dc 0n10204 fffffa80080c3b00 CubeU.exe 1 0 0 1<br/>
0x17e8 0n6120 fffffa800db68b00 CARC.exe 1 0 1 1<br/>
0xa48 0n2632 fffffa800cf726b0 CARCHMx64.exe 1 0 1 1<br/>
0xf74 0n3956 fffffa80075d82d0 CARCHMx32.exe 1 0 1 1<br/>
0x1870 0n6256 fffffa800a0dd480 syscfg64.exe 1 0 1 1<br/>
0x884 0n2180 fffffa800824c060 TDepend.exe 1 0 1 2<br/>
0x1b1c 0n6940 fffffa800d386aa0 TDepend64.exe 1 0 1 2<br/>
0x2308 0n8968 fffffa800c4cdb00 TDepend64.exe 1 0 1 2<br/>
0x2440 0n9280 fffffa800e3b5b00 TDepend64.exe 1 0 1 2<br/>
0x2170 0n8560 fffffa8007e9b900 EXCEL.EXE 1 0 1 1<br/>
0x27b0 0n10160 fffffa800d6fab00 notepad.exe 1 0 1 1<br/>
0x2808 0n10248 fffffa800832e060 POWERPNT.EXE 1 0 1 1<br/>
0x31b0 0n12720 fffffa80082645f0 iexplore.exe 1 0 1 1<br/>
0x860 0n2144 fffffa800db47510 POWERPNT.EXE 1 0 1 1<br/>
0x16b4 0n5812 fffffa800a079ad0 POWERPNT.EXE 1 0 1 1<br/>
0x1970 0n6512 fffffa800e158b00 POWERPNT.EXE 1 0 1 1<br/>
0x33b4 0n13236 fffffa800e213b00 POWERPNT.EXE 1 0 1 1<br/>
0x33cc 0n13260 fffffa800ea2c060 POWERPNT.EXE 1 0 1 1<br/>
0x242c 0n9260 fffffa800ad7f060 POWERPNT.EXE 1 0 1 1<br/>
0x2d74 0n11636 fffffa800d2a1940 POWERPNT.EXE 1 0 1 1<br/>
0x147c 0n5244 fffffa800ebd7480 EXCEL.EXE 1 0 1 1<br/>
0x3230 0n12848 fffffa800d8b41b0 POWERPNT.EXE 1 0 1 1<br/>
0x3228 0n12840 fffffa800e4d9b00 POWERPNT.EXE 1 0 1 1<br/>
0x2450 0n9296 fffffa800abd45b0 POWERPNT.EXE 1 0 1 1<br/>
0x1bbc 0n7100 fffffa800b55c9d0 CubeU.exe 4 0 0 1<br/>
0x2f60 0n12128 fffffa800d7c68f0 CubeU.exe 4 0 0 1<br/>
0x100 0n256 fffffa800e5ccb00 syscfgdy.exe 1 0 1 2<br/>
0x3240 0n12864 fffffa800a319720 iexplore.exe 1 0 1 1<br/>
0x2b7c 0n11132 fffffa800e29fb00 iexplore.exe 1 0 1 1<br/>
0x1f10 0n7952 fffffa800e9cdb00 POWERPNT.EXE 1 0 3 3<br/>
0x2fbc 0n12220 fffffa8009d4fb00 POWERPNT.EXE 1 0 1 1<br/>
0x1ec0 0n7872 fffffa800c66b060 POWERPNT.EXE 1 0 1 1<br/>
0x1be4 0n7140 fffffa8007db0b00 POWERPNT.EXE 1 0 1 1<br/>
0xaf4 0n2804 fffffa800ea73b00 POWERPNT.EXE 1 0 1 1<br/>
0x1a58 0n6744 fffffa800df86b00 POWERPNT.EXE 1 0 1 1<br/>
0x23c8 0n9160 fffffa800d6c26f0 POWERPNT.EXE 1 0 1 1<br/>
0x3130 0n12592 fffffa800d910300 software_reporter_tool.exe 1 0 0 1<br/>
0x2698 0n9880 fffffa800c652060 V3Exec.exe 1 0 1 1<br/>
0x3774 0n14196 fffffa8008164190 V3Exec.exe 1 0 1 1<br/>
============== ================ ========================== === === =========== ============<br/>
PID Address Name Ses Thd Obj Handles Obj Pointers</p>
<p>Priority:<br/>
Current Base Decrement ForegroundBoost IO Page<br/>
12 8 0 2 0 5</p>
<p># Child-SP Return Call Site<br/>
0 fffff880147ff6c0 fffff80001a57f32 nt!KiSwapContext+0x7a<br/>
1 fffff880147ff800 fffff80001a592b3 nt!KiCommitThreadWait+0x1d2<br/>
2 fffff880147ff890 fffff80001d0b6bc nt!KeRemoveQueueEx+0x323<br/>
3 fffff880147ff950 fffff80001a5d3c5 nt!IoRemoveIoCompletion+0x5c<br/>
4 fffff880147ff9e0 fffff80001ac09d3 nt!NtWaitForWorkViaWorkerFactory+0x285<br/>
5 fffff880147ffae0 000000007789b18a nt!KiSystemServiceCopyEnd+0x13<br/>
0 000000001015fd98 0000000077a3fa9e ntdll_779f0000!ZwWaitForWorkViaWorkerFactory+0x12<br/>
1 000000001015fda0 00000000774a343d ntdll_779f0000!TppWorkerThread+0x209<br/>
2 000000001015fef0 0000000077a29802 kernel32!BaseThreadInitThunk+0xe<br/>
3 000000001015fefc 0000000077a297d5 ntdll_779f0000!__RtlUserThreadStart+0x70<br/>
4 000000001015ff3c 0000000000000000 ntdll_779f0000!_RtlUserThreadStart+0x1b</p>
<p>1: kd&gt; !cpu<br/>
Process PID Thread Id Pri Base Pri Next CPU CSwitches User Kernel State Time Reason<br/>
================ ==== ================ ==== === ======== ======== ========= ============ =============== ======= =============== =============<br/>
Idle 0 fffff80001c141c0 0 16 0 0 553290675 0 2d.09:23:53.324 Running 3d.00:32:26.126 Executive<br/>
MiniCtrl.exe 2924 fffffa800d9a9b50 1474 9 8 1 155 0 31ms Running 0 WrDispatchInt<br/>
iexplore.exe *32 1d78 fffffa800da30b50 27ac 11 8 2 70840493 2h:38:23.643 37m:26.789 Running 0 WrUserRequest<br/>
Idle 0 fffff8800210b140 0 16 0 3 539279526 0 2d.14:19:12.729 Running 3d.00:32:26.126 Executive</p>
<p>1: kd&gt; !mex.t fffffa800d9a9b50<br/>
Process Thread CID TEB UserTime KernelTime ContextSwitches Wait Reason Time State<br/>
MiniCtrl.exe (fffffa80095ed060) fffffa800d9a9b50 (E|K|W|R|V) 2924.1474 000007fffff7e000 0 31ms 155 WrDispatchInt 0 Running on processor 1</p>
<p>Priority:<br/>
Current Base Decrement ForegroundBoost IO Page<br/>
9 8 0 0 0 5</p>
<p># Child-SP Return Call Site<br/>
0 fffff8801b90c358 fffff80001ac0d69 nt!KeBugCheckEx<br/>
1 fffff8801b90c360 fffff80001ac047c nt!KiBugCheckDispatch+0x69<br/>
2 fffff8801b90c4a0 fffff80001ab9cdd nt!KiSystemServiceHandler+0x7c<br/>
3 fffff8801b90c4e0 fffff80001a3b445 nt!RtlpExecuteHandlerForException+0xd<br/>
4 fffff8801b90c510 fffff80001b9984e nt!RtlDispatchException+0x415<br/>
5 fffff8801b90cbf0 fffff80001ac0e42 nt!KiDispatchException+0x17e<br/>
6 fffff8801b90d280 fffff80001abeb62 nt!KiExceptionDispatch+0xc2<br/>
7 fffff8801b90d460 fffff80001dc87b8 nt!KiPageFault+0x422<br/>
8 fffff8801b90d5f8 fffff80001e53b8d nt!ObpCaptureHandleInformation+0x68<br/>
9 fffff8801b90d600 fffff80001e54267 nt!ExSnapShotHandleTables+0x10d<br/>
a fffff8801b90d680 fffff80001edfaf5 nt!ObGetHandleInformation+0x37<br/>
b fffff8801b90d6b0 fffff80001ef4e5b nt!ExpGetHandleInformation+0x55<br/>
c fffff8801b90d6f0 fffff80001d6aa25 nt!ExpQuerySystemInformation+0x17eb<br/>
d fffff8801b90daa0 fffff80001ac09d3 nt!NtQuerySystemInformation+0x4d<br/>
e fffff8801b90dae0 0000000077899bea nt!KiSystemServiceCopyEnd+0x13<br/>
f 000000000359ab88 000000014005708d ntdll!ZwQuerySystemInformation+0xa<br/>
10 000000000359ab90 00000001400579f0 MiniCtrl+0x5708d<br/>
11 000000000359abd0 000000014003a1c1 MiniCtrl+0x579f0<br/>
12 000000000359b0f0 00000001400264ec MiniCtrl+0x3a1c1<br/>
13 000000000359b130 0000000000000000 MiniCtrl+0x264ec</p>
<p>1: kd&gt; !mex.p 0xfffffa80095ed060<br/>
Name Address Ses PID Parent PEB Create Time Mods Handle Thrd User Name<br/>
============ ======================== === ============== ============== ================ ========================== ==== ====== ==== ===============<br/>
MiniCtrl.exe fffffa80095ed060 (E|K|O) 1 2924 (0n10532) 2d90 (0n11664) 000007fffffd4000 01-15-2019 07:10:47.095 오후 81 277 24 HYNIXAD\2024974</p>
<p>Command Line: “C:\Windows\system32\MiniCtrl.exe” /L</p>
<p>Memory Details:</p>
<p>VM Peak Work Set Commit Size<br/>
========= ========= ======== ===========<br/>
145.35 MB 172.57 MB 34.88 MB 17.6 MB</p>
<p>0: kd&gt; lmvm minictrl<br/>
start end module name<br/>
00000001`40000000 00000001`405ec000 MiniCtrl (no symbols)<br/>
Loaded symbol image file: MiniCtrl.exe<br/>
Image path: C:\Windows\system32\MiniCtrl.exe<br/>
Image name: MiniCtrl.exe<br/>
Timestamp: Thu Dec 06 10:40:45 2018 (5C087E1D)<br/>
CheckSum: 000EDA25<br/>
ImageSize: 005EC000<br/>
File version: 1.2.0.87<br/>
Product version: 1.2.0.87<br/>
File flags: 0 (Mask 3F)<br/>
File OS: 4 Unknown Win32<br/>
File type: 1.0 App<br/>
File date: 00000000.00000000<br/>
Translations: 0409.04b0<br/>
CompanyName: ITM System<br/>
ProductName: MiniCtrl Application<br/>
InternalName: MiniCtrl<br/>
OriginalFilename: MiniCtrl.EXE<br/>
ProductVersion: 1.2.0.87<br/>
FileVersion: 1.2.0.87<br/>
FileDescription: MiniCtrl MFC Application<br/>
LegalCopyright: Copyright (C) 2011 ITM Syste</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
