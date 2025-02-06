---
layout: raw_code
lang: en
title: Removing ASLR & Authenticode from a given module
author: Otávio
author_url:
author_nickname: estr3llas
tags: [windows, cpp]
code: |
    bool TamperDllCharacteristics(DWORD_PTR moduleBase) {
	// Retrieve the module's NT header
        const auto dos = reinterpret_cast<PIMAGE_DOS_HEADER>(moduleBase);
        const auto nt = reinterpret_cast<PIMAGE_NT_HEADERS>(moduleBase + dos->e_lfanew);

	// Access the DllCharacteristics and toggle the ASLR & Authenticode bit if set
        return nt->OptionalHeader.DllCharacteristics & (IMAGE_DLLCHARACTERISTICS_FORCE_INTEGRITY | IMAGE_DLLCHARACTERISTICS_DYNAMIC_BASE)
            ? (nt->OptionalHeader.DllCharacteristics &= ~(IMAGE_DLLCHARACTERISTICS_FORCE_INTEGRITY | IMAGE_DLLCHARACTERISTICS_DYNAMIC_BASE), true)
            : false;
    }
---
