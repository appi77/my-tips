# Windows 2022 Core NFS 설치

Windows Server 2022 Core에서 "root 매핑 허용" 설정

Root 접근 및 매핑되지 않은 사용자 접근 허용:

```bash
Set-NfsShare -Name "otmm_disk1" -AllowRootAccess $True -EnableUnmappedAccess $True

```

Anonymous UID/GID 설정 (선택 사항, 필요 시):

```bash
Set-NfsShare -Name "otmm_disk1" -AnonymousUid 0 -AnonymousGid 0
```

NTFS 권한 설정:

```bash
$Acl = Get-Acl "F:\otmm_disk1"
$AccessRule = New-Object System.Security.AccessControl.FileSystemAccessRule("ANONYMOUS LOGON", "FullControl", "ContainerInherit,ObjectInherit", "None", "Allow")
$Acl.AddAccessRule($AccessRule)
Set-Acl "F:\otmm_disk1" $Acl
```

icacls F:\otmm_disk1 /grant "ANONYMOUS LOGON:(OI)(CI)F”
icacls F:\otmm_disk1 /grant "Everyone:(OI)(CI)F”

NTFS 권한 확인  icacls 명령어를 이용한 확인 (간단):

```bash
PS F:\otmm_disk1> icacls F:\otmm_disk1
```

```bash
F:\otmm_disk1 Everyone:(OI)(CI)(F)
NT AUTHORITY\ANONYMOUS LOGON:(OI)(CI)(F)
BUILTIN\Administrators:(I)(OI)(CI)(F)
NT AUTHORITY\SYSTEM:(I)(OI)(CI)(F)
Everyone:(I)(OI)(CI)(F)
Successfully processed 1 files; Failed processing 0 files
```

NTFS 권한 확인 Get-Acl PowerShell 명령어를 이용한 확인 (상세):

```bash
(Get-Acl "F:\otmm_disk1").Access | Format-List
```

NFS 서비스 재시작 (선택 사항):

```bash
Restart-Service -DisplayName "Server for NFS"

Restart-Service -Name NfsServer -Force

```

no_root_squash 해결방법

- **NFS 서비스 관리 도구 설치 확인:**
아직 설치되지 않았다면 설치합니다.PowerShell
    
    `Install-WindowsFeature -Name FS-NFS-Service -IncludeManagementTools`
    
- **공유 설정 확인:**
먼저 `/otmm_disk1` 공유가 어떻게 설정되어 있는지 확인합니다.PowerShell
    
    `Get-NfsShare -Name otmm_disk1
    # 또는 모든 공유 목록 확인
    Get-NfsShare`
    

Windows Server 2022 Core에서 레지스트리를 통해 익명 UID/GID 설정

`regedit`을 다시 열고 다음 경로로 이동합니다.
`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default`

- `AnonymousUid`: 더블 클릭하여 **값 데이터(Value data)를 `0` (10진수)**으로 변경합니다.
- `AnonymousGid`: 더블 클릭하여 **값 데이터(Value data)를 `0` (10진수)**으로 변경합니다.

`AnonymousAccess` 값은 `2`로 두어도 무방할 수 있지만, 만약 위의 변경 후에도 문제가 지속된다면 이 값을 `1` (익명 액세스 허용, 기본 매핑 비활성화)로 변경하거나 아예 삭제하는 것을 고려해 볼 수 있습니다.