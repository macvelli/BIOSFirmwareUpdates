#
# README.txt - Instructions for updating the LSI SAS9211-8i HBA card
#
# Copyright (C) 2019 Edward Smith <edwardsmith@devopsbroker.org>
#
# This program is free software: you can redistribute it and/or modify it under
# the terms of the GNU General Public License as published by the Free Software
# Foundation, either version 3 of the License, or (at your option) any later
# version.
#
# This program is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
# FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more
# details.
#
# You should have received a copy of the GNU General Public License along with
# this program.  If not, see <http://www.gnu.org/licenses/>.
#
# -----------------------------------------------------------------------------
# Authored on Ubuntu 18.04.2 LTS running kernel.osrelease = 4.18.0-20
#
# -----------------------------------------------------------------------------
#

# ----------------
# File Information
# ¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯

efi/boot/bootx64.efi
  o Sourced from https://github.com/tianocore/edk2/blob/UDK2014/EdkShellBinPkg/FullShell/X64/Shell_Full.efi
    and then renamed to bootx64.efi

2118ir.bin
2118it.bin
  o Sourced from 9211-8i_Package_P20_IR_IT_FW_BIOS_for_MSDOS_Windows.zip file
    found on https://www.broadcom.com/support/ website

sas2flash.efi
SAS2Flash Reference Guide.pdf
  o Sourced from Installer_P20_for_UEFI.zip file found on https://www.broadcom.com/support/
    website

x64sas2.rom
  o Sourced from UEFI_BSD_P20.zip file found on https://www.broadcom.com/support/
    website

# ------------
# Instructions
# ¯¯¯¯¯¯¯¯¯¯¯¯

1. Insert the LSI SAS9211-8i in an available PCI Express 2.0 x8 slot

2. Format a USB thumb drive with a FAT32 partition

3. Place all files extracted from this archive onto the USB thumb drive

4. Restart the PC and select the USB thumb drive from the boot menu

5. At the Shell> prompt, type 'map -b' to find which file system is the USB
   thumb drive (e.g. fs1)

6. Type 'fs1:' (include the :) to switch to the USB thumb drive and then type
   'ls' to view the filesystem contents

7. To erase the existing firmware and BIOS, type:

   sas2flash.efi -o -e 6

8. Then load the new firmware and BIOS by typing:

   NOTE: Choose the IR firmware for controller-based RAID management and the IT
         firmware for RAID passthrough

   sas2flash.efi -o -f 2118it.bin -b x64sas2.rom

9. Reboot for changes to take effect
