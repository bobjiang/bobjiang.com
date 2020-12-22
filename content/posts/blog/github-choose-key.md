---
Title: Github指定本地私钥访问仓库
Date: 2020-12-21
URL: /github-choose-key/
tags: [github, git, private key]
---

一共有三个关键步骤：

1. 生成新的私钥
2. 上传公钥到github
3. 修改本地ssh配置

Mac pro迁移后，本地的 github 私钥忘记是哪个，重新生成一个新的私钥放在一个新目录。（怕覆盖了原来的私钥，其他应用受影响）

# 1. 生成新的私钥

```
ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/<default>/.ssh/id_rsa): <your new path>/id_rsa
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in <your new path>/id_rsa.
Your public key has been saved in <your new path>/id_rsa.pub.
The key fingerprint is:
... ...
```

注意指定一个新的目录 `<your new path>`

# 2. 上传公钥到github

打开公钥内容，如下：

```
cat <your new path>/id_rsa.pub

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCsYg2PbSzt+5Km0fX89xHq2i4iDAignMjLytV409jE5BK+66eTKeBgcsRlVVFUzYCrxrqNtFiXpuBcDARjXfUUTxIhazpv1k/reh34jXC0Mz+34PDaGdds/x+VGoG9W7u71MfBEz79uKag5IxrqUYZ8kH8ooVc3OrVF3kyRLb+QCdTbgefoTMxvilU+yocrYCv6lOD0Pvy47d63kPufS529sy3sF5U3Cx5O2Jutzxsw8k6a9kJ/UQz9iOkqXUvxDJH6abdBejx83nVEESPVQV6EQN0ix9wpy5+zzL7YbCuBq060CJUPnoiF7f+0Qt9B2mZSJfdXukWCIprwNFeWoMwDe7/0q7tagqgYleC1QOB1V7V0xeUUWLH0jVWtKHZs7BER8b49PQ8FgIZWWeuGAS2I8Gb6DTTL+bEun2OI3CcgLoxHf0onv0tyWPmP3kWELKTlyD5QpcetsTG42M9OIBPpQpvbGO/gcuCRjsGC+WF8F0Jwt/PMcAoApc+AUoAcyk= bobjiang1@BobJiang
```

	a. 登录 github，并访问链接修改 github SSH keys https://github.com/settings/keys
	b. 点击 New SSH Keys
	c. Title输入新的SSH Key的名字（随意起名）， Key 输入上面 id_rsa.pub 内容
	d. 点击 Add SSH Key 保存

# 3. 修改本地ssh配置

修改本地 ssh 配置，访问github的时候采用新的 ssh key

```
vim ~/.ssh/config
# config文件增加以下内容

Host github.com
    HostName github.com
    User bobjiang
    IdentityFile <your new path>/id_rsa
    IdentitiesOnly yes

```

以上三步设置好了即可，就可以本地用新的私钥访问 github 仓库啦。


