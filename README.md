## Emulator

### Emulator installation

On Debian and derivatives, install the `vice` package:

```
apt install vice
```

Then, install the ROMs, which are not included in the Debian package (they are
however included in the `vice` package on Arch Linux, for example):

```
wget https://downloads.sourceforge.net/project/vice-emu/releases/vice-3.6.1.tar.gz
mkdir -p ~/.local/share/vice
tar xf vice-3.6.1.tar.gz -C ~/.local/share/vice/ vice-3.6.1/data --strip-components=2
```

### Compiling the software into an image

```
make package
```

### Running the emulator

```
make vice
```

Then, type `run`, followed by enter.

## Reading files from the floppy (disk image)

To view the contents of a file within a disk image (e.g. the logfile), use:

```
c1541 -attach kasse.d64 -read "log-2" >(petcat -nh) >&-
```

## .git/config

To make git display contents of https://en.wikipedia.org/wiki/PETSCII files:

```
[diff "petscii"]
	textconv = /bin/sh -c 'petcat -nc -nh "$0"'
[diff "items"]
	textconv = /bin/sh -c "petcat -nc -nh \"$0\" | hexdump -e '8/1 \"%_p\"\"\n\"'"
[diff "credits"]
	textconv = /bin/sh -c "petcat -nc -nh \"$0\" | hexdump -e '8/1 \"%_p\"\"\n\"'"
```
