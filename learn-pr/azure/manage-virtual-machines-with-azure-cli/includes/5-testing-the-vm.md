가상 머신을 만들 때는 인터넷을 통해 연결할 수 있는 공용 IP 주소와 Azure 데이터 센터 내에서 사용되는 개인 IP 주소가 할당됩니다. `ssh` 도구를 사용하여 Linux VM이 시작되어 실행 중인지 신속하게 테스트할 수 있습니다. 관리자 이름을 `aldis`로 설정했으므로 이 이름을 지정해야 합니다.

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> VM을 만드는 동안 SSH 키 쌍을 생성했으므로 암호가 필요하지 않습니다. 처음으로 VM에 셸로 연결하면 호스트의 신뢰성을 묻는 메시지가 표시됩니다. 
> 
> 이는 호스트 이름 대신 직접 IP 주소에 연결하기 때문입니다. “예”를 선택하면 해당 IP가 연결에 대한 유효한 호스트로 저장되고 연결을 계속 진행할 수 있습니다.

```output
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
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

몇 가지 명령을 연습해 보고 완료되면 계정에서 로그아웃합니다(셸에서 `logout` 또는 `exit` 입력).