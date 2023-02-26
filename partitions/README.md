1. Dump your sotck partitions
   - Install EDL requirements, see [tools/edl/requirements.txt](./tools/edl/requirements.txt)
   - Boot your UFI001C to 9008 mode
     - Hold the only button on the board and plug it to USB port
     - `05c6:9008 Qualcomm, Inc. Gobi Wireless Modem (QDL mode)` should appear in the output of `lsusb`
   - Dump partitions to `stock_partitions`
     - `./tools/edl/edl rl stock_partitions --skip=userdata --genxml`
2. Get Qualcomm partitions
   - Download the `dragonboard-410c-bootloader-emmc-linux-*.zip` from <http://releases.linaro.org/96boards/dragonboard410c/linaro/rescue/latest>
   - Extract `hyp.mbn` `rpm.mbn` `sbc_1.0_8016.bin` `sbl1.mbn` `tz.mbn` to `qcom_partitions`
3. Create patition table
   - `sudo ./tools/db-boot-tools/mksdcard -g -o emmc.img -p partitions.txt`
   - `sgdisk -bgpt.bin emmc.img`
   - `./tools/db-boot-tools/mkgpt -i gpt.bin -o gpt_both0.bin`
4. Build lk1st
   - Clone <https://github.com/msm8916-mainline/lk2nd>
   - `make TOOLCHAIN_PREFIX=arm-none-eabi- LK1ST_DTB=msm8916-512mb-mtp lk1st-msm8916 -j$(nproc)`
5. Sign the bootloader
   - `./tools/qtestsign/qtestsign.py aboot ./lk2nd/build-lk1st-msm8916/emmc_appsboot.mbn`
6. Format
   - Reboot UFI001C to fastboot (you can also use edl to flash, but fastboot is more stable)
   - Run [`fastboot_init_partitions.sh`](./fastboot_init_partitions.sh)
7. Done. Your UFI001C is ready to install the pmOS

# Notes

`partition.txt` is from `db-boot-tools/dragonboard410c/linux/partition.txt` but:
- Deleted boot partition: which is useless since pmOS is booted from rootfs
- Added modem partition: the modem firmware of UFI devices is device-related
