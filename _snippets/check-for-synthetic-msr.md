---
layout: raw_code
lang: en
title: Check for Synthetic MSR
author: Otávio
author_url:
author_nickname: estr3llas
tags: [windows, cpp, antivm]
code: |
// Reserved MSR Address Space, meaning all future processors will not implement MSRs in this range.
//
// Goes up to 0x400000FF
//
#define SYNTHETIC_MSR_RANGE_START 0x40000000

BOOLEAN CheckForSyntheticMSR() {

    __try {
        __readmsr(SYNTHETIC_MSR_RANGE_START);
    }
    // If by any chance __readmsr returns a value, we are likely being virtualized
    __except(EXCEPTION_EXECUTE_HANDLER) {
        return FALSE;
    }

    return TRUE;
}
---
