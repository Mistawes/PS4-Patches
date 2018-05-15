# PS4-Patches
Gathering some of the snippets I've seen posted around the interwebs. This is not my work, but I'll try to keep credits where possible. 

Feel free to submit PRs!


## 4.05

```
// Kernel base
void* kernel_base = &((uint8_t*)__readmsr(0xC0000082))[-0x30EB30];
uint8_t* kernel_ptr = (uint8_t*)kernel_base;
void** got_prison0 =   (void**)&kernel_ptr[0xF26010];
void** got_rootvnode = (void**)&kernel_ptr[0x206D250];
```
```
// 2much4u @2much4ux
Kernel patch to disable process ASLR on 4.05
*(uint16_t*)(kernelBase + 0x2862D6) = 0x9090;
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
```
// Correct patches to enable mmap of all SELF
*(uint8_t*)(kernel_base + 0x31EE40) = 0x90;
*(uint8_t*)(kernel_base + 0x31EE41) = 0xE9;
*(uint8_t*)(kernel_base + 0x31EF98) = 0x90;
*(uint8_t*)(kernel_base + 0x31EF99) = 0x90;
```


## 4.55
```
// flatz 4.55
// Disable RSA signature check for PFS.
kernel_text_base + 0x69F4E0: 55 48 89 E5 -> 31 C0 C3 90
// Enable debug RIFs.
kernel_text_base + 0x62D30D: E8 0E 04 00 00 EB 38 3D -> B8 01 00 00 00 EB 38 3D
```
```
// Joonie86
// TargetID patches for 4.55 (Spoofs to Devkit)
*(uint16_t *)(kernel_base + 0x1AF82C4) = 0x8101;
*(uint16_t *)(kernel_base + 0X1AF85A4) = 0x8101;
*(uint16_t *)(kernel_base + 0x1B6D08C) = 0x8101;
```
```
// 2much4u
// Full debug settings offsets for 4.55
*(char *)(kernel_base + 0x1B6D086) |= 0x14;
*(char *)(kernel_base + 0x1B6D0A9) |= 3;
*(char *)(kernel_base + 0x1B6D0AA) |= 1;
*(char *)(kernel_base + 0x1B6D0C8) |= 1;	

// debug menu full patches
*(uint32_t *)(kernel_base + 0x4D70F7) = 0;
*(uint32_t *)(kernel_base + 0x4D7F81) = 0;

// Xvortex
// enable mmap of all SELF
*(uint8_t*)(kernel_base + 0x143BF2) = 0x90;
*(uint8_t*)(kernel_base + 0x143BF3) = 0xE9;
*(uint8_t*)(kernel_base + 0x143E0E) = 0x90;
*(uint8_t*)(kernel_base + 0x143E0F) = 0x90;

```
```
//Vultra UART Enabler 4.55
*(char *)(kernel_base + 0x1997BC8) = 0;
```
