# RTX 3070 Ti 언락 실험 — 처음 하는 분도 따라가는 한국어 안내

**받으신 ZIP을 풀고, 아래 1번부터 순서대로 따라 해주세요.** 어려운 용어를 외울 필요는 없습니다. 파일 이름과 명령어는 그대로 사용하시면 됩니다.

이 안내는 **라이젠 5600X + GIGABYTE B550M AORUS ELITE + ASUS TUF RTX 3070 Ti** 구성에 맞춰 정리했습니다. 다만 이 PC에서 실제 언락에 성공한 것은 아직 아닙니다. 준비 도구는 검사했지만, 실제 적용·안정성·성능은 해당 PC에서 확인해야 합니다.

**전체 순서:** ZIP 풀기 → PC 점검 → 파일 준비 → 펌웨어 파일 만들기 → USB 복사 → F12로 USB 부팅 → 화면 확인 후 U → 결과 확인.

**이 PC는 아래 1~9번 순서대로 진행해주세요.**

앞부분은 Windows에서 진행합니다. **마지막 적용은 USB로 부팅한 뒤 직접 `U`를 눌러 진행합니다.** 더블클릭 한 번으로 모든 과정이 끝나는 프로그램은 아닙니다. 게임 FPS가 올라간다는 보장도 없습니다.

## 전달하는 분께 — 이대로 보내시면 됩니다

[전달용 ZIP 바로 내려받기](https://github.com/gigaminkyu/rtx3070ti-windows-guide/raw/refs/heads/main/RTX3070Ti-OtherPC-Experiment.zip)를 누르세요. **이 설명서와 ZIP은 로그인 없이 볼 수 있습니다.** 이 페이지 링크 또는 ZIP 파일을 상대방에게 전달하시면 됩니다.

함께 보낼 메시지:

> 이 ZIP을 다운로드 폴더에 저장하고, 우클릭해서 ‘모두 압축 풀기’를 해줘. 안에 있는 `00-먼저읽어주세요.txt`부터 열면 돼. 설명서에 클릭할 곳과 복사할 명령어를 순서대로 적어뒀어. 오류가 나오면 다음 단계로 넘어가지 말고 화면을 보내줘. 실제 언락이 성공할지, 게임이 빨라질지는 아직 확인 전이야.

## 1. ZIP을 풀고 설명서를 열어주세요

1. 받은 `RTX3070Ti-OtherPC-Experiment.zip`을 **다운로드 폴더**에 저장하세요.
2. ZIP을 마우스 오른쪽 버튼으로 누르고 **모두 압축 풀기**를 선택하세요. 압축 프로그램을 쓰고 있다면 ‘압축 풀기’를 선택하셔도 됩니다.
3. 압축이 풀린 폴더 안에서 **`RTX3070Ti-OtherPC` 폴더**를 여세요.
4. **`00-먼저읽어주세요.txt`를 더블클릭**하세요. Windows 메모장으로 읽을 수 있습니다. 자세한 설명은 같은 폴더의 `START-HERE.ko.txt`에도 들어 있습니다.

**잘 됐나요?** 같은 폴더 안에 `Run-3070Ti-Intake.cmd`와 `RUN-PREPARE.cmd`가 보이면 맞습니다. ZIP 안에서 바로 실행하지 말고, 반드시 압축을 푼 다음 실행해주세요. 준비는 PC의 로컬 NTFS 디스크(보통 Windows의 C: 드라이브)에서 진행하며, USB 안에서 실행하지 않습니다.

파일 끝의 `.cmd`나 `.txt`가 안 보일 수도 있습니다. Windows가 확장자를 숨겨둔 경우이므로, 앞부분 이름을 확인하세요. 파일 이름을 직접 바꾸실 필요는 없습니다.

## 2. 내 PC가 맞는지 먼저 점검해주세요

1. **`Run-3070Ti-Intake.cmd`를 우클릭**하세요.
2. **관리자 권한으로 실행**을 누르세요. Windows 11에서 메뉴가 안 보이면 ‘더 많은 옵션 표시’를 먼저 눌러보세요.
3. 본인이 방금 실행한 파일의 Windows 권한 확인 창이면 **예**를 누르세요.
4. 검은색 창에 결과가 나올 때까지 기다리세요. 이 단계는 PC 정보를 읽어 결과 파일만 만듭니다. GPU 언락은 시작되지 않습니다.

화면에 아래 영어 중 하나가 나옵니다.

| 화면에 나온 문구 | 한국어 뜻 / 다음 행동 |
|---|---|
| `RTX3070TI_FOUND_UNVALIDATED` | 3070 Ti가 확인됐습니다. **언락 성공이라는 뜻은 아닙니다.** 아래 보안 상태도 확인해주세요. |
| `REFERENCE_FIELDS_MATCH_NOT_VALIDATED` | 과거 참고 PC와 조회 항목이 같습니다. 이것도 언락 성공 판정은 아닙니다. |
| `NOT_RTX3070TI` | 3070 Ti를 확인하지 못했습니다. 여기서 멈추고 결과를 전달해주세요. |
| `INCOMPLETE` | 필요한 정보를 읽지 못했습니다. 여기서 멈추고 결과를 전달해주세요. |

### 결과 파일은 어디에 있나요?

방금 실행한 파일이 있는 폴더에서 `output` → 가장 최근 날짜·시간 폴더 → `inventory.json` 순서로 여세요. 우클릭 → 연결 프로그램 → 메모장으로 열 수 있습니다. 이 파일이 점검 결과입니다. 화면의 `ReportFile`에도 위치가 나옵니다.

`MissingInformation`은 **읽지 못한 정보**라는 뜻입니다. `Unknown`은 **확인하지 못함**이지, ‘꺼져 있음’이나 ‘문제없음’이라는 뜻이 아닙니다.

### USB 부팅 전에 확인할 두 가지

`inventory.json`에서 `Security` 아래 항목을 확인하세요. 메모장에서는 `Ctrl + F`로 이름을 찾을 수 있습니다.

| 항목 | 의미 / 진행 조건 |
|---|---|
| `SecureBoot` | `Disabled`는 꺼짐, `Enabled`는 켜짐입니다. 이 실험용 USB는 Secure Boot가 켜진 상태에서 실행할 수 없습니다. **Enabled 또는 Unknown이면 USB 부팅 단계로 넘어가지 마세요.** |
| `OsVolume` | Windows 드라이브의 암호화 상태입니다. `VolumeStatus: FullyDecrypted`, `ProtectionStatus: Off`, `EncryptionPercentage: 0`이면 암호화되지 않은 상태로 조회된 것입니다. 다른 값이거나 모르면 여기서 멈추고 확인해주세요. |

**`ProtectionStatus: Off` 하나만 보고 암호화가 해제됐다고 판단하지 마세요.** 암호화된 PC에서는 소유자가 복구키를 확보하고 부팅 변경에 따른 복구 절차를 이해한 뒤 별도로 준비해야 합니다. 복구키 자체는 누구에게도 보내지 마세요. 이 설명서는 암호화 해제나 보안 설정 변경을 자동으로 하지 않습니다.

현재 BIOS 버전과 보드 리비전을 모르기 때문에, Secure Boot를 끄는 메뉴 위치를 임의로 적지 않았습니다. 위 조건을 확인하지 못했다면 **점검 결과까지만 전달**해주세요. BIOS 업데이트나 초기화를 시도할 필요는 없습니다.

## 3. 인터넷에서 필요한 파일을 준비해주세요

1. 압축을 풀었던 폴더로 돌아가세요.
2. **`RUN-PREPARE.cmd`를 더블클릭**하세요. 이 파일은 관리자 권한이 필요 없습니다.
3. 인터넷에서 파일 두 개를 받습니다. `Downloading`은 **다운로드 중**이라는 뜻입니다. 완료될 때까지 기다려주세요.
4. 아래의 완료 문구와 폴더 경로를 확인하세요.

| 화면 문구 | 뜻 |
|---|---|
| `Prepared only. No EXE/EFI was executed.` | 필요한 파일 준비가 끝났습니다. 아직 언락 프로그램은 실행하지 않았습니다. |
| `Output: ...` | 준비된 파일이 들어 있는 폴더입니다. |
| `Set-Location -LiteralPath '...'` | 다음 단계에서 사용할 **폴더 이동 명령어**입니다. 이 줄을 복사해두세요. |
| `Preparation finished or stopped. Read the result above.` | 실행기가 마지막에 표시하는 안내입니다. **이 문구만으로 성공이라고 판단하지 마세요.** 위에 오류가 없는지 확인해야 합니다. |

**잘 됐나요?** `prepared-날짜-고유번호`라는 새 폴더가 생기고, 안에 `EFI`, `RTX-UNLOCK`, `firmware-assets.exe`, `PREPARATION.json`이 있으면 준비 결과를 확인할 수 있습니다. `PREPARATION.json`의 `PREPARED_ONLY_NOT_HARDWARE_VALIDATED`도 ‘파일 준비만 완료, 실제 PC 적용은 미확인’이라는 뜻입니다.

**여기서 멈춰야 하는 경우:** 빨간 오류, `SHA256 mismatch`, `Unsafe ZIP path`, `Refusing to overwrite`, 다운로드 실패가 나오면 다음으로 넘어가지 마세요. 창의 오류를 복사하거나 사진으로 남겨주세요. 백신이나 조직 정책이 차단했을 때 임의로 끄거나 우회하지 마세요.

동봉 실행기는 이 PowerShell 실행 한 번에만 `ExecutionPolicy Bypass`를 사용합니다. Windows의 영구 실행 정책은 바꾸지 않습니다. 이 준비 단계는 파일 다운로드·검사·압축 해제까지만 합니다.

## 4. PowerShell을 열고 펌웨어 파일을 만들어주세요

펌웨어 파일은 다음 USB 부팅에서 필요한 자료입니다. 여기서는 제작자가 배포한 `firmware-assets.exe`를 직접 실행합니다. **가이드 작성 과정에서는 이 EXE를 실행하지 않았습니다.**

### 4-1. PowerShell을 여세요

1. 키보드의 **Windows 키**를 누르세요.
2. **Windows PowerShell**을 검색하세요.
3. **Windows PowerShell**을 여세요. `PowerShell ISE`나 `명령 프롬프트`는 선택하지 마세요. 이 단계는 관리자 권한이 필요 없습니다.
4. 3번의 준비 완료 화면에서 **`Set-Location -LiteralPath '...'` 한 줄 전체**를 복사해서 새 PowerShell 창에 붙여 넣고 **Enter**를 누르세요.

이 명령은 방금 만들어진 `prepared-...` 폴더로 이동하는 것입니다. **따옴표와 실제 경로까지 통째로 복사**해주세요. 예시의 점 세 개 `...`를 직접 입력하는 것이 아닙니다. 준비 창을 닫았다면 파일 준비를 다시 실행해 새로 나온 경로를 사용해도 됩니다. 이때는 이후 단계도 새 폴더 기준으로 진행하세요.

### 4-2. 아래 상자 전체를 복사해서 실행하세요

아래 코드의 첫 줄부터 마지막 줄까지 복사한 뒤, 같은 PowerShell 창에 붙여 넣으세요. 입력만 되고 실행되지 않으면 **Enter**를 한 번 누르세요. 복붙할 때 코드 상자 바깥의 설명이나 ``` 기호는 넣지 않습니다.

```powershell
$ErrorActionPreference = 'Stop'
if (-not (Test-Path -LiteralPath '.\firmware-assets.exe' -PathType Leaf)) { throw '준비 완료 화면의 Set-Location 명령으로 먼저 이동하세요.' }
if (-not (Test-Path -LiteralPath '.\RTX-UNLOCK\DEBUG.ON' -PathType Leaf)) { throw 'DEBUG.ON이 없습니다. 준비 도구부터 다시 실행하세요.' }
& '.\firmware-assets.exe'
if ($LASTEXITCODE -ne 0) { throw '펌웨어 생성 실패입니다. USB 부팅으로 넘어가지 마세요.' }
```

다운로드와 파일 생성이 끝날 때까지 기다려주세요. **오류가 나오면 4-3이나 USB 단계로 넘어가지 않습니다.** 실행이 막히거나 파일이 누락되면 오류 문구를 남겨주세요.

### 4-3. 만들어진 파일이 맞는지 검사하세요

같은 PowerShell 창에서 아래 코드 전체를 복사해서 실행하세요. 길어 보여도 고칠 부분은 없습니다. 파일 이름과 해시를 비교하는 검사입니다. **해시란 ‘같은 파일인지 확인하는 지문’이라고 생각하시면 됩니다.**

```powershell
$ErrorActionPreference = 'Stop'
$RtxAssetHashes = [ordered]@{
    'gsp_ga10x.bin' = '572373620a37418f24dc16b5031c39338778c3257e48e8408de9a57291b24f3a'
    'v67-ga102-610.43.03.bin' = '2a0aa1f86d0b6afff5214d641d87d46dc98ef06ed908ff05d0ddbad5ffb7e197'
    'booter_load_ga102.bin' = '056cbc064a888f80717726c54d7f64fcd68044d123870c95a74f37f4975dcaa4'
    'gsp_boot_ga102.bin' = '3df651acb174fd5f5561a1996965b192f50c5d763168446ed0d4ead19d895768'
    'gsp_boot_desc_ga102.bin' = 'cc5a3fc1f4c47f2fe107b1b68f0176d8a448e6dec84b575e5560ccef5262bf15'
    'NVIDIA-LICENSE' = 'c692fb14ad4f499c6aee1b9e144e6905148c420e6225b17cb2937366c1e507ad'
}
foreach ($RtxName in $RtxAssetHashes.Keys) {
    $RtxPath = Join-Path '.\RTX-UNLOCK\ASSETS' $RtxName
    if (-not (Test-Path -LiteralPath $RtxPath -PathType Leaf)) { throw ('파일 누락: ' + $RtxName) }
    if ((Get-FileHash -LiteralPath $RtxPath -Algorithm SHA256).Hash -ne $RtxAssetHashes[$RtxName]) { throw ('해시 불일치: ' + $RtxName) }
}
if (-not (Test-Path -LiteralPath '.\EFI\BOOT\BOOTX64.EFI' -PathType Leaf)) { throw 'EFI 파일이 없습니다.' }
if (-not (Test-Path -LiteralPath '.\RTX-UNLOCK\DEBUG.ON' -PathType Leaf)) { throw '수동 확인용 DEBUG.ON이 없습니다.' }
if ((Get-Item -LiteralPath '.\RTX-UNLOCK\DEBUG.ON').Length -ne 0) { throw 'DEBUG.ON은 빈 파일이어야 합니다.' }
Write-Host '펌웨어 5개와 라이선스 해시 확인 완료. 이것은 언락 성공 판정이 아닙니다.'
```

**잘 됐나요?** 마지막에 **‘펌웨어 5개와 라이선스 해시 확인 완료’**가 나오고 오류가 없으면 USB 복사 단계로 가세요. 이 문구는 파일 검사 완료이지, 언락 성공이라는 뜻은 아닙니다.

파일명에 `ga102`가 있어도 `ga104`로 고치지 마세요. 파일명과 내용은 그대로 사용합니다.

## 5. 빈 FAT32 USB에 폴더 두 개를 복사해주세요

1. 중요한 파일이 없는 **별도 USB**를 준비하세요.
2. 파일 탐색기 → **내 PC**에서 USB를 우클릭 → **속성**을 여세요. **파일 시스템이 FAT32인지** 확인하세요. 다른 형식이거나 어떤 드라이브가 USB인지 헷갈리면 여기서 멈추세요. 이 가이드에는 자동 포맷 명령이 없습니다.
3. 4번에서 사용한 `prepared-...` 폴더를 여세요.
4. 그 안의 **`EFI`와 `RTX-UNLOCK` 두 폴더만** 복사하세요.
5. USB를 열었을 때 처음 보이는 위치에 붙여 넣으세요. 이 위치를 ‘USB의 맨 위’ 또는 ‘루트’라고 합니다. USB 안에 `prepared-...` 폴더를 통째로 넣는 것이 아닙니다.

USB를 열면 아래와 같은 구조여야 합니다. `USB:`는 설명용 표시이며 실제 드라이브 문자는 PC마다 다릅니다.

```text
USB를 열었을 때
├─ EFI
│  └─ BOOT
│     └─ BOOTX64.EFI
└─ RTX-UNLOCK
   ├─ UNLOCK.md
   ├─ DEBUG.ON
   └─ ASSETS
      └─ 펌웨어 파일 5개와 NVIDIA-LICENSE
```

**`DEBUG.ON`은 꼭 남겨두세요.** 준비 도구가 만든 0바이트짜리 빈 파일입니다. 파일 내용이 비어 있는 것이 정상입니다. 이 파일이 없으면 이 배포판은 검사 후 자동 적용될 수 있습니다. 지금 안내는 직접 `U`를 누르기 전까지 기다리는 방식이므로 지우지 마세요.

USB에 같은 이름의 폴더가 이미 있으면 덮어쓰지 말고 다른 빈 USB를 사용하세요. 다른 PC에서 만들어진 `PROFILE.BIN`이나 실행 로그도 섞지 않습니다. **Windows가 설치된 디스크의 EFI 파티션에는 복사하지 마세요.**

## 6. F12로 USB를 한 번만 부팅해주세요

**성능을 비교하고 싶다면 지금, 적용 전 결과부터 기록해주세요.** 평소 사용하는 프로그램이나 게임에서 설정·장면과 결과를 남겨두고, 적용 후에도 같은 조건으로 비교합니다. 비교하지 않을 분은 이 기록을 생략하셔도 됩니다.

이제부터 실제 적용을 시도하는 PC에서 진행합니다. **라이젠 5600X에는 내장 그래픽이 없으므로 모니터는 계속 3070 Ti의 HDMI/DP 단자에 연결**해주세요. 메인보드 영상 단자로 옮기면 안 됩니다.

처음 시험은 그래픽카드에 연결한 모니터 한 대로 진행해주세요. 다만 모니터가 한 대라는 것만으로 내부 화면 검사까지 통과한다고 보장되지는 않습니다.

1. 열려 있는 문서와 작업을 저장하세요.
2. **Shift 키를 누른 상태로 Windows 시작 메뉴 → 전원 → 종료**를 누르세요. PC가 완전히 꺼지면 Shift 키를 놓으세요. 이번에는 ‘다시 시작’을 사용하지 않습니다.
3. 준비한 USB가 꽂힌 상태에서 전원을 켜세요.
4. 화면이 켜지기 시작할 때부터 **F12를 여러 번 눌러** 부팅 선택 메뉴를 여세요.
5. 목록에서 USB 이름이 들어간 **UEFI 항목**을 선택하고 Enter를 누르세요. USB 이름은 제조사마다 다릅니다. 확실한 항목을 찾지 못하면 임의로 다른 디스크를 선택하지 마세요.

**평소 부팅 순서는 바꾸지 않습니다.** 이번 한 번만 USB로 부팅하는 메뉴를 사용합니다. Windows가 그대로 켜졌다면 아직 언락한 것이 아닙니다. F12 시점을 놓쳤을 수 있으므로 Windows 작업을 저장한 뒤 다시 완전히 종료하고 시도할 수 있습니다.

F12는 **전원을 켤 때** 누르는 키입니다. BIOS 설정 화면 안에서 누르는 F12는 다른 기능일 수 있습니다. 보드 공식 매뉴얼은 전원 켤 때 F12로 부팅 메뉴, Del로 BIOS 진입을 안내합니다.

## 7. 검사 화면을 보고, 진행할 때만 U를 눌러주세요

1. USB 프로그램이 PC 상태를 검사합니다. **오류나 거부 메시지가 있으면 멈추고 화면을 남겨주세요.**
2. 검사를 통과하고 **실행 확인 화면이 나온 경우에만**, 적용을 진행하려면 키보드 **`U`를 한 번** 누르세요. 이것이 실제 언락을 시작하는 단계입니다.
3. 진행하지 않으려면 **Esc**를 누르세요. **30초 동안 누르지 않아도 취소**됩니다. 취소 뒤에는 프로그램이 멈추며, Windows로 자동 이동하는 것이 아닙니다. 아래 8번 복귀 방법을 사용하세요.

`U`를 누른 뒤 화면이 꺼질 수 있습니다. 소스의 안내는 Windows로 돌아오기까지 **최대 10분**입니다. 처리 중에는 키를 반복해서 누르거나 같은 작업을 다시 실행하지 마세요. **검은 화면은 성공 표시가 아닙니다.**

이 구현에는 GPU 화면 구성과 Windows 부팅 파일 구조에 대한 조건도 있습니다. 예를 들어 Windows Boot Manager 후보가 여러 개면 거부할 수 있습니다. SSD가 두 개라는 이유만으로 실패하는 것은 아니며, 오류를 없애려고 EFI 파티션을 삭제하면 안 됩니다.

## 8. 취소했거나 Windows로 돌아오지 않으면

오류로 멈췄거나 취소한 경우, 또는 위 안내 시간까지 기다려도 Windows로 돌아오지 않는 경우에 사용하세요.

1. PC 전원을 완전히 끄세요. 화면이 멈춰 정상 종료를 할 수 없으면 본체 전원 버튼을 길게 눌러 꺼주세요.
2. 실험용 **USB를 빼세요**.
3. 전원을 다시 켜세요. 부팅 대상을 골라야 한다면 **Windows Boot Manager**를 선택하세요.
4. 여전히 화면이나 Windows가 정상으로 돌아오지 않으면 반복 적용하지 말고, 마지막으로 보였던 화면과 진행 단계를 전달해주세요.

이 절차는 Windows EFI 파티션을 수정하지 않고 USB로 한 번 실행하도록 구성했습니다. USB를 제거해 평소 부팅 경로로 돌아가는 방법이지만, **모든 펌웨어 문제의 복구를 보장하는 것은 아닙니다.** 모니터 케이블은 계속 3070 Ti에 연결해두세요.

## 9. 진짜 적용됐는지 확인하고 결과를 보내주세요

**Windows가 켜졌다는 것만으로 언락 성공이나 성능 향상을 확정할 수는 없습니다.** 다음 자료를 함께 확인합니다.

1. Windows에서 NVIDIA 그래픽카드가 정상 인식되고 화면이 정상인지 확인하세요.
2. USB의 `RTX-UNLOCK` 폴더에 생긴 `RUNxx`·`PROBExx` 로그를 보관하세요. 적용·정리 완료 여부나 거부 이유를 확인할 때 필요합니다.
3. 성능을 확인하려면 **언락하기 전의 결과를 먼저 남겨두고**, 적용 후 같은 프로그램·설정·장면으로 비교하세요. 비교 기록이 없으면 향상됐다고 단정할 수 없습니다.

게임이 목적이라면 같은 해상도·옵션·장면에서 여러 번 측정해 FPS와 프레임시간을 비교해주세요. 이 실험은 Tensor 연산 제한과 관련된 경로이므로, 해당 연산이 빨라졌다고 모든 게임의 FPS가 같은 비율로 오르는 것은 아닙니다. 재부팅이나 절전 뒤에도 상태가 유지된다고 가정하지 마세요.

**전달할 것:** `inventory.json`, 어느 단계까지 했는지, 오류 문구 또는 화면, 관련 실행 로그. 내용을 확인한 뒤 필요한 것만 보내주세요. **암호화 복구키는 보내지 않습니다.**

## 막혔을 때 자주 보는 문구

| 문구 / 상황 | 이렇게 해주세요 |
|---|---|
| `계속하려면 아무 키나 누르십시오` | 실행기가 창을 열어둔 상태입니다. 결과를 먼저 읽고 복사한 뒤 키를 누르면 창이 닫힙니다. |
| `INCOMPLETE`, `Unknown` | 정보를 확인하지 못했습니다. 성공으로 넘기지 말고 점검 결과를 전달하세요. |
| `Access is denied`, `액세스가 거부되었습니다` | 권한이나 접근 문제입니다. 어느 파일에서 나왔는지 확인하세요. 사양 점검은 관리자 실행을 사용합니다. |
| `SHA256 mismatch`, `해시 불일치` | 기대한 파일과 다릅니다. 검사 코드를 지우거나 건너뛰지 말고 멈추세요. |
| `Unsafe ZIP path`, `Unexpected ZIP entry` | 배포 파일 구성이 예상과 다릅니다. 그대로 멈추세요. |
| `Refusing to overwrite` | 기존 파일을 덮어쓰지 않도록 중단했습니다. 파일을 임의로 섞지 마세요. |
| `DEBUG.ON이 없습니다` | 올바른 준비 폴더가 아니거나 파일이 누락됐습니다. 새로 파일 준비를 진행한 뒤 그 폴더를 사용하세요. |
| F12 목록에 USB의 UEFI 항목이 없음 | USB 형식과 폴더 위치를 다시 확인하세요. BIOS의 CSM 등 다른 설정을 임의로 바꾸지 마세요. |
| Windows에서 실행이 차단됨 | 경고 문구와 차단한 프로그램 이름을 남기고 멈추세요. 보안 기능을 끄는 방법은 이 안내에 포함하지 않습니다. |

## 확인한 내용과 아직 확인하지 못한 내용

**확인한 것:** 사용자 제공 견적 이미지, 고정 배포 파일 다운로드·해시·ZIP 구성, 준비 도구와 점검 코드, 수동 확인용 `DEBUG.ON` 생성. 준비 도구의 검증 기록과 테스트 코드는 ZIP에 포함했습니다.

**확인하지 못한 것:** 대상 PC의 현재 BIOS·Windows·드라이버·보안 설정, 펌웨어 EXE 실제 실행, USB 실제 부팅, ASUS TUF 3070 Ti에서의 언락 성공·안정성·성능 향상. 준비 파일의 정상 다운로드가 실제 언락 성공을 의미하지 않습니다.

사진에 나온 사양은 Ryzen 5 5600X / GIGABYTE B550M AORUS ELITE / ASUS TUF Gaming RTX 3070 Ti O8G OC D6X 8GB / DDR4-3200 32GB / 마이크로닉스 Classic II 750W GOLD입니다. 구매 구성 자료이므로 현재 장착 상태까지 확인된 것은 아닙니다.

## 출처와 버전 — 필요할 때만 읽으세요

- 기준 배포: [craftingmod/rtx30-unlock v0.1.0](https://github.com/craftingmod/rtx30-unlock/releases/tag/v0.1.0), 고정 커밋 `5c076dc4ee7fa369639669fa591ac74d8f6dfcd8`.
- [제작자 설명](https://github.com/craftingmod/rtx30-unlock/blob/5c076dc4ee7fa369639669fa591ac74d8f6dfcd8/README.md): 공개한 실기 확인 장비는 Colorful RTX 3090 Ti입니다. 이 안내의 ASUS 3070 Ti 조합 성공 사례를 뜻하지 않습니다.
- [실제 GPU에서 프로필을 만드는 코드](https://github.com/craftingmod/rtx30-unlock/blob/5c076dc4ee7fa369639669fa591ac74d8f6dfcd8/src/unlock/profile_probe.c): 3070 Ti의 GA104는 코드상 대상이며, 예전 가이드의 MSI 카드·ASUS B660M 보드로 고정된 방식은 아닙니다.
- [펌웨어 생성 도구](https://github.com/craftingmod/rtx30-unlock/blob/5c076dc4ee7fa369639669fa591ac74d8f6dfcd8/tools/firmware/exe.ts), [파일 해시 목록](https://github.com/craftingmod/rtx30-unlock/blob/5c076dc4ee7fa369639669fa591ac74d8f6dfcd8/tools/firmware/artifacts-610.43.03.json), [U 확인·취소 동작](https://github.com/craftingmod/rtx30-unlock/blob/5c076dc4ee7fa369639669fa591ac74d8f6dfcd8/src/gop/app.c).
- [GIGABYTE 공식 매뉴얼 21쪽](https://download.gigabyte.com/FileList/Manual/mb_manual_b550m-aorus-elite_e_1201.pdf#page=21): 전원 켤 때 F12 부팅 메뉴. [AMD 5600X 공식 사양](https://www.amd.com/en/products/processors/desktops/ryzen/5000-series/amd-ryzen-5-5600x.html): 별도 그래픽카드 필요.
- 작성·확인일: 2026-10-26. 검색어: RTX3070Ti, ASUS TUF, 5600X, B550M AORUS ELITE, Windows, GA104, 자동 프로필, 한국어, 초보자, 복붙, USB, DEBUG.ON.

