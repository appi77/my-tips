---
title: "WinDbg 사례"
date: "No Date"
---

WinDbg 사례
=========

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2018년 10월 30일
· Updated 2018년 11월 8일

0:000> !analyze -v

```
*******************************************************************************
* *
* Exception Analysis *
* *
*******************************************************************************

*** WARNING: symbols timestamp is wrong 0x5b079867 0x5b0791e3 for mshtml.dll
*** WARNING: Unable to verify checksum for System.Windows.Forms.ni.dll
*** WARNING: symbols timestamp is wrong 0x4a5be036 0x4a5bdadf for rasman.dll
*** WARNING: symbols timestamp is wrong 0x4a5be0b0 0x4ce7ba42 for winmm.dll
*** ERROR: Symbol file could not be found. Defaulted to export symbols for MKW_M.dll -
*** WARNING: symbols timestamp is wrong 0x5a4db72e 0x5a4db715 for SPF_M.dll
*** ERROR: Symbol file could not be found. Defaulted to export symbols for SPF_M.dll -
*** WARNING: symbols timestamp is wrong 0x5b90f1b6 0x5b90f198 for SPF.dll
*** ERROR: Symbol file could not be found. Defaulted to export symbols for SPF.dll -
Failed calling InternetOpenUrl, GLE=12002

FAULTING_IP:
+c7827e0
00000000`00000000 ?? ???

EXCEPTION_RECORD: ffffffffffffffff -- (.exr 0xffffffffffffffff)
ExceptionAddress: 0000000000000000
ExceptionCode: 80000003 (Break instruction exception)
ExceptionFlags: 00000000
NumberParameters: 0

FAULTING_THREAD: 0000000000001d34

PROCESS_NAME: CubeDisk.exe

OVERLAPPED_MODULE: Address regions for 'DWrite' and 'msls31' overlap

ERROR_CODE: (NTSTATUS) 0x80000003 - {

EXCEPTION_CODE: (HRESULT) 0x80000003 (2147483651) - .

MOD_LIST: 

NTGLOBALFLAG: 0

APPLICATION_VERIFIER_FLAGS: 0

MANAGED_STACK: !dumpstack -EE
No export dumpstack found

ADDITIONAL_DEBUG_TEXT: Followup set based on attribute [Is_ChosenCrashFollowupThread] from Frame:[0] on thread:[PSEUDO_THREAD]

LAST_CONTROL_TRANSFER: from 0000000074792dbf to 0000000074792e09

BUGCHECK_STR: APPLICATION_FAULT_STACKIMMUNE_NOSOS

PRIMARY_PROBLEM_CLASS: STACKIMMUNE

DEFAULT_BUCKET_ID: STACKIMMUNE

STACK_TEXT:
00000000`00000000 00000000`00000000 SmartDisk.exe+0x0

SYMBOL_NAME: SmartDisk.exe

FOLLOWUP_NAME: wintriage

MODULE_NAME: cubedisk

IMAGE_NAME: CubeDisk.exe

DEBUG_FLR_IMAGE_TIMESTAMP: 5b6831d7

STACK_COMMAND: ** Pseudo Context ** ; kb

FAILURE_BUCKET_ID: STACKIMMUNE_80000003_CubeDisk.exe!Unknown

BUCKET_ID: X64_APPLICATION_FAULT_STACKIMMUNE_NOSOS_SmartDisk.exe

FOLLOWUP_IP:
CubeDisk!.ctor+0 [D:\CubeDisk_18-09-27\CubeDisk\HttpBusiness.cs @ 24]
00000000`002d0000 4d5a pop r10

WATSON_STAGEONE_URL: http://watson.microsoft.com/StageOne/CubeDisk_exe/1_0_0_0/5b6831d7/unknown/0_0_0_0/bbbbbbb4/80000003/00000000.htm?Retriage=1

Followup: wintriage
---------
```

**(NTSTATUS) 0x80000003 강제로 덤프를 실행할 경우 발생함 hang이 발생한 곳을 찾기 위해 다음과 같이 실행**

0:000> !analyze -v -hang

```
*******************************************************************************
* *
* Exception Analysis *
* *
*******************************************************************************

Failed calling InternetOpenUrl, GLE=12002

FAULTING_IP:
+c5a7c60
00000000`00000000 ?? ???

EXCEPTION_RECORD: ffffffffffffffff -- (.exr 0xffffffffffffffff)
ExceptionAddress: 0000000000000000
ExceptionCode: 80000003 (Break instruction exception)
ExceptionFlags: 00000000
NumberParameters: 0

FAULTING_THREAD: 000000000000000e

BUGCHECK_STR: HANG

DEFAULT_BUCKET_ID: APPLICATION_HANG

PROCESS_NAME: CubeDisk.exe

OVERLAPPED_MODULE: Address regions for 'DWrite' and 'msls31' overlap

ERROR_CODE: (NTSTATUS) 0xcfffffff - 

EXCEPTION_CODE: (NTSTATUS) 0xcfffffff - 

MOD_LIST: 

NTGLOBALFLAG: 0

APPLICATION_VERIFIER_FLAGS: 0

MANAGED_STACK: !dumpstack -EE
No export dumpstack found

DERIVED_WAIT_CHAIN:

Dl Eid Cid WaitType
-- --- ------- --------------------------
0 1d28.1d34 Speculated (Triage) -->
14 1d28.2a58 Unknown

WAIT_CHAIN_COMMAND: ~0s;k;;~14s;k;;

BLOCKING_THREAD: 0000000000002a58

PRIMARY_PROBLEM_CLASS: APPLICATION_HANG

LAST_CONTROL_TRANSFER: from 0000000074792bf1 to 0000000074792e09

STACK_TEXT:

00000000`0393be38 00000000`74792bf1 : 00000000`75f372b9 00000000`ffff0023 00000000`00000246 00000000`07cf7f1c : wow64cpu!CpupSyscallStub+0x9
00000000`0393be40 00000000`7480d286 : 00000000`00000000 00000000`74791904 00000000`00000000 00000000`7480d286 : wow64cpu!Thunk0ArgReloadState+0x23
00000000`0393bf00 00000000`74808a90 : 00000000`00000000 00000000`7480d286 00000000`0393cd18 00000000`74808b14 : wow64!RunCpuSimulation+0xa
00000000`0393bf50 00000000`747d7938 : 00000000`0393c2d0 00000000`0000002f 00000000`0393cc30 00000000`00000030 : wow64!Wow64KiUserCallbackDispatcher+0x204
00000000`0393c2a0 00000000`7707b5ef : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000000 : wow64win!whcbfnHkINLPMSG+0xc0
00000000`0393ccb0 00000000`747e0bda : 00000000`747c374c 00000002`00000000 00000000`ffffffff 00000000`77ec623e : ntdll!KiUserCallbackDispatcherContinue
00000000`0393cd68 00000000`747c374c : 00000002`00000000 00000000`ffffffff 00000000`77ec623e 00000000`0393d6d0 : wow64win!ZwUserRealInternalGetMessage+0xa
00000000`0393cd70 00000000`7480d18f : 00000000`07cfc95c 00000000`07cfc9cc 00000002`00000000 00000000`7ef96000 : wow64win!whNtUserRealInternalGetMessage+0x40
00000000`0393cde0 00000000`74792776 : 00000000`771e010c 00000000`74790023 00000000`00000246 00000000`07cfca0c : wow64!Wow64SystemServiceEx+0xd7
00000000`0393d6a0 00000000`7480d286 : 00000000`07cfca68 00000000`74791904 00000000`7ef94000 00000000`7ef96000 : wow64cpu!TurboDispatchJumpAddressEnd+0x2d
00000000`0393d760 00000000`74808a90 : 00000002`00000000 00000000`0393e548 00000000`7ef96000 00000121`00000000 : wow64!RunCpuSimulation+0xa
00000000`0393d7b0 00000000`747d8f5b : 00000000`0393db60 00000000`0000003f 00000000`0393e4c0 00000000`00000014 : wow64!Wow64KiUserCallbackDispatcher+0x204
00000000`0393db00 00000000`7707b5ef : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00001fa0 : wow64win!whcbClientGetMessageMPH+0x9b
00000000`0393e4f0 00000000`747dfd4a : 00000000`747bad9b 00000000`00000000 00000000`00000000 00000000`00000000 : ntdll!KiUserCallbackDispatcherContinue
00000000`0393e568 00000000`747bad9b : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000000 : wow64win!ZwUserPeekMessage+0xa
00000000`0393e570 00000000`7480d18f : 00000000`07cfca40 00000000`7ef94000 00000000`00000000 00000000`0393e5f8 : wow64win!whNtUserPeekMessage+0x37
00000000`0393e5e0 00000000`74792776 : 00000000`75f372b9 00000000`00000023 00000000`00000246 00000000`07cfca2c : wow64!Wow64SystemServiceEx+0xd7
00000000`0393eea0 00000000`7480d286 : 00000000`00000000 00000000`74791920 00000000`00000000 00000000`00000000 : wow64cpu!TurboDispatchJumpAddressEnd+0x2d
00000000`0393ef60 00000000`7480c69e : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000000 : wow64!RunCpuSimulation+0xa
00000000`0393efb0 00000000`770a9ba4 : 00000000`00000000 00000000`7efdf000 00000000`7ef94000 00000000`00000000 : wow64!Wow64LdrpInitialize+0x42a
00000000`0393f500 00000000`7705374e : 00000000`0393f5c0 00000000`00000000 00000000`7efdf000 00000000`00000000 : ntdll! ?? ::FNODOBFM::`string'+0x22b94
00000000`0393f570 00000000`00000000 : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000000 : ntdll!LdrInitializeThunk+0xe

MODULE_NAME: Unknown_Module

IMAGE_NAME: Unknown_Image

DEBUG_FLR_IMAGE_TIMESTAMP: 0

STACK_COMMAND: ~14s ; kb                     ~14s; kb 이 명령어를 command 창에 입력하라는 것임

BUCKET_ID: X64_HANG

FAILURE_BUCKET_ID: APPLICATION_HANG_cfffffff_Unknown_Image!Unknown

WATSON_STAGEONE_URL: http://watson.microsoft.com/00000000.htm?Retriage=1
*** Followup info cannot be found !!! Please contact "Debugger Team"
---------
```

> !wow64exts.sw                         *wow64cpu를 만나면 32bit mode로 전환해야함*

```
Switched to 32bit mode
```

0:000:x86> ~14s ; kb

```
ntdll_771d0000!ZwWaitForSingleObject+0x15:
771ef901 83c404 add esp,4
ChildEBP RetAddr Args to Child
07cf7068 7721ebf6 000010c0 00000000 00000000 ntdll_771d0000!ZwWaitForSingleObject+0x15
07cf70cc 7721eada 00000000 00000000 07cf8eec ntdll_771d0000!RtlpWaitOnCriticalSection+0x13e
07cf70f4 10062647 100d0078 7d9a68e8 000c1b60 ntdll_771d0000!RtlEnterCriticalSection+0x150
WARNING: Stack unwind information not available. Following frames may be wrong.   위 오류에 대한 스택입니다.
07cf7b44 10065a66 7d9a6c28 000c1b60 07cf8eec SPF!ExitThreadHook+0x46507
07cf7f84 10037629 07cf8eec 100891ec 07cf8eec SPF!ExitThreadHook+0x49926
07cf83d8 100378f2 000c1b60 0e132748 07cf8eec SPF!ExitThreadHook+0x1b4e9
07cf83f8 10029f0b 000c1b60 0000004b 0000003b SPF!ExitThreadHook+0x1b7b2
07cfa7b0 1002c4cc 002516ec 00000016 07cfc21c SPF!ExitThreadHook+0xddcb
07cfc1f0 1001b111 07cfc21c 00000000 100ce940 SPF!ExitThreadHook+0x1038c
07cfc870 75f47451 00000000 00000001 07cfc934 SPF!CheckAttachType+0xd31
07cfc88c 75f380a9 00030000 00000001 07cfc934 user32!DispatchHookW+0x38
07cfc8cc 75f38ba1 07cfc924 07cfc934 07cfc950 user32!CallHookWithSEH+0x21
07cfc90c 771e013a 07cfc924 00000000 07cfca1c user32!__fnHkINLPMSG+0x75
*** WARNING: symbols timestamp is wrong 0x4a5bdf26 0x4a5bda06 for duser.dll
07cfc954 64921430 07cfc9d8 00000000 00000000 ntdll_771d0000!KiUserCallbackDispatcher+0x2e
07cfc990 649214e9 07cfc9d8 00000000 00000000 duser!CoreSC::xwProcessNL+0xfb
07cfc9b8 75f7fd3b 07cfc9d8 00000000 00000000 duser!MphProcessMessage+0x5e
07cfca0c 771e013a 07cfca24 00000000 07cfe854 user32!__ClientGetMessageMPH+0x34
07cfca38 75f40703 07cfcab4 00000000 00000000 ntdll_771d0000!KiUserCallbackDispatcher+0x2e
07cfca60 75f40769 07cfcab4 00000000 00000000 user32!_PeekMessage+0x88
07cfca8c 75f5d7ee 07cfcab4 00000000 00000000 user32!PeekMessageW+0x108
07cfcadc 75f5da5c 002516ec 001f19ba 00000008 user32!DialogBox2+0xfc
07cfcb08 75f5d98a 75b80000 0dff0b58 001f19ba user32!InternalDialogBox+0xe5
07cfcb28 75f5d70e 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamAorW+0x37
07cfcb48 75b8597b 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamW+0x1b
07cfcb94 6de7011a 0dff0b58 001f19ba 6495e610 comdlg32!CFileOpenSave::Show+0x181
07cfcbbc 531d56dc 54c93509 04363758 07cfe918 mfc90u!CFileDialog::DoModal+0xc5
07cfe85c 531dcaaa 07cfe918 54c916ad 04356204 JECM!CJBusiness::Function+0xa3c [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 1462]
07cfe8b0 531e9bde 04363784 04351ef8 54c91605 JECM!CJBusiness::Query+0x7ea [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 591]
07cfec34 531db624 04363758 043561f8 04363da8 JECM!CJCustomize::QueryStart+0x2be [c:\cubedisk\cubedisk_18-09-27\jecm\jcustomizequery.cpp @ 615]
07cfecdc 531dc97d 043561f8 54c9122d 07cfed98 JECM!CJBusiness::Download+0x684 [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 858]
07cfed30 531df1b0 04363784 04351e68 54c91385 JECM!CJBusiness::Query+0x6bd [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 558]
07cfee18 755c5bfa 07cff060 00000000 755c5a4a JECM!ATL::CAxDialogImpl::CreateActiveXControls+0x210 [c:\program files (x86)\microsoft visual studio 9.0\vc\atlmfc\include\atlwin.h @ 3708]
07cfee74 755a64f6 00000000 b1b3e261 036faa58 rpcrt4!NdrpServerOutInit+0x10f
07cfeea8 7720649f 75a28e42 75a28382 07cff030 rpcrt4!_SEH_epilog4
07cfeedc 00000000 000036b7 75b19bd4 071f0778 ntdll_771d0000!RtlNtStatusToDosError+0x3b
```

0:014:x86> kbn                                   *문제가 있는  부분 심볼 적용*

```
 # ChildEBP RetAddr  Args to Child              
00 07cf7068 7721ebf6 000010c0 00000000 00000000 ntdll_771d0000!NtWaitForSingleObject+0x15
01 07cf70cc 7721eada 00000000 00000000 07cf8eec ntdll_771d0000!RtlpWaitOnCriticalSection+0x13e
02 07cf70f4 10062647 100d0078 7d9a68e8 000c1b60 ntdll_771d0000!RtlEnterCriticalSection+0x150
03 07cf7b44 10065a66 7d9a6c28 000c1b60 07cf8eec SPF!CheckPath+0x2f7 [e:\projects2010\hook\spf\spfolder.cpp @ 1280] 
04 07cf7f84 10037629 07cf8eec 100891ec 07cf8eec SPF!GetFullPathOfComboLBox2+0x896 [e:\projects2010\hook\spf\spfolder.cpp @ 2254] 
05 07cf83d8 100378f2 000c1b60 0e132748 07cf8eec SPF!GetActiveFolder+0x429 [e:\projects2010\hook\spf\exputil2.cpp @ 401] 
06 07cf83f8 10029f0b 000c1b60 0000004b 0000003b SPF!GetTreeViewFolder+0x52 [e:\projects2010\hook\spf\exputil2.cpp @ 484] 
07 07cfa7b0 1002c4cc 002516ec 00000016 07cfc21c SPF!ChkOpenDlg+0x2ceb [e:\projects2010\hook\spf\commondlg.cpp @ 2600] 
08 07cfc1f0 1001b111 07cfc21c 00000000 100ce940 SPF!ChkRun+0x16c [e:\projects2010\hook\spf\commondlg.cpp @ 6285] 
09 07cfc870 75f47451 00000000 00000001 07cfc934 SPF!GetMsgProc+0x751 [e:\projects2010\hook\spf\api1.cpp @ 1587] 
0a 07cfc88c 75f380a9 00030000 00000001 07cfc934 user32!DispatchHookW+0x38
0b 07cfc8cc 75f38ba1 07cfc924 07cfc934 07cfc950 user32!CallHookWithSEH+0x21
0c 07cfc90c 771e013a 07cfc924 00000000 07cfca1c user32!__fnHkINLPMSG+0x75
0d 07cfc954 64921430 07cfc9d8 00000000 00000000 ntdll_771d0000!KiUserCallbackDispatcher+0x2e
0e 07cfc990 649214e9 07cfc9d8 00000000 00000000 duser!CoreSC::xwProcessNL+0xfb
0f 07cfc9b8 75f7fd3b 07cfc9d8 00000000 00000000 duser!MphProcessMessage+0x5e
10 07cfca0c 771e013a 07cfca24 00000000 07cfe854 user32!__ClientGetMessageMPH+0x34
11 07cfca38 75f40703 07cfcab4 00000000 00000000 ntdll_771d0000!KiUserCallbackDispatcher+0x2e
12 07cfca60 75f40769 07cfcab4 00000000 00000000 user32!_PeekMessage+0x88
13 07cfca8c 75f5d7ee 07cfcab4 00000000 00000000 user32!PeekMessageW+0x108
14 07cfcadc 75f5da5c 002516ec 001f19ba 00000008 user32!DialogBox2+0xfc
15 07cfcb08 75f5d98a 75b80000 0dff0b58 001f19ba user32!InternalDialogBox+0xe5
16 07cfcb28 75f5d70e 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamAorW+0x37
17 07cfcb48 75b8597b 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamW+0x1b
18 07cfcb94 6de7011a 0dff0b58 001f19ba 6495e610 comdlg32!CFileOpenSave::Show+0x181
19 07cfcbbc 531d56dc 54c93509 04363758 07cfe918 mfc90u!CFileDialog::DoModal+0xc5
1a 07cfe85c 531dcaaa 07cfe918 54c916ad 04356204 JECM!CJBusiness::Function+0xa3c [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 1462] 
1b 07cfe8b0 531e9bde 04363784 04351ef8 54c91605 JECM!CJBusiness::Query+0x7ea [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 591] 
1c 07cfec34 531db624 04363758 043561f8 04363da8 JECM!CJCustomize::QueryStart+0x2be [c:\cubedisk\cubedisk_18-09-27\jecm\jcustomizequery.cpp @ 615] 
1d 07cfecdc 531dc97d 043561f8 54c9122d 07cfed98 JECM!CJBusiness::Download+0x684 [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 858] 
1e 07cfed30 531df1b0 04363784 04351e68 54c91385 JECM!CJBusiness::Query+0x6bd [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 558] 
1f 07cfee18 755c5bfa 07cff060 00000000 755c5a4a JECM!ATL::CAxDialogImpl::CreateActiveXControls+0x210 [c:\program files (x86)\microsoft visual studio 9.0\vc\atlmfc\include\atlwin.h @ 3708] 
20 07cfee74 755a64f6 00000000 b1b3e261 036faa58 rpcrt4!NdrpServerOutInit+0x10f
21 07cfeea8 7720649f 75a28e42 75a28382 07cff030 rpcrt4!_SEH_epilog4
22 07cfeedc 00000000 000036b7 75b19bd4 071f0778 ntdll_771d0000!RtlNtStatusToDosError+0x3b
```

0:014:x86> !cs **100d0078***RtlEnterCriticalSection 의 args주소 확인*

```
-----------------------------------------
Critical section   = 0x100d0078 (SPF!g_spfolder_cs+0x0)
DebugInfo          = 0x0726d640
LOCKED
LockCount          = 0x1
WaiterWoken        = No
OwningThread       = 0x00003004
RecursionCount     = 0x1
LockSemaphore      = 0x10C0
SpinCount          = 0x00000000
```

0:014:x86> u 10062647

```
SPF!CheckPath+0x2f7 [e:\projects2010\hook\spf\spfolder.cpp @ 1280]:
10062647 393590000d10    cmp     dword ptr [SPF!g_pSpFolder (100d0090)],esi
1006264d 7410            je      SPF!CheckPath+0x30f (1006265f)
1006264f 6878000d10      push    offset SPF!g_spfolder_cs (100d0078)
10062654 ff15d8d10710    call    dword ptr [SPF!_imp__LeaveCriticalSection (1007d1d8)]
1006265a e9bc040000      jmp     SPF!InitSpecialFolder+0x25b (10062b1b)
1006265f 89b5e4f5ffff    mov     dword ptr [ebp-0A1Ch],esi
10062665 89b5d4f5ffff    mov     dword ptr [ebp-0A2Ch],esi
1006266b 89b5ecf5ffff    mov     dword ptr [ebp-0A14h],esi
```

0:014:x86> dt SPF!CheckPath  // SPF!CheckPath *args 주소(* 0x7d9a6c28 )확인을 위해 구조체 Parsing

```
CheckPath void (
ATL::CStringT > >*)
```

0:014:x86>dx -r1 ((SPF!ATL::CStringT > > \*)0x7d9a6c28)

```
((SPF!ATL::CStringT > > *)0x7d9a6c28)                 : 0x7d9a6c28 [Type: ATL::CStringT > > *]
    [+0x000] m_pszData        : Unable to read memory at Address 0x7d9a6c28
```

0:014:x86> lmvm SPF                                                  *문제가 있는 모듈 정보확인*

```
start    end        module name
10010000 1069d000   SPF      # (private pdb symbols)  \\166.125.11.182\edm5\debug\windbg\ossymbols_win7\SPF.pdb\0B4AA2F79BAD4546AAA743BE12C607041\SPF.pdb
    Loaded symbol image file: SPF.dll
    Image path: C:\Windows\System32\SPF.dll
    Image name: SPF.dll
    Browse all global symbols  functions  data
    Timestamp:        Thu Sep  6 02:21:58 2018 (5B90F1B6)
    CheckSum:         00665ACA
    ImageSize:        0068D000
    File version:     3.3.0.57
    Product version:  3.3.0.57
    File flags:       0 (Mask 3F)
    File OS:          4 Unknown Win32
    File type:        2.0 Dll
    File date:        00000000.00000000
    Translations:     0409.04b0
    Information from resource tables:
        CompanyName:      ITM System
        ProductName:      SPF Dynamic Link Library
        InternalName:     SPF
        OriginalFilename: SPF.DLL
        ProductVersion:   3.3.0.57
        FileVersion:      3.3.0.57
        FileDescription:  SPF DLL
        LegalCopyright:   Copyright (C) 2008 ITM System

0:014:x86> !dh 10010000 -f

File Type: DLL
FILE HEADER VALUES
14C machine (i386)
6 number of sections
5B90F198 time date stamp Thu Sep 06 18:21:28 2018

0 file pointer to symbol table
0 number of symbols
E0 size of optional header
2102 characteristics
Executable
32 bit word machine
DLL

OPTIONAL HEADER VALUES
10B magic #
10.00 linker version
6B800 size of code
5E6400 size of initialized data
0 size of uninitialized data
677D5 address of entry point
1000 base of code
----- new -----
0000000010000000 image base
1000 section alignment
200 file alignment
2 subsystem (Windows GUI)
5.01 operating system version
0.00 image version
5.01 subsystem version
67D000 size of image
400 size of headers
65DD5E checksum
0000000000100000 size of stack reserve
0000000000001000 size of stack commit
0000000000100000 size of heap reserve
0000000000001000 size of heap commit
100 DLL characteristics
NX compatible
9CFD0 [ 203] address [size] of Export Directory
9ACA4 [ 17C] address [size] of Import Directory
66B000 [ 4DC4] address [size] of Resource Directory
0 [ 0] address [size] of Exception Directory
0 [ 0] address [size] of Security Directory
670000 [ 8C28] address [size] of Base Relocation Directory
6D9D0 [ 1C] address [size] of Debug Directory
0 [ 0] address [size] of Description Directory
0 [ 0] address [size] of Special Directory
0 [ 0] address [size] of Thread Storage Directory
976A8 [ 40] address [size] of Load Configuration Directory
0 [ 0] address [size] of Bound Import Directory
6D000 [ 9A0] address [size] of Import Address Table Directory
0 [ 0] address [size] of Delay Import Directory
0 [ 0] address [size] of COR20 Header Directory
0 [ 0] address [size] of Reserved Directory
```

0:014:x86> !lmi SPF.DLL                                               *문제가 있는 모듈 정보확인*

```
Loaded Module Info: [spf] 
         Module: SPF
   Base Address: 10010000
     Image Name: SPF.dll
   Machine Type: 332 (I386)
     Time Stamp: 5b90f198 Thu Sep  6 02:21:28 2018
           Size: 67d000
       CheckSum: 65dd5e
Characteristics: 2102  
Debug Data Dirs: Type  Size     VA  Pointer
             CODEVIEW    47, 976f0,   962f0 RSDS - GUID: {0B4AA2F7-9BAD-4546-AAA7-43BE12C60704}
               Age: 1, Pdb: E:\Projects2010\Hook\SPF\Win32\Release\SPF.pdb
     Image Type: MEMORY   - Image read successfully from loaded memory.
    Symbol Type: PDB      - Symbols loaded successfully from image header.
                 \\166.125.11.182\edm5\debug\windbg\ossymbols_win7\SPF.pdb\0B4AA2F79BAD4546AAA743BE12C607041\SPF.pdb
       Compiler: Resource - front end [0.0 bld 0] - back end [10.0 bld 40219]
    Load Report: private symbols & lines, not source indexed 
                 \\166.125.11.182\edm5\debug\windbg\ossymbols_win7\SPF.pdb\0B4AA2F79BAD4546AAA743BE12C607041\SPF.pdb
```

```html
<article class="post-438 post type-post status-publish format-standard hentry category-debug"><div class="post-inner group">
<h1 class="post-title entry-title">WinDbg 사례</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2018년 10월 30일">2018년 10월 30일</time>
              · Updated <time class="updated" datetime="2018년 11월 8일">2018년 11월 8일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>0:000&gt; <span style="color: #0000ff;">!analyze -v</span></p>
<pre>*******************************************************************************
* *
* Exception Analysis *
* *
*******************************************************************************

*** WARNING: symbols timestamp is wrong 0x5b079867 0x5b0791e3 for mshtml.dll
*** WARNING: Unable to verify checksum for System.Windows.Forms.ni.dll
*** WARNING: symbols timestamp is wrong 0x4a5be036 0x4a5bdadf for rasman.dll
*** WARNING: symbols timestamp is wrong 0x4a5be0b0 0x4ce7ba42 for winmm.dll
*** ERROR: Symbol file could not be found. Defaulted to export symbols for MKW_M.dll -
*** WARNING: symbols timestamp is wrong 0x5a4db72e 0x5a4db715 for SPF_M.dll
*** ERROR: Symbol file could not be found. Defaulted to export symbols for SPF_M.dll -
*** WARNING: symbols timestamp is wrong 0x5b90f1b6 0x5b90f198 for SPF.dll
*** ERROR: Symbol file could not be found. Defaulted to export symbols for SPF.dll -
Failed calling InternetOpenUrl, GLE=12002

FAULTING_IP:
+c7827e0
00000000`00000000 ?? ???

EXCEPTION_RECORD: ffffffffffffffff -- (.exr 0xffffffffffffffff)
ExceptionAddress: 0000000000000000
ExceptionCode: 80000003 (Break instruction exception)
ExceptionFlags: 00000000
NumberParameters: 0

FAULTING_THREAD: 0000000000001d34

PROCESS_NAME: CubeDisk.exe

OVERLAPPED_MODULE: Address regions for 'DWrite' and 'msls31' overlap

ERROR_CODE: <span style="color: #ff0000;"><strong>(NTSTATUS) 0x80000003</strong></span> - {

EXCEPTION_CODE: (HRESULT) 0x80000003 (2147483651) - .

MOD_LIST: <analysis></analysis>

NTGLOBALFLAG: 0

APPLICATION_VERIFIER_FLAGS: 0

MANAGED_STACK: !dumpstack -EE
No export dumpstack found

ADDITIONAL_DEBUG_TEXT: Followup set based on attribute [Is_ChosenCrashFollowupThread] from Frame:[0] on thread:[PSEUDO_THREAD]

LAST_CONTROL_TRANSFER: from 0000000074792dbf to 0000000074792e09

BUGCHECK_STR: APPLICATION_FAULT_STACKIMMUNE_NOSOS

PRIMARY_PROBLEM_CLASS: STACKIMMUNE

DEFAULT_BUCKET_ID: STACKIMMUNE

STACK_TEXT:
00000000`00000000 00000000`00000000 SmartDisk.exe+0x0

SYMBOL_NAME: SmartDisk.exe

FOLLOWUP_NAME: wintriage

MODULE_NAME: cubedisk

IMAGE_NAME: CubeDisk.exe

DEBUG_FLR_IMAGE_TIMESTAMP: 5b6831d7

STACK_COMMAND: ** Pseudo Context ** ; kb

FAILURE_BUCKET_ID: STACKIMMUNE_80000003_CubeDisk.exe!Unknown

BUCKET_ID: X64_APPLICATION_FAULT_STACKIMMUNE_NOSOS_SmartDisk.exe

FOLLOWUP_IP:
CubeDisk!.ctor+0 [D:\CubeDisk_18-09-27\CubeDisk\HttpBusiness.cs @ 24]
00000000`002d0000 4d5a pop r10

WATSON_STAGEONE_URL: http://watson.microsoft.com/StageOne/CubeDisk_exe/1_0_0_0/5b6831d7/unknown/0_0_0_0/bbbbbbb4/80000003/00000000.htm?Retriage=1

Followup: wintriage
---------</pre>
<p><span style="color: #ff0000;"><strong>(NTSTATUS) 0x80000003 강제로 덤프를 실행할 경우 발생함 hang이 발생한 곳을 찾기 위해 다음과 같이 실행</strong></span></p>
<p>0:000&gt; <span style="color: #0000ff;">!analyze -v -hang</span></p>
<pre>*******************************************************************************
* *
* Exception Analysis *
* *
*******************************************************************************

Failed calling InternetOpenUrl, GLE=12002

FAULTING_IP:
+c5a7c60
00000000`00000000 ?? ???

EXCEPTION_RECORD: ffffffffffffffff -- (.exr 0xffffffffffffffff)
ExceptionAddress: 0000000000000000
ExceptionCode: 80000003 (Break instruction exception)
ExceptionFlags: 00000000
NumberParameters: 0

<span style="color: #000000;">FAULTING_THREAD: 000000000000000e</span>

BUGCHECK_STR: HANG

DEFAULT_BUCKET_ID: APPLICATION_HANG

PROCESS_NAME: CubeDisk.exe

OVERLAPPED_MODULE: Address regions for 'DWrite' and 'msls31' overlap

ERROR_CODE: (NTSTATUS) 0xcfffffff - <unable code="" error="" get="" text="" to="">

EXCEPTION_CODE: (NTSTATUS) 0xcfffffff - <unable code="" error="" get="" text="" to="">

MOD_LIST: <analysis></analysis>

NTGLOBALFLAG: 0

APPLICATION_VERIFIER_FLAGS: 0

MANAGED_STACK: !dumpstack -EE
No export dumpstack found

DERIVED_WAIT_CHAIN:

Dl Eid Cid WaitType
-- --- ------- --------------------------
0 1d28.1d34 Speculated (Triage) --&gt;
14 1d28.2a58 Unknown

<span style="color: #0000ff;">WAIT_CHAIN_COMMAND: ~0s;k;;~14s;k;;</span>

<span style="color: #ff0000;">BLOCKING_THREAD: 0000000000002a58</span>

PRIMARY_PROBLEM_CLASS: APPLICATION_HANG

LAST_CONTROL_TRANSFER: from 0000000074792bf1 to 0000000074792e09

STACK_TEXT:

00000000`0393be38 00000000`74792bf1 : 00000000`75f372b9 00000000`ffff0023 00000000`00000246 00000000`07cf7f1c : <span style="color: #0000ff;">wow64cpu!CpupSyscallStub</span>+0x9
00000000`0393be40 00000000`7480d286 : 00000000`00000000 00000000`74791904 00000000`00000000 00000000`7480d286 : <span style="color: #0000ff;">wow64cpu!Thunk0ArgReloadState</span>+0x23
00000000`0393bf00 00000000`74808a90 : 00000000`00000000 00000000`7480d286 00000000`0393cd18 00000000`74808b14 : wow64!RunCpuSimulation+0xa
00000000`0393bf50 00000000`747d7938 : 00000000`0393c2d0 00000000`0000002f 00000000`0393cc30 00000000`00000030 : wow64!Wow64KiUserCallbackDispatcher+0x204
00000000`0393c2a0 00000000`7707b5ef : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000000 : wow64win!whcbfnHkINLPMSG+0xc0
00000000`0393ccb0 00000000`747e0bda : 00000000`747c374c 00000002`00000000 00000000`ffffffff 00000000`77ec623e : ntdll!KiUserCallbackDispatcherContinue
00000000`0393cd68 00000000`747c374c : 00000002`00000000 00000000`ffffffff 00000000`77ec623e 00000000`0393d6d0 : wow64win!ZwUserRealInternalGetMessage+0xa
00000000`0393cd70 00000000`7480d18f : 00000000`07cfc95c 00000000`07cfc9cc 00000002`00000000 00000000`7ef96000 : wow64win!whNtUserRealInternalGetMessage+0x40
00000000`0393cde0 00000000`74792776 : 00000000`771e010c 00000000`74790023 00000000`00000246 00000000`07cfca0c : wow64!Wow64SystemServiceEx+0xd7
00000000`0393d6a0 00000000`7480d286 : 00000000`07cfca68 00000000`74791904 00000000`7ef94000 00000000`7ef96000 : wow64cpu!TurboDispatchJumpAddressEnd+0x2d
00000000`0393d760 00000000`74808a90 : 00000002`00000000 00000000`0393e548 00000000`7ef96000 00000121`00000000 : wow64!RunCpuSimulation+0xa
00000000`0393d7b0 00000000`747d8f5b : 00000000`0393db60 00000000`0000003f 00000000`0393e4c0 00000000`00000014 : wow64!Wow64KiUserCallbackDispatcher+0x204
00000000`0393db00 00000000`7707b5ef : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00001fa0 : wow64win!whcbClientGetMessageMPH+0x9b
00000000`0393e4f0 00000000`747dfd4a : 00000000`747bad9b 00000000`00000000 00000000`00000000 00000000`00000000 : ntdll!KiUserCallbackDispatcherContinue
00000000`0393e568 00000000`747bad9b : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000000 : wow64win!ZwUserPeekMessage+0xa
00000000`0393e570 00000000`7480d18f : 00000000`07cfca40 00000000`7ef94000 00000000`00000000 00000000`0393e5f8 : wow64win!whNtUserPeekMessage+0x37
00000000`0393e5e0 00000000`74792776 : 00000000`75f372b9 00000000`00000023 00000000`00000246 00000000`07cfca2c : wow64!Wow64SystemServiceEx+0xd7
00000000`0393eea0 00000000`7480d286 : 00000000`00000000 00000000`74791920 00000000`00000000 00000000`00000000 : wow64cpu!TurboDispatchJumpAddressEnd+0x2d
00000000`0393ef60 00000000`7480c69e : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000000 : wow64!RunCpuSimulation+0xa
00000000`0393efb0 00000000`770a9ba4 : 00000000`00000000 00000000`7efdf000 00000000`7ef94000 00000000`00000000 : wow64!Wow64LdrpInitialize+0x42a
00000000`0393f500 00000000`7705374e : 00000000`0393f5c0 00000000`00000000 00000000`7efdf000 00000000`00000000 : ntdll! ?? ::FNODOBFM::`string'+0x22b94
00000000`0393f570 00000000`00000000 : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000000 : ntdll!LdrInitializeThunk+0xe

MODULE_NAME: Unknown_Module

IMAGE_NAME: Unknown_Image

DEBUG_FLR_IMAGE_TIMESTAMP: 0

<span style="color: #0000ff;">STACK_COMMAND: ~14s ; kb                    <em><span style="color: #ff0000;"> ~14s; kb 이 명령어를 command 창에 입력하라는 것임</span></em></span>

<span style="color: #0000ff;">BUCKET_ID: X64_HANG</span>

<span style="color: #0000ff;">FAILURE_BUCKET_ID: APPLICATION_HANG_cfffffff_Unknown_Image!Unknown</span>

WATSON_STAGEONE_URL: http://watson.microsoft.com/00000000.htm?Retriage=1
*** Followup info cannot be found !!! Please contact "Debugger Team"
---------</unable></unable></pre>
<p><span style="font-size: 1rem;">&gt; !wow64exts.sw                         <span style="color: #ff0000;"><em>wow64cpu를 만나면 32bit mode로 전환해야함</em></span></span></p>
<pre>Switched to 32bit mode</pre>
<p>0:000:x86&gt;<span style="color: #000000;"> ~14s ; kb</span></p>
<pre>ntdll_771d0000!ZwWaitForSingleObject+0x15:
771ef901 83c404 add esp,4
ChildEBP RetAddr Args to Child
07cf7068 7721ebf6 000010c0 00000000 00000000 ntdll_771d0000!ZwWaitForSingleObject+0x15
07cf70cc 7721eada 00000000 00000000 07cf8eec ntdll_771d0000!RtlpWaitOnCriticalSection+0x13e
07cf70f4 10062647 <span style="color: #ff0000;">100d0078</span> 7d9a68e8 000c1b60 ntdll_771d0000!<span style="color: #ff0000;">RtlEnterCriticalSection</span>+0x150
WARNING: Stack unwind information not available. Following frames may be wrong.  <span style="color: #ff0000;"><em> 위 오류에 대한 스택입니다.</em></span>
<span style="color: #ff0000;">07cf7b44 10065a66 7d9a6c28 000c1b60 07cf8eec SPF!ExitThreadHook+0x46507</span>
07cf7f84 10037629 07cf8eec 100891ec 07cf8eec SPF!ExitThreadHook+0x49926
07cf83d8 100378f2 000c1b60 0e132748 07cf8eec SPF!ExitThreadHook+0x1b4e9
07cf83f8 10029f0b 000c1b60 0000004b 0000003b SPF!ExitThreadHook+0x1b7b2
07cfa7b0 1002c4cc 002516ec 00000016 07cfc21c SPF!ExitThreadHook+0xddcb
07cfc1f0 1001b111 07cfc21c 00000000 100ce940 SPF!ExitThreadHook+0x1038c
07cfc870 75f47451 00000000 00000001 07cfc934 SPF!CheckAttachType+0xd31
07cfc88c 75f380a9 00030000 00000001 07cfc934 user32!DispatchHookW+0x38
07cfc8cc 75f38ba1 07cfc924 07cfc934 07cfc950 user32!CallHookWithSEH+0x21
07cfc90c 771e013a 07cfc924 00000000 07cfca1c user32!__fnHkINLPMSG+0x75
*** WARNING: symbols timestamp is wrong 0x4a5bdf26 0x4a5bda06 for duser.dll
07cfc954 64921430 07cfc9d8 00000000 00000000 ntdll_771d0000!KiUserCallbackDispatcher+0x2e
07cfc990 649214e9 07cfc9d8 00000000 00000000 duser!CoreSC::xwProcessNL+0xfb
07cfc9b8 75f7fd3b 07cfc9d8 00000000 00000000 duser!MphProcessMessage+0x5e
07cfca0c 771e013a 07cfca24 00000000 07cfe854 user32!__ClientGetMessageMPH+0x34
07cfca38 75f40703 07cfcab4 00000000 00000000 ntdll_771d0000!KiUserCallbackDispatcher+0x2e
07cfca60 75f40769 07cfcab4 00000000 00000000 user32!_PeekMessage+0x88
07cfca8c 75f5d7ee 07cfcab4 00000000 00000000 user32!PeekMessageW+0x108
07cfcadc 75f5da5c 002516ec 001f19ba 00000008 user32!DialogBox2+0xfc
07cfcb08 75f5d98a 75b80000 0dff0b58 001f19ba user32!InternalDialogBox+0xe5
07cfcb28 75f5d70e 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamAorW+0x37
07cfcb48 75b8597b 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamW+0x1b
07cfcb94 6de7011a 0dff0b58 001f19ba 6495e610 comdlg32!CFileOpenSave::Show+0x181
07cfcbbc 531d56dc 54c93509 04363758 07cfe918 mfc90u!CFileDialog::DoModal+0xc5
07cfe85c 531dcaaa 07cfe918 54c916ad 04356204 JECM!CJBusiness::Function+0xa3c [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 1462]
07cfe8b0 531e9bde 04363784 04351ef8 54c91605 JECM!CJBusiness::Query+0x7ea [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 591]
07cfec34 531db624 04363758 043561f8 04363da8 JECM!CJCustomize::QueryStart+0x2be [c:\cubedisk\cubedisk_18-09-27\jecm\jcustomizequery.cpp @ 615]
07cfecdc 531dc97d 043561f8 54c9122d 07cfed98 JECM!CJBusiness::Download+0x684 [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 858]
07cfed30 531df1b0 04363784 04351e68 54c91385 JECM!CJBusiness::Query+0x6bd [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 558]
07cfee18 755c5bfa 07cff060 00000000 755c5a4a JECM!ATL::CAxDialogImpl<cjecmcontrol,atl::cwindow>::CreateActiveXControls+0x210 [c:\program files (x86)\microsoft visual studio 9.0\vc\atlmfc\include\atlwin.h @ 3708]
07cfee74 755a64f6 00000000 b1b3e261 036faa58 rpcrt4!NdrpServerOutInit+0x10f
07cfeea8 7720649f 75a28e42 75a28382 07cff030 rpcrt4!_SEH_epilog4
07cfeedc 00000000 000036b7 75b19bd4 071f0778 ntdll_771d0000!RtlNtStatusToDosError+0x3b</cjecmcontrol,atl::cwindow></pre>
<p>0:014:x86&gt; kbn                                   <em><span style="color: #ff0000;">문제가 있는  부분 심볼 적용</span></em></p>
<pre> # ChildEBP RetAddr  Args to Child              
00 07cf7068 7721ebf6 000010c0 00000000 00000000 ntdll_771d0000!NtWaitForSingleObject+0x15
01 07cf70cc 7721eada 00000000 00000000 07cf8eec ntdll_771d0000!RtlpWaitOnCriticalSection+0x13e
02 07cf70f4 <strong><span style="color: #ff0000;">10062647</span></strong> <strong><span style="color: #ff0000;">100d0078</span></strong> 7d9a68e8 000c1b60 ntdll_771d0000!RtlEnterCriticalSection+0x150
03 07cf7b44 10065a66 <span style="color: #0000ff;">7d9a6c28</span> 000c1b60 07cf8eec SPF!CheckPath+0x2f7 [e:\projects2010\hook\spf\spfolder.cpp @ 1280] 
04 07cf7f84 10037629 07cf8eec 100891ec 07cf8eec SPF!GetFullPathOfComboLBox2+0x896 [e:\projects2010\hook\spf\spfolder.cpp @ 2254] 
05 07cf83d8 100378f2 000c1b60 0e132748 07cf8eec SPF!GetActiveFolder+0x429 [e:\projects2010\hook\spf\exputil2.cpp @ 401] 
06 07cf83f8 10029f0b 000c1b60 0000004b 0000003b SPF!GetTreeViewFolder+0x52 [e:\projects2010\hook\spf\exputil2.cpp @ 484] 
07 07cfa7b0 1002c4cc 002516ec 00000016 07cfc21c SPF!ChkOpenDlg+0x2ceb [e:\projects2010\hook\spf\commondlg.cpp @ 2600] 
08 07cfc1f0 1001b111 07cfc21c 00000000 100ce940 SPF!ChkRun+0x16c [e:\projects2010\hook\spf\commondlg.cpp @ 6285] 
09 07cfc870 75f47451 00000000 00000001 07cfc934 SPF!GetMsgProc+0x751 [e:\projects2010\hook\spf\api1.cpp @ 1587] 
0a 07cfc88c 75f380a9 00030000 00000001 07cfc934 user32!DispatchHookW+0x38
0b 07cfc8cc 75f38ba1 07cfc924 07cfc934 07cfc950 user32!CallHookWithSEH+0x21
0c 07cfc90c 771e013a 07cfc924 00000000 07cfca1c user32!__fnHkINLPMSG+0x75
0d 07cfc954 64921430 07cfc9d8 00000000 00000000 ntdll_771d0000!KiUserCallbackDispatcher+0x2e
0e 07cfc990 649214e9 07cfc9d8 00000000 00000000 duser!CoreSC::xwProcessNL+0xfb
0f 07cfc9b8 75f7fd3b 07cfc9d8 00000000 00000000 duser!MphProcessMessage+0x5e
10 07cfca0c 771e013a 07cfca24 00000000 07cfe854 user32!__ClientGetMessageMPH+0x34
11 07cfca38 75f40703 07cfcab4 00000000 00000000 ntdll_771d0000!KiUserCallbackDispatcher+0x2e
12 07cfca60 75f40769 07cfcab4 00000000 00000000 user32!_PeekMessage+0x88
13 07cfca8c 75f5d7ee 07cfcab4 00000000 00000000 user32!PeekMessageW+0x108
14 07cfcadc 75f5da5c 002516ec 001f19ba 00000008 user32!DialogBox2+0xfc
15 07cfcb08 75f5d98a 75b80000 0dff0b58 001f19ba user32!InternalDialogBox+0xe5
16 07cfcb28 75f5d70e 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamAorW+0x37
17 07cfcb48 75b8597b 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamW+0x1b
18 07cfcb94 6de7011a 0dff0b58 001f19ba 6495e610 comdlg32!CFileOpenSave::Show+0x181
19 07cfcbbc 531d56dc 54c93509 04363758 07cfe918 mfc90u!CFileDialog::DoModal+0xc5
1a 07cfe85c 531dcaaa 07cfe918 54c916ad 04356204 JECM!CJBusiness::Function+0xa3c [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 1462] 
1b 07cfe8b0 531e9bde 04363784 04351ef8 54c91605 JECM!CJBusiness::Query+0x7ea [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 591] 
1c 07cfec34 531db624 04363758 043561f8 04363da8 JECM!CJCustomize::QueryStart+0x2be [c:\cubedisk\cubedisk_18-09-27\jecm\jcustomizequery.cpp @ 615] 
1d 07cfecdc 531dc97d 043561f8 54c9122d 07cfed98 JECM!CJBusiness::Download+0x684 [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 858] 
1e 07cfed30 531df1b0 04363784 04351e68 54c91385 JECM!CJBusiness::Query+0x6bd [c:\cubedisk\cubedisk_18-09-27\jecm\jbusiness.cpp @ 558] 
1f 07cfee18 755c5bfa 07cff060 00000000 755c5a4a JECM!ATL::CAxDialogImpl<cjecmcontrol,atl::cwindow>::CreateActiveXControls+0x210 [c:\program files (x86)\microsoft visual studio 9.0\vc\atlmfc\include\atlwin.h @ 3708] 
20 07cfee74 755a64f6 00000000 b1b3e261 036faa58 rpcrt4!NdrpServerOutInit+0x10f
21 07cfeea8 7720649f 75a28e42 75a28382 07cff030 rpcrt4!_SEH_epilog4
22 07cfeedc 00000000 000036b7 75b19bd4 071f0778 ntdll_771d0000!RtlNtStatusToDosError+0x3b



</cjecmcontrol,atl::cwindow></pre>
<p>0:014:x86&gt; !cs <strong><span style="color: #ff0000;">100d0078                              </span></strong><span style="color: #ff0000;"><em>RtlEnterCriticalSection 의 args주소 확인</em></span></p>
<pre>-----------------------------------------
Critical section   = 0x100d0078 (<span style="color: #ff0000;">SPF!g_spfolder_cs+0x0</span>)
DebugInfo          = 0x0726d640
LOCKED
LockCount          = 0x1
WaiterWoken        = No
OwningThread       = 0x0000<span style="color: #ff0000;">3004</span>
RecursionCount     = 0x1
LockSemaphore      = 0x10C0
SpinCount          = 0x00000000

</pre>
<p>0:014:x86&gt; u 10062647</p>
<pre>SPF!CheckPath+0x2f7 [e:\projects2010\hook\spf\spfolder.cpp @ 1280]:
10062647 393590000d10    cmp     dword ptr [SPF!g_pSpFolder (100d0090)],esi
1006264d 7410            je      SPF!CheckPath+0x30f (1006265f)
1006264f 6878000d10      push    offset SPF!g_spfolder_cs (100d0078)
10062654 ff15d8d10710    call    dword ptr [SPF!_imp__LeaveCriticalSection (1007d1d8)]
1006265a e9bc040000      jmp     SPF!InitSpecialFolder+0x25b (10062b1b)
1006265f 89b5e4f5ffff    mov     dword ptr [ebp-0A1Ch],esi
10062665 89b5d4f5ffff    mov     dword ptr [ebp-0A2Ch],esi
1006266b 89b5ecf5ffff    mov     dword ptr [ebp-0A14h],esi</pre>
<p>0:014:x86&gt; dt SPF!CheckPath  <span style="color: #ff0000;">// SPF!CheckPath <em>args 주소( </em>0x7d9a6c28 )확인을 위해 구조체 Parsing</span></p>
<pre>CheckPath void (
ATL::CStringT<wchar_t,strtraitmfc_dll<wchar_t,atl::chtraitscrt<wchar_t> &gt; &gt;*)</wchar_t,strtraitmfc_dll<wchar_t,atl::chtraitscrt<wchar_t></pre>
<p>0:014:x86&gt;dx -r1 ((SPF!ATL::CStringT<wchar_t,strtraitmfc_dll<wchar_t,atl::chtraitscrt<wchar_t> &gt; &gt; *)0x7d9a6c28)</wchar_t,strtraitmfc_dll<wchar_t,atl::chtraitscrt<wchar_t></p>
<pre>((SPF!ATL::CStringT<wchar_t,strtraitmfc_dll<wchar_t,atl::chtraitscrt<wchar_t> &gt; &gt; *)0x7d9a6c28)                 : 0x7d9a6c28 [Type: ATL::CStringT<wchar_t,strtraitmfc_dll<wchar_t,atl::chtraitscrt<wchar_t> &gt; &gt; *]
    [+0x000] m_pszData        : Unable to read memory at Address 0x7d9a6c28</wchar_t,strtraitmfc_dll<wchar_t,atl::chtraitscrt<wchar_t></wchar_t,strtraitmfc_dll<wchar_t,atl::chtraitscrt<wchar_t></pre>
<p>0:014:x86&gt; lmvm SPF                                                  <em><span style="color: #ff0000;">문제가 있는 모듈 정보확인</span></em></p>
<pre>start    end        module name
10010000 1069d000   SPF      # (private pdb symbols)  \\166.125.11.182\edm5\debug\windbg\ossymbols_win7\SPF.pdb\0B4AA2F79BAD4546AAA743BE12C607041\SPF.pdb
    Loaded symbol image file: SPF.dll
    Image path: C:\Windows\System32\SPF.dll
    Image name: SPF.dll
    Browse all global symbols  functions  data
    Timestamp:        Thu Sep  6 02:21:58 2018 (5B90F1B6)
    CheckSum:         00665ACA
    ImageSize:        0068D000
    File version:     3.3.0.57
    Product version:  3.3.0.57
    File flags:       0 (Mask 3F)
    File OS:          4 Unknown Win32
    File type:        2.0 Dll
    File date:        00000000.00000000
    Translations:     0409.04b0
    Information from resource tables:
        CompanyName:      ITM System
        ProductName:      SPF Dynamic Link Library
        InternalName:     SPF
        OriginalFilename: SPF.DLL
        ProductVersion:   3.3.0.57
        FileVersion:      3.3.0.57
        FileDescription:  SPF DLL
        LegalCopyright:   Copyright (C) 2008 ITM System

0:014:x86&gt; !dh 10010000 -f

File Type: DLL
FILE HEADER VALUES
14C machine (i386)
6 number of sections
5B90F198 time date stamp Thu Sep 06 18:21:28 2018

0 file pointer to symbol table
0 number of symbols
E0 size of optional header
2102 characteristics
Executable
32 bit word machine
DLL

OPTIONAL HEADER VALUES
10B magic #
10.00 linker version
6B800 size of code
5E6400 size of initialized data
0 size of uninitialized data
677D5 address of entry point
1000 base of code
----- new -----
0000000010000000 image base
1000 section alignment
200 file alignment
2 subsystem (Windows GUI)
5.01 operating system version
0.00 image version
5.01 subsystem version
67D000 size of image
400 size of headers
65DD5E checksum
0000000000100000 size of stack reserve
0000000000001000 size of stack commit
0000000000100000 size of heap reserve
0000000000001000 size of heap commit
100 DLL characteristics
NX compatible
9CFD0 [ 203] address [size] of Export Directory
9ACA4 [ 17C] address [size] of Import Directory
66B000 [ 4DC4] address [size] of Resource Directory
0 [ 0] address [size] of Exception Directory
0 [ 0] address [size] of Security Directory
670000 [ 8C28] address [size] of Base Relocation Directory
6D9D0 [ 1C] address [size] of Debug Directory
0 [ 0] address [size] of Description Directory
0 [ 0] address [size] of Special Directory
0 [ 0] address [size] of Thread Storage Directory
976A8 [ 40] address [size] of Load Configuration Directory
0 [ 0] address [size] of Bound Import Directory
6D000 [ 9A0] address [size] of Import Address Table Directory
0 [ 0] address [size] of Delay Import Directory
0 [ 0] address [size] of COR20 Header Directory
0 [ 0] address [size] of Reserved Directory</pre>
<p>0:014:x86&gt; !lmi SPF.DLL                                               <em><span style="color: #ff0000;">문제가 있는 모듈 정보확인</span></em></p>
<pre>Loaded Module Info: [spf] 
         Module: SPF
   Base Address: 10010000
     Image Name: SPF.dll
   Machine Type: 332 (I386)
     Time Stamp: 5b90f198 Thu Sep  6 02:21:28 2018
           Size: 67d000
       CheckSum: 65dd5e
Characteristics: 2102  
Debug Data Dirs: Type  Size     VA  Pointer
             CODEVIEW    47, 976f0,   962f0 RSDS - GUID: {0B4AA2F7-9BAD-4546-AAA7-43BE12C60704}
               Age: 1, Pdb: E:\Projects2010\Hook\SPF\Win32\Release\SPF.pdb
     Image Type: MEMORY   - Image read successfully from loaded memory.
    Symbol Type: PDB      - Symbols loaded successfully from image header.
                 \\166.125.11.182\edm5\debug\windbg\ossymbols_win7\SPF.pdb\0B4AA2F79BAD4546AAA743BE12C607041\SPF.pdb
       Compiler: Resource - front end [0.0 bld 0] - back end [10.0 bld 40219]
    Load Report: private symbols &amp; lines, not source indexed 
                 \\166.125.11.182\edm5\debug\windbg\ossymbols_win7\SPF.pdb\0B4AA2F79BAD4546AAA743BE12C607041\SPF.pdb</pre>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
