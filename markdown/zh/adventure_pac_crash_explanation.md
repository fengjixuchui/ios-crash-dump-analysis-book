### 指针验证机制崩溃

之前，在 _指针验证机制_ 一章中，我们看到了用户启用指针验证机制会导致崩溃。接下来我们看一些使用指针验证机制的系统库发生的崩溃。

```
Incident Identifier: 692E5696-6994-4FB3-B42D-C9317D956EE7
CrashReporter Key:   1f2cdb7448d354584634e8576c1e5257634fc0cd
Hardware Model:      iPhone12,1
Process:             get [1737]
Path:               
 /private/var/containers/Bundle/Application/2BF678BB-7CC6-4CAC-BF
49-0298B611F1BA/get.app/get
Identifier:         
 com.soul.merge.cat.cute.simulator.adventure.get
Version:             44 (1.4.4)
AppStoreTools:       11C29
AppVariant:          1:iPhone12,1:13
Code Type:           ARM-64 (Native)
Role:                Foreground
Parent Process:      launchd [1]
Coalition:          
 com.soul.merge.cat.cute.simulator.adventure.get [757]

Date/Time:           2019-12-26 09:54:15.6806 +0300
Launch Time:         2019-12-26 09:43:08.8423 +0300
OS Version:          iPhone OS 13.3 (17C54)
Release Type:        User
Baseband Version:    1.03.12
Report Version:      104

Exception Type:  EXC_BAD_ACCESS (SIGSEGV)
Exception Subtype: KERN_INVALID_ADDRESS at 0x41fc821e000001b0 ->
 0xffffff9e000001b0 (possible pointer authentication failure)
VM Region Info: 0xffffff9e000001b0 is not in any region.  Bytes
 after previous region: 18446743641528467889
      REGION TYPE                      START - END             [
 VSIZE] PRT/MAX SHRMOD  REGION DETAIL
      MALLOC_NANO            0000000280000000-00000002a0000000
 [512.0M] rw-/rwx SM=PRV
--->
      UNUSED SPACE AT END

Triggered by Thread:  27

Thread 27 name:
Thread 27 Crashed:
0   libEmbeddedSystemAUs.dylib          0x00000001d0246644
 InterruptionListener(void*, unsigned int, unsigned int, void
 const*) + 352 (AURemoteIO.cpp:257)
1   libEmbeddedSystemAUs.dylib          0x00000001d0246578
 InterruptionListener(void*, unsigned int, unsigned int, void
 const*) + 148 (AURemoteIO.cpp:256)
2   AudioToolbox                        0x00000001bd34e710
 AudioSessionPropertyListeners::CallPropertyListeners(unsigned
 int, unsigned int, void const*) + 596
 (AudioSessionPropertyListeners.cpp:146)
3   AudioToolbox                        0x00000001bd3ab564
 HandleAudioSessionCFTypePropertyChangedMessage(unsigned int,
 unsigned int, void*, unsigned int) + 1104 (AudioSession.cpp:932)
4   AudioToolbox                        0x00000001bd3aac1c
 ProcessDeferredMessage(unsigned int, __CFData const*, unsigned
 int, unsigned int) + 2540 (AudioSession.cpp:1050)
5   AudioToolbox                        0x00000001bd4187e0
 _XAudioSessionPingMessage + 688 (AudioSession.cpp:1161)
6   libAudioToolboxUtility.dylib        0x00000001bd4a76b4
 mshMIGPerform + 268 (MachServerHelper.c:450)
7   CoreFoundation                      0x00000001b1f207c4
 __CFRUNLOOP_IS_CALLING_OUT_TO_A_SOURCE1_PERFORM_FUNCTION__ + 60
 (CFRunLoop.c:1937)
8   CoreFoundation                      0x00000001b1f1fe90
 __CFRunLoopDoSource1 + 448 (CFRunLoop.c:2075)
9   CoreFoundation                      0x00000001b1f1aac8
 __CFRunLoopRun + 2144 (CFRunLoop.c:3098)
10  CoreFoundation                      0x00000001b1f19f40
 CFRunLoopRunSpecific + 480 (CFRunLoop.c:3192)
11  AVFAudio                            0x00000001beeb1f70
 GenericRunLoopThread::Entry(void*) + 160
 (GenericRunLoopThread.h:91)
12  AVFAudio                            0x00000001bef031fc
 CAPThread::Entry(CAPThread*) + 208 (CAPThread.cpp:286)
13  libsystem_pthread.dylib             0x00000001b1cad840
 _pthread_start + 168 (pthread.c:896)
14  libsystem_pthread.dylib             0x00000001b1cb59f4
 thread_start + 8

Thread 27 crashed with ARM Thread State (64-bit):
    x0: 0x0000000000000000   x1: 0x0000000000000000   x2:
 0x0000000000000100   x3: 0x0000000000000000
    x4: 0x00000000000020a0   x5: 0x0000000000000020   x6:
 0x0000000000000000   x7: 0x00000000000003da
    x8: 0x41fc821e00000000   x9: 0x0000000000000020  x10:
 0x0000000000000000  x11: 0x0000000000000202
   x12: 0x0000000000000002  x13: 0x0000000000000000  x14:
 0x0000000000000002  x15: 0x0000000000000001
   x16: 0x00000001b1c6b43c  x17: 0x00000001f0430630  x18:
 0x0000000000000000  x19: 0x0000000103823040
   x20: 0x00000001710287fc  x21: 0x00000000696e7472  x22:
 0x0000000108aa3b28  x23: 0x000000010fd10588
   x24: 0x000000010fd105a0  x25: 0x0000000064696564  x26:
 0x00000001fb421000  x27: 0x00000000006c9000
   x28: 0x0000000000000049   fp: 0x0000000171028660   lr:
 0xe970e981d0246578
    sp: 0x0000000171028600   pc: 0x00000001d0246644 cpsr:
 0x80000000
   esr: 0x56000080  Address size fault

Binary Images:
0x10005c000 - 0x102687fff get arm64 
 <bde08a08d8cf3e6b8cee8ab2cf246ccb>
 /var/containers/Bundle/Application/2BF678BB-7CC6-4CAC-BF49-0298B
611F1BA/get.app/get
.
.
0x1d01b7000 - 0x1d02c3fff libEmbeddedSystemAUs.dylib arm64e 
 <48e72efe02243faabf3e1760bb4c2731>
 /System/Library/Frameworks/AudioToolbox.framework/libEmbeddedSys
temAUs.dylib
```

这里，我们看到故障地址 `0x41fc821e000001b0`最高 24 位为`41fc82`。 这就是 _指针校验验证码_（PAC）。\index{PAC}

我们看到故障函数 `InterruptionListener` 使用两个指针作为参数，并且我们已经将寄存器 `x8` 的地址设置为`0x41fc821e00000000`。 因此，大概我们的失败代码正在使用该地址，加上一些小的偏移量 `0x1b0`。 这可能是由于使用了手动指针算法，导致使用了未经身份验证的指针。

