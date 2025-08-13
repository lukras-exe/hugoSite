---
title: "Security Research and Reverse Engineering on iOS"
summary: "Medium blog post about iOS exploitation for security research and reverse engineering on iOS."
date: 2024-12-26T00:00:00Z
draft: false
---

Mobile smartphone devices have become seamlessly integrated in our daily professional and personal lives, and the security of iOS has never been more important. I will explain a general overview of iOS security research and iOS reverse engineering, exploring methodologies used to identify exploits and vulnerabilities within iOS as well as delving into the concept of jailbreaking, explaining its purpose, methods, and challenges it faces due to Apple’s improving security measures.

### Tool Evaluation
In the space of reverse engineering iOS, there are many reverse engineering frameworks and tools that are used by professionals, and knowing which one to use is one of the key considerations as each disassembler and decompiler can offer their own different pros and cons. The main point of a disassembler is to read machine code on an executable file, for instance, translate that machine code instruction to human- readable assembly language and identify functions, data sections, and memory addresses. Decompilers on the other hand, start with the disassembled code, analyze it to identify higher-level structures like loops and conditionals, reconstruct the variables and data types, and then generate that pseudocode to a high-level language code like C, that essentially approximates the original source code.

#### Disassemblers, Decompilers, and Reverse Engineering Frameworks
Two of the main disassemblers that I have used from personal experience are IDA pro, and Hopper (on macOS). IDA Pro is one of the most sophisticated commercial disassembler and debugger. It offeres various key features like disassembling complex code with an interactive programmable interface, as well as support for scripting languages like Python. This is very useful in iOS security research because it can analyze ARM and ARM64 instruction sets on iOS. Hopper is another reverse engineering tool solely built for macOS and Linux. Hopper essentially performs everything as IDA Pro does, but it is more capable in terms of analyzing macOS and iOS binaries and it’s often considered a more accessible alternative to IDA since it’s more affordable and focuses more on the Apple ecosystem especially when working with iOS security research.

![Hopper v3 dissassembler example](/images/HopperExample.jpg)

**Ghidra**, developed by the NSA in 2019, is a popular choice when it comes to reverse engineering. I personally don’t have much experience with it but, it can analyze compiled code on various platforms not limited to just iOS and macOS. This is why it is considered one of the more popular and desired tools for reverse engineering. It is customizable and users can create their own extensions and scripts to help with iOS reverse engineering. Although it does lack some advanced features found in IDA Pro, overall it is a great tool not only because its capable of analyzing malicious code, but because its completely free.

#### iOS Tools

When it comes to iOS specific tools, most of them are found in repos on Cydia, a package manager for iOS after iOS has been jailbroken.

**Cycript** is one of the special tools used by developers to explore and modify running applications (runtime manipulation) on iOS and macOS developed by Jay Freeman, a popular software engineer. Cycript is used for a variety of cases including analysis of iOS apps, manipulating the application state during runtime and bypassing security measures for research purposes. 

**Clutch** is another iOS open-source tool with the sole purpose of decrypting iOS applications. Decrypting iOS apps is needed in order to be able to reverse engineer them. Decrypting an iOS app or the operating system itself using Clutch involves several stes including jailbreaking an iOS device, installing Clutch and then using SSH to secure a connection to the iPhone from your macOS machine. Clutch injects itself into an application process, then dumps the decrypted app from memory, and reconstructs the app bundle with the decrypted binary that can be viewed in on of the reverse engineering tools.

![iOS filesystem accessed through ssh](/images/iosFilesystem.jpg)

The iOS filesystem and directory is viewable through FileZilla and ssh. To log into the iPhone, you can run the command 

    ssh root@ip-address 

with *root* being the user name and *alpine* being the password. You are able to then manage your way around the iOS filesystem using simple commands like ls, and cd just like in Linux. We can see that when we change the directory to root, and list the contents, we can see some very familiar files like /etc, /bin, /boot, /usr, etc similar to the Linux operating systems.

### Jailbreaking/Decryption
In order for any reverse engineering to happen, the OS, or applciations in iOS need to be decrypted with various iOS jailbreaks. When the idea of jailbreaking is mentioned, specifically iOS jailbreaking, it refers to removing software restrictions that are intentionally put in place by Apple through a series of kernel patches. The term “kernel” in iOS refers to the core part of the iOS operating system, that manages system resources, and acts as a bridge between software applications and hardware. By exploiting kernel vulnerabilities or modifying kernel behavior, “jailbreakers” can bypass Apple’s security measures, making kernel exploitation a central aspect of both jailbreaking and iOS security research.

#### Purpose
There are many reasons as to why someone would want to jailbreak their device. The process of jailbreaking allows users to gain root access to their iOS file system and manager, allowing them to install applications, extensions, and themes not offered through the official App Store, with various package managers like Cydia, and Sileo. There are numerous tools that can be used to jailbreak an iPhone but it all depends on what model iPhone and what iOS version is being jailbroken. Checkra1n is a popular jailbreak tool specifically for iOS devices that are based off the “checkm8” bootrom exploit (iPhone 5s up to the iPhone 11). The Unc0ver jailbreak tool only supports iOS versions from 11.0 to 13.0. Different devices require different steps to jailbreak your iOS device.

![iPhone test devcice running Neofetch command](/images/iPhoneNeofetch.jpg)

Neofetch is a popluar command line interface (CLI) system tool commonly used in Unix-like operating systems such as Linux, and macOS, that displays an aesthetic and concise overview of the systems hardware and software configuration. This is also possible on iOS after jailbreaking it as it allows us to run commands on itself. In Cydia, there is a special repository just for Neofetch on iOS and after installation, Neofetch is able to execute on a terminal on iOS.

#### Future of Jailbreaking
The process of jailbreaking an iPhone requires having a jailbreak-compatible iPhone with a compatible iOS version as not all iOS versions are compatible with all iPhones. Jailbreaking has increasingly been incredibly difficult as:
- Apple continuously improves their iOS security and its proactive stance against jailbreaking
- Jailbreaking is becoming very unpopular because with every iOS update version, Apple integrates all the jailbreak-able features from previous versions into current iOS versions, therefore not having a need to jailbreak a device anymore
- Jailbreak tool and “tweak” creators/developers get contacted by Apple to work for them instead of progressing the future of jailbreaking

![Time in days it took to jailbreak each iOS version](/images/iOSJailbreakGraph.jpg)

This graph depicts the timeline of iOS jailbreaks, showing a clear trend of iOS devices increasingly getting significantly more difficult to jailbreak with each new release. Initially, jailbreaking an iPhone was relatively simple and straightforward. iPhone OS released in June 2007 was jailbroken in less than 2 weeks. As time progressed by the time iOS 12/13 were released, the average time to achieve a stable jailbreak extended several months and iOS 16 took almost 2 years.

### Risks, Legality, and Ethical Considerations
While jailbreaking offers the freedom to customize and use your device beyond Apple’s restrictions, it comes with significant legal and ethical risks. Jailbreaking is legal for personal use but the legal status in some countries can vary, with laws against bypassing digital rights management (DRM), as well as Apple’s EULA explicitly prohibits jailbreaking. By jailbreaking, you breach the EULA agreement which can lead to Apple denying you service/support for your device as Apple does consider jailbreaking a violation of the warranty.

There are also many ethical risks associated with iOS security research and reverse engineering and should be taken into serious consideration. There are major security vulnerabilities with jailbreaking, making your device more susceptible to malware, and other security threats, which puts your personal data at risk. Jailbreaking allows the installation of untrusted software and should be treated like an Android phone where you can install whatever you want off any random website. This can lead to the installation of malicious software and can harm your device.

Security research and reverse engineering in general causes system instability. Like explained before, security research involves manipulating, and testing the operating system and application in ways that were not originally intended for. This can cause crashes, freezes and general unpredictable behavior such as “bricking” your device. “Bricking” your devices refers to the idea where your phone ultimately becomes unusable and there is nothing you can do. Researchers should use dedicated devices just for testing purposes.

### Conclusion
The overall landscape of iOS security research and reverse engineering is a fairly complex topic with a lot of information that can still be covered with great detail. The analysis of these different disassemblers, decompilers and revere engineering frameworks, highlight the importance of selecting the right tools. Whether it’s iOS specific tools, or disassemblers, they play a crucial role for decrypting, and manipulating iOS, gaining a deeper understanding of iOS security mechanisms.

While jailbreaking and iOS security research offer valuable insights and capabilities, it should be approached with immense caution and responsibility. Anyone involved with such activities should prioritize ethical considerations and legal compliance. While a controversial topic, Jailbreaking remains a crucial aspect of iOS security research offering access to the system’s internals. However, as discussed, the future of jailbreaking faces challenges with improved security from Apple and integration not being supported and updated.

Blog post on [Medium](https://medium.com/@lkrapukaitis_70061/security-research-and-reverse-engineering-on-ios-dfcd2fd14329)