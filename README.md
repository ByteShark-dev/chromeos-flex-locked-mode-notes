# ChromeOS Flex on QEMU/KVM — Compatibility Research

**ByteShark · Experimental field notes · 9 November 2026**

[Versión en español](README.es.md)

> This is a single-machine compatibility observation, **not a security vulnerability claim**, a certification of Google Forms Locked Mode, or advice for using an unapproved device in an actual examination.

## Why this experiment?

I wanted to use ChromeOS Flex without replacing my Linux installation. After successfully running it inside QEMU/KVM, I tested a **self-owned demonstration quiz** configured with Google Forms Locked Mode. Some behavior was unexpected and worth recording for independent discussion.

## Tested environment

| Component | Configuration |
| --- | --- |
| Host | CachyOS / Hyprland (Linux x86-64) |
| Host kernel | `7.3.3-1-cachyos` |
| Hypervisor | QEMU `11.1.3` with KVM (Intel VT-x) |
| Guest | ChromeOS Flex, updated to `156.0.8078.93` (64-bit) |
| Original recovery image | Reven `16805.36.0` |
| VM memory / CPUs | 6144 MiB / 2 vCPU |
| Guest storage | 32 GiB QCOW2 disk |
| Display | GTK with OpenGL, `virtio-vga-gl` |
| Input | Virtual USB tablet |
| Network | QEMU user-mode NAT, e1000 adapter |
| Device setup | Personal-device flow; enterprise enrollment did not complete |

The recovery image was installed onto a **separate virtual disk**. The host system and other VMs were not replaced. An initial guest connectivity issue was resolved during setup; the operating system subsequently updated successfully.

## What was observed?

The following checks were conducted **only in a test form owned by the experimenter**.

| Area | Observation | Scope |
| --- | --- | --- |
| ChromeOS Flex installation and startup | Successful | Confirmed on this VM |
| Educational account sign-in | Successful | Account-specific |
| Displaying the demo quiz in Locked Mode | Successful | Interface appeared |
| Submitting a demo response | Successful | Response and score appeared in Forms |
| Reopening the demo quiz | Recorded | Reopening alert visible to form owner |
| Email alert about reopening | Received | Email notification observed |
| Opening another tab inside the guest | Restricted | Observed during the demo |
| Extension UI inside the quiz | Restricted | Observed for installed extensions |
| Guest clipboard during the quiz | Restricted | Test copy/paste did not succeed |
| Security assurances equivalent to an enrolled Chromebook | **Not established** | Not independently validated |

The observation about opening the quiz **does not establish that every device-trust check or security restriction was satisfied**. Policies applied to an educational account are also not proof of device enrollment. No claim is made that a production exam would accept or approve this environment.

## Limitations

- One host, one guest build, and one self-owned demonstration form; no independent reproduction yet.
- No controlled comparison with an officially managed Chromebook.
- Hypervisor and host input/window behaviors are not equivalent to a physical Chromebook.
- A blocked UI action and a disabled underlying extension process are different claims; only the former was observed.
- Clipboard integration between host and guest was absent from this QEMU setup, so cross-system clipboard behavior cannot be attributed to Locked Mode.
- The absence of a visible alert is not proof that no other detection mechanism exists.
- ChromeOS Flex virtualized operation is experimental and is not a supported substitute for a school-managed Chromebook.

## Screenshots

Screenshots were captured during the experiment, but **are not included in this initial public version**. Several contain an institutional email address and account details. Only carefully redacted images will be considered for a later revision.

## References

- [Google: Use locked mode for quizzes](https://support.google.com/docs/answer/7634943)
- [Google: Differences between ChromeOS Flex and ChromeOS](https://support.google.com/chromeosflex/answer/11542901)
- [QEMU system invocation reference](https://www.qemu.org/docs/master/system/invocation.html)

## Responsible discussion

This page documents compatibility research, not a guide to defeating assessment controls. If using a device for a real assessment, follow the institution's instructions and obtain approval. Independent confirmation and constructive corrections are welcome.

*ChromeOS, ChromeOS Flex and Google Forms are Google products. ByteShark is not affiliated with Google or the QEMU project.*
