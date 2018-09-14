<span data-ttu-id="8b530-101">가상 머신을 만들 때는 인터넷을 통해 연결할 수 있는 공용 IP 주소와 Azure 데이터 센터 내에서 사용되는 개인 IP 주소가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b530-101">When you create a virtual machine, it gets assigned a public IP address that is reachable over the Internet, and a private IP address used within the Azure data center.</span></span> <span data-ttu-id="8b530-102">`ssh` 도구를 사용하여 Linux VM이 시작되어 실행 중인지 신속하게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b530-102">We can quickly test that the Linux VM is up and running using the `ssh` tool.</span></span> <span data-ttu-id="8b530-103">관리자 이름을 `aldis`로 설정했으므로 이 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b530-103">Remember that we set our admin name to `aldis`, so we have to specify that.</span></span>

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> <span data-ttu-id="8b530-104">VM을 만드는 동안 SSH 키 쌍을 생성했으므로 암호가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b530-104">We don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="8b530-105">처음으로 VM에 셸로 연결하면 호스트의 신뢰성을 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b530-105">The first time you shell into the VM, it will give you a prompt about the authenticity of the host.</span></span> 
> 
> <span data-ttu-id="8b530-106">이는 호스트 이름 대신 직접 IP 주소에 연결하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="8b530-106">This is because we are hitting an IP address directly instead of a host name.</span></span> <span data-ttu-id="8b530-107">“예”를 선택하면 해당 IP가 연결에 대한 유효한 호스트로 저장되고 연결을 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b530-107">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

```output
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

<span data-ttu-id="8b530-108">그런 다음, Linux 명령을 입력할 수 있는 원격 셸이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b530-108">Then you'll be presented with a remote shell where you can enter Linux commands.</span></span>

```output
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

<span data-ttu-id="8b530-109">몇 가지 명령을 연습해 보고 완료되면 계정에서 로그아웃합니다(셸에서 `logout` 또는 `exit` 입력).</span><span class="sxs-lookup"><span data-stu-id="8b530-109">Try a few commands as practice and when you are finished, sign out of your account (type `logout` or `exit` in the shell).</span></span>