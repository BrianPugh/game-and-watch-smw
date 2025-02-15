# Port of reverse engineered Super Mario World for the Game and Watch

All credits for reverse engineering goes to https://github.com/snesrev/smw

# Build instructions

- Clone repository with submodules
```sh
git clone --recurse-submodules https://github.com/marian-m12l/game-and-watch-smw.git
```

- Install python requirements using pip
```sh
pip3 install -r requirements.txt
```

- Place your US ROM file named `smw.sfc` in `smw/assets/`.

- Compile and flash (e.g. on internal flash bank 2, leaving 1MB (out of 16) for stock firmware at the beginning of extflash)
```sh
make INTFLASH_BANK=2 EXTFLASH_SIZE_MB=15 EXTFLASH_OFFSET=1048576 ADAPTER=jlink OPENOCD=/path/to/patched/openocd-git/bin/openocd GNW_TARGET=mario flash
```

# Backing up and restoring saves

```sh
ADAPTER=jlink OPENOCD=/path/to/patched/openocd-git/bin/openocd ./scripts/saves_backup.sh build/gw_smw.elf 
ADAPTER=jlink OPENOCD=/path/to/patched/openocd-git/bin/openocd ./scripts/saves_erase.sh build/gw_smw.elf 
ADAPTER=jlink OPENOCD=/path/to/patched/openocd-git/bin/openocd ./scripts/saves_restore.sh build/gw_smw.elf 
```
