
---

# Registry Explorer ~ Live Machine & TryHackMe

**Date:** 2026-04-27 · **Category:** DFIR · 

---

## What was this about?

Hands-on experience with the Windows Registry. First inside a TryHackMe room and then on a live machine. Theory is one thing. Actually working with the data is a different experience entirely.

---

## What did I know beforehand?

I had never used Registry Explorer before and did not know what to expect. The one thing I did know was that the registry holds a significant amount of forensically relevant information and that understanding it would matter in a real investigation.

---

## What did I do?

I worked through the TryHackMe Windows Forensics room and read the official Microsoft documentation on registry hives. I then downloaded the Eric Zimmerman tools into my Windows VM to continue practising outside the guided environment.

**Setup:**
I worked on a MacBook Pro M2 running a Windows 11 VM via UTM. 
Eric Zimmerman tools were installed at C:\Tools\Zimmerman\net9\

---

## What did I learn?

The first time I opened Registry Explorer was inside the TryHackMe room. Since it was completely new to me I explored the interface before attempting the assigned tasks. I was surprised by the sheer amount of information the registry exposes and initially wondered how I would ever make sense of it all.

What I did not expect was how much I would recognise, not from having seen it before but from having studied the theory. The preparation made it clear where to look and what to do.

It was still challenging given the number of paths and terms involved but I genuinely enjoyed it.

---

Afterwards I moved into my Windows VM and loaded the SAM hive from my live machine into Registry Explorer to test whether I could navigate independently. My goal was to locate the different user accounts.

I found them without needing guidance.

That told me something: active learning and consistent note-taking are paying off. I am still relying heavily on my notes at every step and have a lot of terminology left to internalise but the foundation is there.

---

## Sources

- [TryHackMe | Windows Forensics 1](https://tryhackme.com/room/windowsforensics1)
- [Microsoft Documentation | Registry Hives](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry-hives)
- [Digital Corpora | DOMEX sample drives](https://digitalcorpora.s3.amazonaws.com/s3_browser.html#corpora/drives/nps-2009-domexusers/)

---

## Next steps

Timeline Explorer and understanding how it presents a chronological view of events on a machine and how to interpret what it shows.

---

