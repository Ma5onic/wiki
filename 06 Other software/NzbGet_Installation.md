# NzbGet installtion

Procedure is
1. Get installer
2. Run installer
3. Start NzbGet
4. Enjoy

## Get installer
Using the automated genric linux installtion guide from [NzbGet](https://github.com/nzbget/nzbget/wiki/Installation-on-Linux) run following;

```bash
wget -O - http://nzbget.net/info/nzbget-version-linux.json | \
   sed -n "s/^.*stable-download.*: \"\(.*\)\".*/\1/p" | \
   wget --no-check-certificate -i - -O nzbget-latest-bin-linux.run
```
Note, this will install to ~/nzbget.

## Run installer
```bash
./sh nzbget-latest-bin-linux.run
```
## Start NzbGet
```bash
./nzbget -D
```

## Enjoy
![NzbGet logo](https://avatars1.githubusercontent.com/u/3368377?v=3&s=200)
@ip:port

Find IP of your slot by going to [IRC chat](http://webchat.freenode.net/?randomnick=0&channels=%23%23feral&prompt=1&uio=MTY9dHJ1ZSYyPXRydWUmOT10cnVlJjEwPXRydWU52)
and type ```*ip arges``` for ip of Arges.
## Refs
* [Generic Software installation from this FAQ](https://github.com/feralhosting/faqs-cached/blob/master/08%20Software/01%20Generic%20Software%20Installation%20Guide.md)
* [NzbGet auto linux installaion guide](https://github.com/nzbget/nzbget/wiki/Installation-on-Linux)
