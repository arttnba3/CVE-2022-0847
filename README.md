# CVE-2022-0847

my personal poc and exploit of CVE-2022-0847(dirty pipe)

## Usage

### POC: write files arbitrarily
Just a simply POC of this CVE, compile the file poc.c as follow:

```shell
$ gcc poc.c -o poc -static
```

You shall run it as follow:

```shell
./poc target_file offset_in_file data
```

You shall make sure the destination file is at least readable. 

Result tested on Linux kernel 5.13.19:

![image.png](https://s2.loli.net/2022/03/12/vOGZw2Qt9VRsYDd.png)

### EXPLOIT: ROOT PRIVILEGE
I choose to gain a ROT privilege by overwriting SUID application to provide a ROOT SHELL
Just compile the file `exploit_suid.c` and run it as follow:

```shell
$ gcc exploit_suid.c -o exp -static
$ ./exp target_file
```

For test I chose the `/bin/passwd` as the target SUID file, result tested on Ubuntu 21.10 (kernel 5.13.0) is as follow:

![image.png](https://s2.loli.net/2022/03/12/P2QdeIqbASfuxHR.png)

## Analyzation of the CVE-2022-0847
You can visit [my blog](https://arttnba3.cn/2022/03/12/CVE-0X06-CVE-2022-0847/) for more information about this CVE