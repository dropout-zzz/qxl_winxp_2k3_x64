this compiles QXL driver for x64 edition of Windows Server 2003 and Windows XP

## pre-compiled driver download

see GitHub release

## build environment

i used a Quickemu VM running x64 version of Windows 11 25H2 build 26200.8037

## needed stuffs

- [WDK 7.1.0](https://www.microsoft.com/en-us/download/details.aspx?id=11800)
- [spice-protocol 0.12.10](https://launchpad.net/ubuntu/+archive/primary/+sourcefiles/spice-protocol/0.12.10-1/spice-protocol_0.12.10.orig.tar.bz2)
- [qxl e3371bd2](https://gitlab.freedesktop.org/spice/win32/qxl/-/archive/e3371bd2d26473dd42798ae392e0c4cdc6a63a06/qxl-e3371bd2d26473dd42798ae392e0c4cdc6a63a06.zip)

## instructions

### install dotnet 3.5 offline

[credit](https://shrimpmaru.hatenablog.com/entry/windows/enable_dotnet_framework_3-5/)

#### grab installation files

search exact Windows version on [UUP dump](https://uupdump.net/)

this gives a script to download UUP set into `UUPs` folder

find an ESD file which name starts with edition of your Windows version, follow by language code

run `wiminfo` to find `Index` correspond to Setup

run `wimdir` with `Index`, look for a `.cab` file that says `NetFx3-OnDemand` in `/sources/sxs` 

extract the `.cab` file with `winextract` using `Index` and path you found

#### perform installation

put the `.cab` file in an empty folder, say it's in `C:\MyFolder`

open a command prompt with admin rights, run:

```
dism /online /enable-feature /featurename:NetFx3 /all /limitaccess /source:C:\MyFolder
```

