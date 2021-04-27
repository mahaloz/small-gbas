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

