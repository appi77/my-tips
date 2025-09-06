---
title: "[DEBUG사례] Unrecognized configuration section appSettings"
date: "No Date"
---

[DEBUG사례] Unrecognized configuration section appSettings
========================================================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2019년 2월 22일
· Updated 2019년 2월 25일

#### ▶ 실제 사례

0:000> !analyze -v  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
\* \*  
\* Exception Analysis \*  
\* \*  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

FAULTING\_IP:  
KERNELBASE!RaiseException+58  
7704c54f c9 leave

EXCEPTION\_RECORD: (.exr -1)  
ExceptionAddress: 7704c54f (KERNELBASE!RaiseException+0x00000058)  
ExceptionCode: e0434f4d (CLR exception)  
ExceptionFlags: 00000001  
NumberParameters: 1  
Parameter[0]: 80131902

FAULTING\_THREAD: 000032e0

PROCESS\_NAME: CubeDisk.exe

ERROR\_CODE: (NTSTATUS) 0xe0434f4d –

EXCEPTION\_CODE: (HRESULT) 0x80131902 (2148735234) –

EXCEPTION\_PARAMETER1: 80131902

NTGLOBALFLAG: 70

APPLICATION\_VERIFIER\_FLAGS: 0

APP: SmartDisk.exe

ANALYSIS\_VERSION: 10.0.10075.9 x86fre

MANAGED\_CODE: 1

MANAGED\_ENGINE\_MODULE: mscorwks

MANAGED\_ANALYSIS\_PROVIDER: SOS

MANAGED\_THREAD\_ID: 32e0

MANAGED\_EXCEPTION\_ADDRESS: 2481d24

LAST\_CONTROL\_TRANSFER: from 00000000 to 6e48fbb4

BUGCHECK\_STR: CLR\_EXCEPTION\_System.Configuration.ConfigurationErrorsException

DEFAULT\_BUCKET\_ID: CLR\_EXCEPTION\_System.Configuration.ConfigurationErrorsException

STACK\_TEXT:  
003ceba0 6e3e1930 system\_configuration\_ni!System.Configuration.ClientConfigurationSystem.EnsureInit+0x210  
003cec54 6e3e3850 system\_configuration\_ni!System.Configuration.ClientConfigurationSystem.PrepareClientConfigSystem+0x20  
003cec60 6e459b3a system\_configuration\_ni!System.Configuration.ClientConfigurationSystem.System.Configuration.Internal.IInternalConfigSystem.RefreshConfig+0x12  
003cec70 6e4599c9 system\_configuration\_ni!System.Configuration.ConfigurationManager.RefreshSection+0x51  
003cec7c 6f3903ef system\_ni!System.Configuration.ClientSettingsStore.ReadSettings+0x8f  
003cecbc 6f36aaf0 system\_ni!System.Configuration.LocalFileSettingsProvider.GetPropertyValues+0x60  
003ced10 6f36a9b3 system\_ni!System.Configuration.SettingsBase.GetPropertiesFromProvider+0x103  
003ced4c 6f38f9f5 system\_ni!System.Configuration.SettingsBase.GetPropertyValueByName+0x85  
003ced60 6f38f91b system\_ni!System.Configuration.SettingsBase.get\_Item+0x3b  
003ced90 6f38f7a7 system\_ni!System.Configuration.ApplicationSettingsBase.GetPropertyValue+0x37  
003ceda4 6f38f71b system\_ni!System.Configuration.ApplicationSettingsBase.get\_Item+0x3b  
003cedd4 00980857 cubedisk!CubeDisk.Properties.Settings.get\_UPGRADE\_CHECK+0xf  
003cede0 00980219 cubedisk!CubeDisk.Program.Main+0x49

FOLLOWUP\_IP:  
+0  
00980857 8bf0 mov esi,eax

SYMBOL\_STACK\_INDEX: b

SYMBOL\_NAME: cubedisk!CubeDisk.Properties.Settings.get\_UPGRADE\_CHECK+f

FOLLOWUP\_NAME: MachineOwner

MODULE\_NAME: cubedisk

IMAGE\_NAME: CubeDisk.exe

DEBUG\_FLR\_IMAGE\_TIMESTAMP: 0

STACK\_COMMAND: \*\* Pseudo Context \*\* ; kb

BUCKET\_ID: CLR\_EXCEPTION\_System.Configuration.ConfigurationErrorsException\_cubedisk!CubeDisk.Properties.Settings.get\_UPGRADE\_CHECK+f

PRIMARY\_PROBLEM\_CLASS: CLR\_EXCEPTION\_System.Configuration.ConfigurationErrorsException\_cubedisk!CubeDisk.Properties.Settings.get\_UPGRADE\_CHECK+f

FAILURE\_PROBLEM\_CLASS: CLR\_EXCEPTION\_System.Configuration.ConfigurationErrorsException

FAILURE\_EXCEPTION\_CODE: 80131902

FAILURE\_IMAGE\_NAME: CubeDisk.exe

FAILURE\_FUNCTION\_NAME: CubeDisk.Properties.Settings.get\_UPGRADE\_CHECK

FAILURE\_SYMBOL\_NAME: CubeDisk.exe!CubeDisk.Properties.Settings.get\_UPGRADE\_CHECK

FAILURE\_BUCKET\_ID: CLR\_EXCEPTION\_System.Configuration.ConfigurationErrorsException\_80131902\_CubeDisk.exe!CubeDisk.Properties.Settings.get\_UPGRADE\_CHECK

ANALYSIS\_SOURCE: UM

FAILURE\_ID\_HASH\_STRING: um:clr\_exception\_system.configuration.configurationerrorsexception\_80131902\_SmartDisk.exe!cubedisk.properties.settings.get\_upgrade\_check

FAILURE\_ID\_HASH: {795f2366-b1b6-836e-4122-f5d3514a6ec8}

Followup: MachineOwner  
———

0:000> !pe  
Exception object: 02481d24  
Exception type: System.Configuration.ConfigurationErrorsException  
Message: 구성 시스템을 초기화하지 못했습니다.  
InnerException: System.Configuration.ConfigurationErrorsException, use !PrintException 02481a7c to see more  
StackTrace (generated):  
SP IP Function  
003CEBA0 6E3E1930 System\_Configuration\_ni!System.Configuration.ClientConfigurationSystem.EnsureInit(System.String)+0x210  
003CEC54 6E3E3850 System\_Configuration\_ni!System.Configuration.ClientConfigurationSystem.PrepareClientConfigSystem(System.String)+0x20  
003CEC60 6E459B3A System\_Configuration\_ni!System.Configuration.ClientConfigurationSystem.System.Configuration.Internal.IInternalConfigSystem.RefreshConfig(System.String)+0x12  
003CEC70 6E4599C9 System\_Configuration\_ni!System.Configuration.ConfigurationManager.RefreshSection(System.String)+0x51  
003CEC7C 6F3903EF System\_ni!System.Configuration.ClientSettingsStore.ReadSettings(System.String, Boolean)+0x8f  
003CECBC 6F36AAF0 System\_ni!System.Configuration.LocalFileSettingsProvider.GetPropertyValues(System.Configuration.SettingsContext, System.Configuration.SettingsPropertyCollection)+0x60  
003CED10 6F36A9B3 System\_ni!System.Configuration.SettingsBase.GetPropertiesFromProvider(System.Configuration.SettingsProvider)+0x103  
003CED4C 6F38F9F5 System\_ni!System.Configuration.SettingsBase.GetPropertyValueByName(System.String)+0x85  
003CED60 6F38F91B System\_ni!System.Configuration.SettingsBase.get\_Item(System.String)+0x3b  
003CED90 6F38F7A7 System\_ni!System.Configuration.ApplicationSettingsBase.GetPropertyValue(System.String)+0x37  
003CEDA4 6F38F71B System\_ni!System.Configuration.ApplicationSettingsBase.get\_Item(System.String)+0x3b  
003CEDD4 00980857 CubeDisk!CubeDisk.Properties.Settings.get\_UPGRADE\_CHECK()+0xf  
003CEDE0 00980219 CubeDisk!CubeDisk.Program.Main(System.String[])+0x49

StackTraceString:   
HResult: 80131902  
There are nested exceptions on this thread. Run with -nested for details  
0:000> !do 02481d24  
Name: System.Configuration.ConfigurationErrorsException  
MethodTable: 6e3f6ae4  
EEClass: 6e3c288c  
Size: 92(0x5c) bytes  
(C:\Windows\assembly\GAC\_MSIL\System.Configuration\2.0.0.0\_\_b03f5f7f11d50a3a\System.Configuration.dll)  
Fields:  
MT Field Offset Type VT Attr Value Name  
701d0f1c 40000b5 4 System.String 0 instance 00000000 \_className  
701d0390 40000b6 8 …ection.MethodBase 0 instance 00000000 \_exceptionMethod  
701d0f1c 40000b7 c System.String 0 instance 00000000 \_exceptionMethodString  
701d0f1c 40000b8 10 System.String 0 instance 02481dd0 \_message  
701ca878 40000b9 14 …tions.IDictionary 0 instance 00000000 \_data  
701d10b0 40000ba 18 System.Exception 0 instance 02481a7c \_innerException  
701d0f1c 40000bb 1c System.String 0 instance 00000000 \_helpURL  
701d0b38 40000bc 20 System.Object 0 instance 02481fa4 \_stackTrace  
701d0f1c 40000bd 24 System.String 0 instance 00000000 \_stackTraceString  
701d0f1c 40000be 28 System.String 0 instance 00000000 \_remoteStackTraceString  
701d3168 40000bf 34 System.Int32 1 instance 0 \_remoteStackIndex  
701d0b38 40000c0 2c System.Object 0 instance 00000000 \_dynamicMethods  
701d3168 40000c1 38 System.Int32 1 instance -2146232062 \_HResult  
701d0f1c 40000c2 30 System.String 0 instance 00000000 \_source  
701d37e4 40000c3 3c System.IntPtr 1 instance 0 \_xptrs  
701d3168 40000c4 40 System.Int32 1 instance -532459699 \_xcode  
701d0f1c 400317e 44 System.String 0 instance 00000000 \_filename  
701d3168 400317f 48 System.Int32 1 instance 0 \_line  
701d0f1c 4000254 4c System.String 0 instance 00000000 \_firstFilename  
701d3168 4000255 54 System.Int32 1 instance 0 \_firstLine  
701a46ec 4000256 50 System.Object[] 0 instance 00000000 \_errors  
0:000> !do 02481a7c  
Name: System.Configuration.ConfigurationErrorsException  
MethodTable: 6e3f6ae4  
EEClass: 6e3c288c  
Size: 92(0x5c) bytes  
(C:\Windows\assembly\GAC\_MSIL\System.Configuration\2.0.0.0\_\_b03f5f7f11d50a3a\System.Configuration.dll)  
Fields:  
MT Field Offset Type VT Attr Value Name  
701d0f1c 40000b5 4 System.String 0 instance 00000000 \_className  
701d0390 40000b6 8 …ection.MethodBase 0 instance 00000000 \_exceptionMethod  
701d0f1c 40000b7 c System.String 0 instance 00000000 \_exceptionMethodString  
701d0f1c 40000b8 10 System.String 0 instance 02480e68 \_message  
701ca878 40000b9 14 …tions.IDictionary 0 instance 00000000 \_data  
701d10b0 40000ba 18 System.Exception 0 instance 00000000 \_innerException  
701d0f1c 40000bb 1c System.String 0 instance 00000000 \_helpURL  
701d0b38 40000bc 20 System.Object 0 instance 02481cb8 \_stackTrace  
701d0f1c 40000bd 24 System.String 0 instance 00000000 \_stackTraceString  
701d0f1c 40000be 28 System.String 0 instance 00000000 \_remoteStackTraceString  
701d3168 40000bf 34 System.Int32 1 instance 0 \_remoteStackIndex  
701d0b38 40000c0 2c System.Object 0 instance 00000000 \_dynamicMethods  
701d3168 40000c1 38 System.Int32 1 instance -2146232062 \_HResult  
701d0f1c 40000c2 30 System.String 0 instance 00000000 \_source  
701d37e4 40000c3 3c System.IntPtr 1 instance 0 \_xptrs  
701d3168 40000c4 40 System.Int32 1 instance -532459699 \_xcode  
701d0f1c 400317e 44 System.String 0 instance 00000000 \_filename  
701d3168 400317f 48 System.Int32 1 instance 0 \_line  
701d0f1c 4000254 4c System.String 0 instance 02449fec \_firstFilename  
701d3168 4000255 54 System.Int32 1 instance 8 \_firstLine  
701a46ec 4000256 50 System.Object[] 0 instance 00000000 \_errors  
0:000> !do 02480e68  
Name: System.String  
MethodTable: 701d0f1c  
EEClass: 6ff8d66c  
Size: 78(0x4e) bytes  
(C:\Windows\assembly\GAC\_32\mscorlib\2.0.0.0\_\_b77a5c561934e089\mscorlib.dll)  
String: 인식할 수 없는 구성 섹션 startup입니다.  
Fields:  
MT Field Offset Type VT Attr Value Name  
701d3168 4000096 4 System.Int32 1 instance 31 m\_arrayLength  
701d3168 4000097 8 System.Int32 1 instance 26 m\_stringLength  
701d1bfc 4000098 c System.Char 1 instance ffffc778 m\_firstChar  
701d0f1c 4000099 10 System.String 0 shared static Empty  
>> Domain:Value 00113ac8:02441198 <<  
701d1b4c 400009a 14 System.Char[] 0 shared static WhitespaceChars  
>> Domain:Value 00113ac8:02441954 <<

C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG\machine.config 파일에 start 섹션에 잘못된 항목이 있음을 나타냅니다 . 따라서 잘 작동하는 PC에서 machine.config 파일의 appSettings 섹션을 비교해 보세요.  
예)

```html
<article class="post-566 post type-post status-publish format-standard hentry category-debug"><div class="post-inner group">
<h1 class="post-title entry-title">[DEBUG사례] Unrecognized configuration section appSettings</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2019년 2월 22일">2019년 2월 22일</time>
              · Updated <time class="updated" datetime="2019년 2월 25일">2019년 2월 25일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<h4 align="left"><span lang="EN-US">▶ </span><span lang="EN-US">실제 사례</span></h4>
<p>0:000&gt; !analyze -v<br/>
*******************************************************************************<br/>
* *<br/>
* Exception Analysis *<br/>
* *<br/>
*******************************************************************************</p>
<p>FAULTING_IP:<br/>
KERNELBASE!RaiseException+58<br/>
7704c54f c9 leave</p>
<p>EXCEPTION_RECORD: (.exr -1)<br/>
ExceptionAddress: 7704c54f (KERNELBASE!RaiseException+0x00000058)<br/>
ExceptionCode: e0434f4d (CLR exception)<br/>
ExceptionFlags: 00000001<br/>
NumberParameters: 1<br/>
Parameter[0]: 80131902</p>
<p>FAULTING_THREAD: 000032e0</p>
<p>PROCESS_NAME: CubeDisk.exe</p>
<p>ERROR_CODE: (NTSTATUS) 0xe0434f4d – <unable code="" error="" get="" text="" to=""></unable></p>
<p>EXCEPTION_CODE: (HRESULT) 0x80131902 (2148735234) – <unable code="" error="" get="" text="" to=""></unable></p>
<p>EXCEPTION_PARAMETER1: 80131902</p>
<p>NTGLOBALFLAG: 70</p>
<p>APPLICATION_VERIFIER_FLAGS: 0</p>
<p>APP: SmartDisk.exe</p>
<p>ANALYSIS_VERSION: 10.0.10075.9 x86fre</p>
<p>MANAGED_CODE: 1</p>
<p>MANAGED_ENGINE_MODULE: mscorwks</p>
<p>MANAGED_ANALYSIS_PROVIDER: SOS</p>
<p>MANAGED_THREAD_ID: 32e0</p>
<p>MANAGED_EXCEPTION_ADDRESS: 2481d24</p>
<p>LAST_CONTROL_TRANSFER: from 00000000 to 6e48fbb4</p>
<p>BUGCHECK_STR: CLR_EXCEPTION_System.Configuration.ConfigurationErrorsException</p>
<p>DEFAULT_BUCKET_ID: CLR_EXCEPTION_System.Configuration.ConfigurationErrorsException</p>
<p>STACK_TEXT:<br/>
003ceba0 6e3e1930 system_configuration_ni!System.Configuration.ClientConfigurationSystem.EnsureInit+0x210<br/>
003cec54 6e3e3850 system_configuration_ni!System.Configuration.ClientConfigurationSystem.PrepareClientConfigSystem+0x20<br/>
003cec60 6e459b3a system_configuration_ni!System.Configuration.ClientConfigurationSystem.System.Configuration.Internal.IInternalConfigSystem.RefreshConfig+0x12<br/>
003cec70 6e4599c9 system_configuration_ni!System.Configuration.ConfigurationManager.RefreshSection+0x51<br/>
003cec7c 6f3903ef system_ni!System.Configuration.ClientSettingsStore.ReadSettings+0x8f<br/>
003cecbc 6f36aaf0 system_ni!System.Configuration.LocalFileSettingsProvider.GetPropertyValues+0x60<br/>
003ced10 6f36a9b3 system_ni!System.Configuration.SettingsBase.GetPropertiesFromProvider+0x103<br/>
003ced4c 6f38f9f5 system_ni!System.Configuration.SettingsBase.GetPropertyValueByName+0x85<br/>
003ced60 6f38f91b system_ni!System.Configuration.SettingsBase.get_Item+0x3b<br/>
003ced90 6f38f7a7 system_ni!System.Configuration.ApplicationSettingsBase.GetPropertyValue+0x37<br/>
003ceda4 6f38f71b system_ni!System.Configuration.ApplicationSettingsBase.get_Item+0x3b<br/>
003cedd4 00980857 cubedisk!CubeDisk.Properties.Settings.get_UPGRADE_CHECK+0xf<br/>
003cede0 00980219 cubedisk!CubeDisk.Program.Main+0x49</p>
<p>FOLLOWUP_IP:<br/>
+0<br/>
00980857 8bf0 mov esi,eax</p>
<p>SYMBOL_STACK_INDEX: b</p>
<p>SYMBOL_NAME: cubedisk!CubeDisk.Properties.Settings.get_UPGRADE_CHECK+f</p>
<p>FOLLOWUP_NAME: MachineOwner</p>
<p>MODULE_NAME: cubedisk</p>
<p>IMAGE_NAME: CubeDisk.exe</p>
<p>DEBUG_FLR_IMAGE_TIMESTAMP: 0</p>
<p>STACK_COMMAND: ** Pseudo Context ** ; kb</p>
<p>BUCKET_ID: CLR_EXCEPTION_System.Configuration.ConfigurationErrorsException_cubedisk!CubeDisk.Properties.Settings.get_UPGRADE_CHECK+f</p>
<p>PRIMARY_PROBLEM_CLASS: CLR_EXCEPTION_System.Configuration.ConfigurationErrorsException_cubedisk!CubeDisk.Properties.Settings.get_UPGRADE_CHECK+f</p>
<p>FAILURE_PROBLEM_CLASS: CLR_EXCEPTION_System.Configuration.ConfigurationErrorsException</p>
<p>FAILURE_EXCEPTION_CODE: 80131902</p>
<p>FAILURE_IMAGE_NAME: CubeDisk.exe</p>
<p>FAILURE_FUNCTION_NAME: CubeDisk.Properties.Settings.get_UPGRADE_CHECK</p>
<p>FAILURE_SYMBOL_NAME: CubeDisk.exe!CubeDisk.Properties.Settings.get_UPGRADE_CHECK</p>
<p>FAILURE_BUCKET_ID: CLR_EXCEPTION_System.Configuration.ConfigurationErrorsException_80131902_CubeDisk.exe!CubeDisk.Properties.Settings.get_UPGRADE_CHECK</p>
<p>ANALYSIS_SOURCE: UM</p>
<p>FAILURE_ID_HASH_STRING: um:clr_exception_system.configuration.configurationerrorsexception_80131902_SmartDisk.exe!cubedisk.properties.settings.get_upgrade_check</p>
<p>FAILURE_ID_HASH: {795f2366-b1b6-836e-4122-f5d3514a6ec8}</p>
<p>Followup: MachineOwner<br/>
———</p>
<p>0:000&gt; !pe<br/>
Exception object: 02481d24<br/>
Exception type: System.Configuration.ConfigurationErrorsException<br/>
Message: 구성 시스템을 초기화하지 못했습니다.<br/>
InnerException: System.Configuration.ConfigurationErrorsException, use !PrintException 02481a7c to see more<br/>
StackTrace (generated):<br/>
SP IP Function<br/>
003CEBA0 6E3E1930 System_Configuration_ni!System.Configuration.ClientConfigurationSystem.EnsureInit(System.String)+0x210<br/>
003CEC54 6E3E3850 System_Configuration_ni!System.Configuration.ClientConfigurationSystem.PrepareClientConfigSystem(System.String)+0x20<br/>
003CEC60 6E459B3A System_Configuration_ni!System.Configuration.ClientConfigurationSystem.System.Configuration.Internal.IInternalConfigSystem.RefreshConfig(System.String)+0x12<br/>
003CEC70 6E4599C9 System_Configuration_ni!System.Configuration.ConfigurationManager.RefreshSection(System.String)+0x51<br/>
003CEC7C 6F3903EF System_ni!System.Configuration.ClientSettingsStore.ReadSettings(System.String, Boolean)+0x8f<br/>
003CECBC 6F36AAF0 System_ni!System.Configuration.LocalFileSettingsProvider.GetPropertyValues(System.Configuration.SettingsContext, System.Configuration.SettingsPropertyCollection)+0x60<br/>
003CED10 6F36A9B3 System_ni!System.Configuration.SettingsBase.GetPropertiesFromProvider(System.Configuration.SettingsProvider)+0x103<br/>
003CED4C 6F38F9F5 System_ni!System.Configuration.SettingsBase.GetPropertyValueByName(System.String)+0x85<br/>
003CED60 6F38F91B System_ni!System.Configuration.SettingsBase.get_Item(System.String)+0x3b<br/>
003CED90 6F38F7A7 System_ni!System.Configuration.ApplicationSettingsBase.GetPropertyValue(System.String)+0x37<br/>
003CEDA4 6F38F71B System_ni!System.Configuration.ApplicationSettingsBase.get_Item(System.String)+0x3b<br/>
003CEDD4 00980857 CubeDisk!CubeDisk.Properties.Settings.get_UPGRADE_CHECK()+0xf<br/>
003CEDE0 00980219 CubeDisk!CubeDisk.Program.Main(System.String[])+0x49</p>
<p>StackTraceString: <none><br/>
HResult: 80131902<br/>
There are nested exceptions on this thread. Run with -nested for details<br/>
0:000&gt; !do 02481d24<br/>
Name: System.Configuration.ConfigurationErrorsException<br/>
MethodTable: 6e3f6ae4<br/>
EEClass: 6e3c288c<br/>
Size: 92(0x5c) bytes<br/>
(C:\Windows\assembly\GAC_MSIL\System.Configuration\2.0.0.0__b03f5f7f11d50a3a\System.Configuration.dll)<br/>
Fields:<br/>
MT Field Offset Type VT Attr Value Name<br/>
701d0f1c 40000b5 4 System.String 0 instance 00000000 _className<br/>
701d0390 40000b6 8 …ection.MethodBase 0 instance 00000000 _exceptionMethod<br/>
701d0f1c 40000b7 c System.String 0 instance 00000000 _exceptionMethodString<br/>
701d0f1c 40000b8 10 System.String 0 instance 02481dd0 _message<br/>
701ca878 40000b9 14 …tions.IDictionary 0 instance 00000000 _data<br/>
701d10b0 40000ba 18 System.Exception 0 instance 02481a7c _innerException<br/>
701d0f1c 40000bb 1c System.String 0 instance 00000000 _helpURL<br/>
701d0b38 40000bc 20 System.Object 0 instance 02481fa4 _stackTrace<br/>
701d0f1c 40000bd 24 System.String 0 instance 00000000 _stackTraceString<br/>
701d0f1c 40000be 28 System.String 0 instance 00000000 _remoteStackTraceString<br/>
701d3168 40000bf 34 System.Int32 1 instance 0 _remoteStackIndex<br/>
701d0b38 40000c0 2c System.Object 0 instance 00000000 _dynamicMethods<br/>
701d3168 40000c1 38 System.Int32 1 instance -2146232062 _HResult<br/>
701d0f1c 40000c2 30 System.String 0 instance 00000000 _source<br/>
701d37e4 40000c3 3c System.IntPtr 1 instance 0 _xptrs<br/>
701d3168 40000c4 40 System.Int32 1 instance -532459699 _xcode<br/>
701d0f1c 400317e 44 System.String 0 instance 00000000 _filename<br/>
701d3168 400317f 48 System.Int32 1 instance 0 _line<br/>
701d0f1c 4000254 4c System.String 0 instance 00000000 _firstFilename<br/>
701d3168 4000255 54 System.Int32 1 instance 0 _firstLine<br/>
701a46ec 4000256 50 System.Object[] 0 instance 00000000 _errors<br/>
0:000&gt; !do 02481a7c<br/>
Name: System.Configuration.ConfigurationErrorsException<br/>
MethodTable: 6e3f6ae4<br/>
EEClass: 6e3c288c<br/>
Size: 92(0x5c) bytes<br/>
(C:\Windows\assembly\GAC_MSIL\System.Configuration\2.0.0.0__b03f5f7f11d50a3a\System.Configuration.dll)<br/>
Fields:<br/>
MT Field Offset Type VT Attr Value Name<br/>
701d0f1c 40000b5 4 System.String 0 instance 00000000 _className<br/>
701d0390 40000b6 8 …ection.MethodBase 0 instance 00000000 _exceptionMethod<br/>
701d0f1c 40000b7 c System.String 0 instance 00000000 _exceptionMethodString<br/>
701d0f1c 40000b8 10 System.String 0 instance 02480e68 _message<br/>
701ca878 40000b9 14 …tions.IDictionary 0 instance 00000000 _data<br/>
701d10b0 40000ba 18 System.Exception 0 instance 00000000 _innerException<br/>
701d0f1c 40000bb 1c System.String 0 instance 00000000 _helpURL<br/>
701d0b38 40000bc 20 System.Object 0 instance 02481cb8 _stackTrace<br/>
701d0f1c 40000bd 24 System.String 0 instance 00000000 _stackTraceString<br/>
701d0f1c 40000be 28 System.String 0 instance 00000000 _remoteStackTraceString<br/>
701d3168 40000bf 34 System.Int32 1 instance 0 _remoteStackIndex<br/>
701d0b38 40000c0 2c System.Object 0 instance 00000000 _dynamicMethods<br/>
701d3168 40000c1 38 System.Int32 1 instance -2146232062 _HResult<br/>
701d0f1c 40000c2 30 System.String 0 instance 00000000 _source<br/>
701d37e4 40000c3 3c System.IntPtr 1 instance 0 _xptrs<br/>
701d3168 40000c4 40 System.Int32 1 instance -532459699 _xcode<br/>
701d0f1c 400317e 44 System.String 0 instance 00000000 _filename<br/>
701d3168 400317f 48 System.Int32 1 instance 0 _line<br/>
701d0f1c 4000254 4c System.String 0 instance 02449fec _firstFilename<br/>
701d3168 4000255 54 System.Int32 1 instance 8 _firstLine<br/>
701a46ec 4000256 50 System.Object[] 0 instance 00000000 _errors<br/>
0:000&gt; !do 02480e68<br/>
Name: System.String<br/>
MethodTable: 701d0f1c<br/>
EEClass: 6ff8d66c<br/>
Size: 78(0x4e) bytes<br/>
(C:\Windows\assembly\GAC_32\mscorlib\2.0.0.0__b77a5c561934e089\mscorlib.dll)<br/>
String: 인식할 수 없는 구성 섹션 startup입니다.<br/>
Fields:<br/>
MT Field Offset Type VT Attr Value Name<br/>
701d3168 4000096 4 System.Int32 1 instance 31 m_arrayLength<br/>
701d3168 4000097 8 System.Int32 1 instance 26 m_stringLength<br/>
701d1bfc 4000098 c System.Char 1 instance ffffc778 m_firstChar<br/>
701d0f1c 4000099 10 System.String 0 shared static Empty<br/>
&gt;&gt; Domain:Value 00113ac8:02441198 &lt;&lt;<br/>
701d1b4c 400009a 14 System.Char[] 0 shared static WhitespaceChars<br/>
&gt;&gt; Domain:Value 00113ac8:02441954 &lt;&lt;</none></p>
<p>C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG\machine.config 파일에 start 섹션에 잘못된 항목이 있음을 나타냅니다 . 따라서 잘 작동하는 PC에서 machine.config 파일의 appSettings 섹션을 비교해 보세요.<br/>
예)<br/>
<section allowlocation="”false”/" culture="neutral," name="”startup”" publickeytoken="b03f5f7f11d50a3a”" system.configuration,="" type="”System.Configuration.IgnoreSection," version="2.0.0.0,"></section></p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
