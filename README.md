# small-gbas
Some small fuzz-interesting GBAs along with compile tools

## Compiling GBAs
To compile GBAs simply use this docker:

```
docker run -it -v $PWD:/host devkitpro/devkitarm 
```

Make sure to run this in the root of where your source files are.

You can find a simple Makefile in:
```
/opt/devkitpro/examples/gba/template
```

There you can modify the file in `source/template.c` and run `make` to get a gba
file (it will be stripped from the ELF in the same directory).

## Interesting GBAs
I've included some tiny gbas for others to use for fuzzing seeds in here.

- fuzz.gba: a minimal screen init gba
- fuzz_no_loop.gba: same as fuzz.gba, but with no ending loop. Stops instantly.
- small.gba: my first attempt at fuzz.gba
- template.gba: a naive huge gba (DO NOT USE)
- fuzzer_golfed.gba: a gba created by the fuzzer smaller than mine

And a source file of `main.c` to start you off with some source for `small.gba`.

## Starting code
Based on this
[blog](https://www.reinterpretcast.com/writing-a-game-boy-advance-game):
```c
int main(void)
{
    volatile unsigned char *ioram = (unsigned char *)0x04000000;
    ioram[0] = 0x03; // Use video mode 3 (in BG2, a 16bpp bitmap in VRAM)
    ioram[1] = 0x04; // Enable BG2 (BG0 = 1, BG1 = 2, BG2 = 4, ...)
    volatile unsigned short *vram = (unsigned short *)0x06000000;
    vram[80*240 + 115] = 0x001F; // X = 115, Y = 80, C = 000000000011111 = R
    while(1);
    return 0;
}
```
