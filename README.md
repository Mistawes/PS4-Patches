# PS4-Patches
Gathering some of the snippets I've seen posted around the interwebs. I haven't tested anything yet, nor is it my work. Will try to keep credits where possible. Presume they're for 4.05 unless otherwise noted.

```
// flatz 4.55
// Disable RSA signature check for PFS.
kernel_text_base + 0x69F4E0: 55 48 89 E5 -> 31 C0 C3 90
// Enable debug RIFs.
kernel_text_base + 0x62D30D: E8 0E 04 00 00 EB 38 3D -> B8 01 00 00 00 EB 38 3D
```

```
// 2much4u @2much4ux
Kernel patch to disable process ASLR on 4.05
*(uint16_t*)(kernelBase + 0x2862D6) = 0x9090;
```
```
// CrazyVoid's patches to allow webkit (4.05)
#define KERNEL_REGMGR_SETINT 0x4CEAB0
uint64_t *(sceRegMgrSetInt)(uint32_t regId, int value) = NULL;
sceRegMgrSetInt = (void *)&ptrKernel[KERNEL_REGMGR_SETINT];
sceRegMgrSetInt(0x3C040000, 0);
```

```
// Correct patches to enable mmap of all SELF (discard previous patches):
*(uint8_t*)(kernel_base + 0x31EE40) = 0x90;
*(uint8_t*)(kernel_base + 0x31EE41) = 0xE9;
*(uint8_t*)(kernel_base + 0x31EF98) = 0x90;
*(uint8_t*)(kernel_base + 0x31EF99) = 0x90;
```

```
// <WildCard - KernelDumper>
// uart enabler
*(char *)(kernel_base + 0x186b0a0) = 0; // set the console disable console output bool
```

```
// specters debug settings patchs
*(char *)(kernel_base + 0x2001516) |= 0x14;
*(char *)(kernel_base + 0x2001539) |= 1;
*(char *)(kernel_base + 0x2001539) |= 2;
*(char *)(kernel_base + 0x200153A) |= 1;
*(char *)(kernel_base + 0x2001558) |= 1;	
```
```
// Disable write protection
uint64_t cr0 = readCr0();
writeCr0(cr0 & ~X86_CR0_WP);
```
```
// debug menu full patches thanks to sealab
*(uint32_t *)(kernel_base + 0x4CECB7) = 0;
*(uint32_t *)(kernel_base + 0x4CFB9B) = 0;
```
```
// Target ID Patches :)
*(uint16_t *)(kernel_base + 0x1FE59E4) = 0x8101;
*(uint16_t *)(kernel_base + 0X1FE5A2C) = 0x8101;
*(uint16_t *)(kernel_base + 0x200151C) = 0x8101;
// </WildCard - KernelDumper>
```

## 4.55

```
// 2much4u
// Full debug settings offsets for 4.55

kernelBase[0x1B6D086] |= 0x14;
kernelBase[0x1B6D0A9] |= 0x3;
kernelBase[0x1B6D0AA] |= 0x1;
kernelBase[0x1B6D0C8] |= 0x1;

// Disable write protection
*(uint32_t*)&kernelBase[0x4D70F7] = 0;
*(uint32_t*)&kernelBase[0x4D7F81] = 0;
```
