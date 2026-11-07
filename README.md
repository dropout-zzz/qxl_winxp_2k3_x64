this compiles QXL display driver for x64 edition of Windows Server 2003 and Windows XP

it improves guest display performance in virt-manager

(it's said that winserver 2k3 shares code base and kernel with xp x64, but i only tested the xp.)

## pre-compiled driver download

see [GitHub release](https://github.com/dropout-zzz/qxl_winxp_2k3_x64/releases)

## build environment

as a reference, i used a Quickemu VM running x64 version of Windows 11 25H2 build 26200.8037

but i guess instructions also works for Windows 10 and etc.

## needed stuffs

- [WDK 7.1.0](https://www.microsoft.com/en-us/download/details.aspx?id=11800)
- [spice-protocol 0.12.10](https://launchpad.net/ubuntu/+archive/primary/+sourcefiles/spice-protocol/0.12.10-1/spice-protocol_0.12.10.orig.tar.bz2)
- [qxl e3371bd2](https://gitlab.freedesktop.org/spice/win32/qxl/-/archive/e3371bd2d26473dd42798ae392e0c4cdc6a63a06/qxl-e3371bd2d26473dd42798ae392e0c4cdc6a63a06.zip)

thanks [this documentation](https://virtio-win.github.io/Development/Building-the-drivers-using-Visual-Studio-2017#3-install-wdk-for-windows-7-required-to-build-drivers-for-legacy-os-ie-xp-wnet-vista) for linking a suitable WDK

## instructions

## appendix

### installing dotnet 3.5

this installs dotnet 3.5 offline

> [!NOTE]
> if you have Internet and Windows Update works for you, you can just enable dotnet 3.5 in Windows Features and skip this section.

credits: thanks to [this post](https://shrimpmaru.hatenablog.com/entry/windows/enable_dotnet_framework_3-5/)

do not follow steps in this section if you have win11 26H1 and higher

instead you want to use [this installer](https://learn.microsoft.com/en-us/dotnet/framework/install/dotnet-35-windows-11#windows-11-26h1-build-28000-and-later)

unfortunately, the installer refuses to run on older systems

#### grab installation files

search your exact Windows version on [UUP dump](https://uupdump.net/)

this gives a script to download UUP set into "UUPs" folder

find an ESD file which name starts with edition of your Windows, follow by language code. in my case, it's "professional_ja-jp.esd"

(you may be able to reduce download size by downloading only the ESD file by examining the aria2 script.)

run `wiminfo` to find "Index" that corresponds to "Setup"

run `wimdir` with "Index", look for a ".cab" file that says "NetFx3-OnDemand" in "/sources/sxs"

extract the ".cab" file with `wimextract` using "Index" and path you found

> [!NOTE]
> you can get these `wim*` commands from [wimlib](https://wimlib.net)

#### perform installation

put the ".cab" file in an empty folder, say it's in "C:\MyFolder"

open a command prompt with admin rights, run:

```
dism /online /enable-feature /featurename:NetFx3 /all /limitaccess /source:C:\MyFolder
```

