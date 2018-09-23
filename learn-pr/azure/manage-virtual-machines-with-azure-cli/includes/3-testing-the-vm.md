<span data-ttu-id="908e5-101">가상 머신을 만들면 인터넷을 통해 연결할 수 있는 공용 IP 주소와 Azure 데이터 센터 내에서 사용되는 개인 IP 주소가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="908e5-101">When you create a virtual machine, it gets assigned a public IP address that is reachable over the Internet, and a private IP address used within the Azure data center.</span></span> <span data-ttu-id="908e5-102">`create` 명령에서 반환하는 JSON 블록의 해당 값을 모두 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="908e5-102">You get both of those values in the returning JSON block from the `create` command:</span></span>

```json
{
   ...
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
   ...
}
```

## <a name="connecting-to-the-vm-with-ssh"></a><span data-ttu-id="908e5-103">SSH로 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="908e5-103">Connecting to the VM with SSH</span></span>

<span data-ttu-id="908e5-104">공용 IP 주소로 Secure Shell(`ssh`) 도구를 사용하여 Linux VM이 시작되어 실행 중인지 신속하게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="908e5-104">With the public IP address we can quickly test that the Linux VM is up and running using the Secure Shell (`ssh`) tool.</span></span> <span data-ttu-id="908e5-105">관리자 이름을 `aldis`로 설정했으므로 이 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="908e5-105">Remember that we set our admin name to `aldis`, so we have to specify that.</span></span> <span data-ttu-id="908e5-106">실행 중인 _your_ 인스턴스에서 공용 IP 주소를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="908e5-106">Make sure to use the public IP address from _your_ running instance.</span></span>

```azurecli
ssh <public-ip-address> -l aldis
```

> [!NOTE]
> <span data-ttu-id="908e5-107">VM 생성의 일부로 SSH 키 쌍을 생성했으므로 암호가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="908e5-107">We don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="908e5-108">처음으로 VM에 셸로 연결하면 호스트의 신뢰성을 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="908e5-108">The first time you shell into the VM, it will give you a prompt about the authenticity of the host.</span></span> 
> 
> <span data-ttu-id="908e5-109">이는 호스트 이름 대신 직접 IP 주소에 연결하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="908e5-109">This is because we are hitting an IP address directly instead of a host name.</span></span> <span data-ttu-id="908e5-110">“예”를 선택하면 해당 IP가 연결에 대한 유효한 호스트로 저장되고 연결을 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="908e5-110">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

```output
The authenticity of host '40.83.165.85 (40.83.165.85)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '40.83.165.85' (RSA) to the list of known hosts.
```

<span data-ttu-id="908e5-111">그런 다음, Linux 명령을 입력할 수 있는 원격 셸이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="908e5-111">Then you'll be presented with a remote shell where you can enter Linux commands.</span></span>

```output
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

<span data-ttu-id="908e5-112">몇 가지 명령을 연습해 보고 완료되면 셸에서 로그아웃합니다(셸에서 `logout` 또는 `exit` 입력).</span><span class="sxs-lookup"><span data-stu-id="908e5-112">Try a few commands as practice and when you are finished, sign out of the shell (type `logout` or `exit` in the shell).</span></span>