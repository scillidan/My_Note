## VirtualBox

File → Preferences → Input → Virtual Machine → Host Key Combination → None or Other

↪ [Virtual Box: How to Increase Disk Size (Windows)](https://www.youtube.com/watch?v=pVjDFBdBQ7I)

Target Machine → Machine → Settings → General → Advanced → Shared Clipboard → Bidirectional → Start Machine

Target Machine → Machine → Settings → USB → Enable USB Controller → USB 3.0 (xHCI) Controller (On) → Add → Generic USB3.0 Card Reader → OK

Target Machine → Machine → Settings → Shared Folders → Add:

```
Folder Path `D:\mnt`
Folder Name `mnt`
Auto-mount (On)
Make Permanent (On)
```

Devices → sf_mnt → 右键 → Thunar Root → 目标文件 → 右键 → Extract