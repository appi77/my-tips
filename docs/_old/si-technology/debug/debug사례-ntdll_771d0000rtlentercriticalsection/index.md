---
title: "[DEBUG사례] ntdll_771d0000!RtlEnterCriticalSection"
date: "No Date"
---

[DEBUG사례] ntdll\_771d0000!RtlEnterCriticalSection
=================================================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2019년 2월 25일

#### ▶ 실제 사례

> !dml\_proc  
DbgId PID Image file name  
0 cbd4 *C:\Program Files (x86)\Notepad++\notepad++.exe*

> !runaway  
User Mode Time  
Thread Time  
0:c628 0 days 0:00:00.374  
10:c994 0 days 0:00:00.015  
11:c470 0 days 0:00:00.000  
9:c8dc 0 days 0:00:00.000  
8:c4b0 0 days 0:00:00.000  
7:c888 0 days 0:00:00.000  
6:ca84 0 days 0:00:00.000  
5:ca60 0 days 0:00:00.000  
4:c130 0 days 0:00:00.000  
3:ca64 0 days 0:00:00.000  
2:c16c 0 days 0:00:00.000  
1:cbd0 0 days 0:00:00.000

> !analyze -v -hang  
STACK\_COMMAND: ~14s ; kb  
BUCKET\_ID: X64\_HANG  
FAILURE\_BUCKET\_ID: APPLICATION\_HANG\_cfffffff\_Unknown\_Image!Unknown

> ~14s ; kb  
00000000`74792bf1 : 00000000`75f372b9 00000000`ffff0023 00000000`00000246 00000000`07cf7f1c : wow64cpu!CpupSyscallStub+0x9  
00000000`7480d286 : 00000000`00000000 00000000`74791904 00000000`00000000 00000000`7480d286 : wow64cpu!Thunk0ArgReloadState+0x23  
…..

> !wow64exts.sw  
Switched to 32bit mode

0:014:x86> kb  
ChildEBP RetAddr Args to Child  
07cf7068 7721ebf6 000010c0 00000000 00000000 ntdll\_771d0000!ZwWaitForSingleObject+0x15  
07cf70cc 7721eada 00000000 00000000 07cf8eec ntdll\_771d0000!RtlpWaitOnCriticalSection+0x13e  
07cf70f4 10062647 **100d0078** 7d9a68e8 000c1b60 ntdll\_771d0000!**RtlEnterCriticalSection**+0x150  
WARNING: Stack unwind information not available. Following frames may be wrong.  
07cf7b44 10065a66 7d9a6c28 000c1b60 07cf8eec SPF!ExitThreadHook+0x46507  
07cf7f84 10037629 07cf8eec 100891ec 07cf8eec SPF!ExitThreadHook+0x49926  
07cf83d8 100378f2 000c1b60 0e132748 07cf8eec SPF!ExitThreadHook+0x1b4e9  
07cf83f8 10029f0b 000c1b60 0000004b 0000003b SPF!ExitThreadHook+0x1b7b2  
07cfa7b0 1002c4cc 002516ec 00000016 07cfc21c SPF!ExitThreadHook+0xddcb  
07cfc1f0 1001b111 07cfc21c 00000000 100ce940 SPF!ExitThreadHook+0x1038c  
07cfc870 75f47451 00000000 00000001 07cfc934 SPF!CheckAttachType+0xd31  
07cfc88c 75f380a9 00030000 00000001 07cfc934 user32!DispatchHookW+0x38  
07cfc8cc 75f38ba1 07cfc924 07cfc934 07cfc950 user32!CallHookWithSEH+0x21  
07cfc90c 771e013a 07cfc924 00000000 07cfca1c user32!\_\_fnHkINLPMSG+0x75  
07cfc954 64921430 07cfc9d8 00000000 00000000 ntdll\_771d0000!KiUserCallbackDispatcher+0x2e  
07cfc990 649214e9 07cfc9d8 00000000 00000000 duser!CoreSC::xwProcessNL+0xfb  
07cfc9b8 75f7fd3b 07cfc9d8 00000000 00000000 duser!MphProcessMessage+0x5e  
07cfca0c 771e013a 07cfca24 00000000 07cfe854 user32!\_\_ClientGetMessageMPH+0x34  
07cfca38 75f40703 07cfcab4 00000000 00000000 ntdll\_771d0000!KiUserCallbackDispatcher+0x2e  
07cfca60 75f40769 07cfcab4 00000000 00000000 user32!\_PeekMessage+0x88  
07cfca8c 75f5d7ee 07cfcab4 00000000 00000000 user32!PeekMessageW+0x108  
07cfcadc 75f5da5c 002516ec 001f19ba 00000008 user32!DialogBox2+0xfc  
07cfcb08 75f5d98a 75b80000 0dff0b58 001f19ba user32!InternalDialogBox+0xe5  
07cfcb28 75f5d70e 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamAorW+0x37  
07cfcb48 75b8597b 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamW+0x1b  
07cfcb94 6de7011a 0dff0b58 001f19ba 6495e610 comdlg32!CFileOpenSave::Show+0x181  
07cfcbbc 531d56dc 54c93509 04363758 07cfe918 mfc90u!CFileDialog::DoModal+0xc5  
07cfcc40 746d3c1b 06730000 00000000 746d3c3a JECM+0x56dc  
07cfcc8c 6de4b325 04354e78 04356204 6de43b6b msvcr90!free+0xcd  
07cfcc98 6de43b6b 04354e78 64959275 54c93352 mfc90u!CMemFile::Free+0xe  
07cfccac 64959296 0673ebf0 07cfcca4 00750051 mfc90u!ATL::CStringData::Release+0x17  
07cfccb0 0673ebf0 07cfcca4 00750051 6ddfee64 duser!JLog::Printf+0x166  
07cfccb4 07cfcca4 00750051 6ddfee64 00000002 0x673ebf0  
07cfccb8 00750051 6ddfee64 00000002 00000000 0x7cfcca4  
07cfccbc 6ddfee64 00000002 00000000 00000000 0x750051  
07cfccc0 00000000 00000000 00000000 00000000 mfc90u!CFileDialog::`vftable’

0:014:x86> !cs **100d0078**  
—————————————–  
Critical section = 0x00000000100d0078 (SPF!ExitThreadHook+0xB3F38)  
DebugInfo = 0x000000000726d640  
LOCKED  
LockCount = 0xFFFFFFFF  
WaiterWoken = Yes  
OwningThread = 0x00000000000010c0  
RecursionCount = 0x3004  
LockSemaphore = 0x0  
SpinCount = 0x0000000000000000

```html
<article class="post-570 post type-post status-publish format-standard hentry category-debug"><div class="post-inner group">
<h1 class="post-title entry-title">[DEBUG사례] ntdll_771d0000!RtlEnterCriticalSection</h1>
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
<p>&gt; !dml_proc<br/>
DbgId PID Image file name<br/>
0 cbd4 <span style="color: #0000ff;"><em>C:\Program Files (x86)\Notepad++\notepad++.exe</em></span></p>
<p>&gt; !runaway<br/>
User Mode Time<br/>
Thread Time<br/>
0:c628 0 days 0:00:00.374<br/>
10:c994 0 days 0:00:00.015<br/>
11:c470 0 days 0:00:00.000<br/>
9:c8dc 0 days 0:00:00.000<br/>
8:c4b0 0 days 0:00:00.000<br/>
7:c888 0 days 0:00:00.000<br/>
6:ca84 0 days 0:00:00.000<br/>
5:ca60 0 days 0:00:00.000<br/>
4:c130 0 days 0:00:00.000<br/>
3:ca64 0 days 0:00:00.000<br/>
2:c16c 0 days 0:00:00.000<br/>
1:cbd0 0 days 0:00:00.000</p>
<p>&gt; !analyze -v -hang<br/>
STACK_COMMAND: ~14s ; kb<br/>
BUCKET_ID: X64_HANG<br/>
FAILURE_BUCKET_ID: APPLICATION_HANG_cfffffff_Unknown_Image!Unknown</p>
<p>&gt; ~14s ; kb<br/>
00000000`74792bf1 : 00000000`75f372b9 00000000`ffff0023 00000000`00000246 00000000`07cf7f1c : <span style="color: #0000ff;">wow64cpu!CpupSyscallStub</span>+0x9<br/>
00000000`7480d286 : 00000000`00000000 00000000`74791904 00000000`00000000 00000000`7480d286 : <span style="color: #0000ff;">wow64cpu!Thunk0ArgReloadState</span>+0x23<br/>
…..</p>
<p>&gt; !wow64exts.sw<br/>
Switched to 32bit mode</p>
<p>0:014:x86&gt; kb<br/>
ChildEBP RetAddr Args to Child<br/>
07cf7068 7721ebf6 000010c0 00000000 00000000 ntdll_771d0000!ZwWaitForSingleObject+0x15<br/>
07cf70cc 7721eada 00000000 00000000 07cf8eec ntdll_771d0000!RtlpWaitOnCriticalSection+0x13e<br/>
07cf70f4 10062647 <span style="color: #ff0000;"><strong>100d0078</strong></span> 7d9a68e8 000c1b60 ntdll_771d0000!<span style="color: #ff0000;"><strong>RtlEnterCriticalSection</strong></span>+0x150<br/>
WARNING: Stack unwind information not available. Following frames may be wrong.<br/>
07cf7b44 10065a66 7d9a6c28 000c1b60 07cf8eec SPF!ExitThreadHook+0x46507<br/>
07cf7f84 10037629 07cf8eec 100891ec 07cf8eec SPF!ExitThreadHook+0x49926<br/>
07cf83d8 100378f2 000c1b60 0e132748 07cf8eec SPF!ExitThreadHook+0x1b4e9<br/>
07cf83f8 10029f0b 000c1b60 0000004b 0000003b SPF!ExitThreadHook+0x1b7b2<br/>
07cfa7b0 1002c4cc 002516ec 00000016 07cfc21c SPF!ExitThreadHook+0xddcb<br/>
07cfc1f0 1001b111 07cfc21c 00000000 100ce940 SPF!ExitThreadHook+0x1038c<br/>
07cfc870 75f47451 00000000 00000001 07cfc934 SPF!CheckAttachType+0xd31<br/>
07cfc88c 75f380a9 00030000 00000001 07cfc934 user32!DispatchHookW+0x38<br/>
07cfc8cc 75f38ba1 07cfc924 07cfc934 07cfc950 user32!CallHookWithSEH+0x21<br/>
07cfc90c 771e013a 07cfc924 00000000 07cfca1c user32!__fnHkINLPMSG+0x75<br/>
07cfc954 64921430 07cfc9d8 00000000 00000000 ntdll_771d0000!KiUserCallbackDispatcher+0x2e<br/>
07cfc990 649214e9 07cfc9d8 00000000 00000000 duser!CoreSC::xwProcessNL+0xfb<br/>
07cfc9b8 75f7fd3b 07cfc9d8 00000000 00000000 duser!MphProcessMessage+0x5e<br/>
07cfca0c 771e013a 07cfca24 00000000 07cfe854 user32!__ClientGetMessageMPH+0x34<br/>
07cfca38 75f40703 07cfcab4 00000000 00000000 ntdll_771d0000!KiUserCallbackDispatcher+0x2e<br/>
07cfca60 75f40769 07cfcab4 00000000 00000000 user32!_PeekMessage+0x88<br/>
07cfca8c 75f5d7ee 07cfcab4 00000000 00000000 user32!PeekMessageW+0x108<br/>
07cfcadc 75f5da5c 002516ec 001f19ba 00000008 user32!DialogBox2+0xfc<br/>
07cfcb08 75f5d98a 75b80000 0dff0b58 001f19ba user32!InternalDialogBox+0xe5<br/>
07cfcb28 75f5d70e 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamAorW+0x37<br/>
07cfcb48 75b8597b 75b80000 0dff0b58 001f19ba user32!DialogBoxIndirectParamW+0x1b<br/>
07cfcb94 6de7011a 0dff0b58 001f19ba 6495e610 comdlg32!CFileOpenSave::Show+0x181<br/>
07cfcbbc 531d56dc 54c93509 04363758 07cfe918 mfc90u!CFileDialog::DoModal+0xc5<br/>
07cfcc40 746d3c1b 06730000 00000000 746d3c3a JECM+0x56dc<br/>
07cfcc8c 6de4b325 04354e78 04356204 6de43b6b msvcr90!free+0xcd<br/>
07cfcc98 6de43b6b 04354e78 64959275 54c93352 mfc90u!CMemFile::Free+0xe<br/>
07cfccac 64959296 0673ebf0 07cfcca4 00750051 mfc90u!ATL::CStringData::Release+0x17<br/>
07cfccb0 0673ebf0 07cfcca4 00750051 6ddfee64 duser!JLog::Printf+0x166<br/>
07cfccb4 07cfcca4 00750051 6ddfee64 00000002 0x673ebf0<br/>
07cfccb8 00750051 6ddfee64 00000002 00000000 0x7cfcca4<br/>
07cfccbc 6ddfee64 00000002 00000000 00000000 0x750051<br/>
07cfccc0 00000000 00000000 00000000 00000000 mfc90u!CFileDialog::`vftable’</p>
<p>0:014:x86&gt; !cs <strong><span style="color: #ff0000;">100d0078</span></strong><br/>
—————————————–<br/>
Critical section = 0x00000000100d0078 (<span style="color: #ff0000;">SPF!ExitThreadHook+0xB3F38</span>)<br/>
DebugInfo = 0x000000000726d640<br/>
LOCKED<br/>
LockCount = 0xFFFFFFFF<br/>
WaiterWoken = Yes<br/>
OwningThread = 0x00000000000010c0<br/>
RecursionCount = 0x3004<br/>
LockSemaphore = 0x0<br/>
SpinCount = 0x0000000000000000</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
