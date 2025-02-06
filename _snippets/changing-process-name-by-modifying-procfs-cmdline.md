---
layout: raw_code
lang: en
title: Changing Process Name by Modifying cmdline in Linux
author: Ricardo
author_url:
author_nickname: astreuw
tags: [windows, linux, python]
code: |
  #!/usr/bin/env python3

  import ctypes
  from threading import get_ident

  libc = ctypes.CDLL("libc.so.6")

  libc.pthread_setname_np(
      ctypes.c_ulong(get_ident()),
      ctypes.c_char_p(b"process_name"))
---
