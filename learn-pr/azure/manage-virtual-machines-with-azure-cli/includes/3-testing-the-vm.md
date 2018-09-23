가상 머신을 만들면 인터넷을 통해 연결할 수 있는 공용 IP 주소와 Azure 데이터 센터 내에서 사용되는 개인 IP 주소가 할당됩니다. `create` 명령에서 반환하는 JSON 블록의 해당 값을 모두 가져옵니다.

```json
{
   ...
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
   ...
}
```

## <a name="connecting-to-the-vm-with-ssh"></a>SSH로 VM에 연결

공용 IP 주소로 Secure Shell(`ssh`) 도구를 사용하여 Linux VM이 시작되어 실행 중인지 신속하게 테스트할 수 있습니다. 관리자 이름을 `aldis`로 설정했으므로 이 이름을 지정해야 합니다. 실행 중인 _your_ 인스턴스에서 공용 IP 주소를 사용해야 합니다.

```azurecli
ssh <public-ip-address> -l aldis
```

> [!NOTE]
> VM 생성의 일부로 SSH 키 쌍을 생성했으므로 암호가 필요하지 않습니다. 처음으로 VM에 셸로 연결하면 호스트의 신뢰성을 묻는 메시지가 표시됩니다. 
> 
> 이는 호스트 이름 대신 직접 IP 주소에 연결하기 때문입니다. “예”를 선택하면 해당 IP가 연결에 대한 유효한 호스트로 저장되고 연결을 계속 진행할 수 있습니다.

```output
The authenticity of host '40.83.165.85 (40.83.165.85)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '40.83.165.85' (RSA) to the list of known hosts.
```

그런 다음, Linux 명령을 입력할 수 있는 원격 셸이 표시됩니다.

```output
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

몇 가지 명령을 연습해 보고 완료되면 셸에서 로그아웃합니다(셸에서 `logout` 또는 `exit` 입력).