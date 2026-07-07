# 10 Digital Security

## Digital Security Risk

- **Digital Security Risk (数字安全风险)** is an event that could cause loss of or damage to computer or mobile device hardware, software, data, information, or processing capability.
  中文：数字安全风险是会导致硬件、软件、数据、信息或处理能力损失/损坏的事件。
- **Computer Crime (计算机犯罪)** is any illegal act involving the use of a computer or related devices.
  中文：计算机犯罪是任何涉及电脑或相关设备的违法行为。
- **Cybercrime (网络犯罪)** is an online or Internet-based illegal act.
  中文：网络犯罪是发生在线上或互联网中的违法行为。
- **Exam Focus - Fill-in**: Event causing loss/damage to hardware, software, data, or information = **Digital Security Risk**.
  中文：event causing loss/damage，对应 Digital Security Risk。
- **Exam Focus - Fill-in**: Illegal act involving use of computers = **Computer Crime** or cybercrime depending on online context.
  中文：只说 use of computers 是 Computer Crime；强调 online/Internet 是 Cybercrime。
- **Practice Focus - Short Answer**: Explain digital security risks and types of malware.
  中文：简答题先定义风险，再列 malware 类型。

## Malware

- **Malware / Malicious Software (恶意软件)** means harmful software written with bad intention.
  中文：恶意软件是带有恶意目的、会伤害系统或数据的软件。
- **Virus (病毒)**: a potentially damaging program that affects or infects a computer or mobile device without the user's knowledge or permission. It usually requires user action to activate and can alter how the device works.
  中文：病毒通常需要用户打开文件/程序才激活，会感染设备并改变其工作方式。
- **Worm (蠕虫)**: a program that copies itself repeatedly, uses resources, and may shut down a device or network.
  中文：蠕虫会自我复制，占用资源，可能让设备或网络瘫痪。
- **Trojan Horse (特洛伊木马)**: a program that hides within or looks like a legitimate program; unlike a virus or worm, it does not replicate itself.
  中文：木马伪装成正常程序，不像病毒/蠕虫那样自我复制。
- **Payload (载荷 / 破坏事件)**: the destructive event delivered when malware is triggered.
  中文：payload 是恶意软件触发后真正造成破坏的部分。
- **Macro Virus (宏病毒)**: malicious code written in word processing or spreadsheet programs.
  中文：宏病毒藏在 Word、Excel 等宏功能中。
- **Adware (广告软件)**: displays online advertisements in banners, pop-ups, pop-unders, email, or other Internet services.
  中文：广告软件会弹广告、横幅、弹窗等。
- **Ransomware (勒索软件)**: blocks or limits access to a computer, phone, or file until the user pays money.
  中文：勒索软件锁住设备或文件，要求付款。
- **Rootkit (Rootkit 隐匿工具)**: hides in a device and allows remote control.
  中文：Rootkit 隐藏在设备里，让攻击者远程控制。
- **Spyware (间谍软件)**: secretly collects user information and sends it to an outside source.
  中文：间谍软件偷偷收集用户资料并发给外部来源。
- **Backdoor (后门)**: a program or instruction set that allows users to bypass security controls.
  中文：后门让人绕过正常安全控制进入系统。
- **Exam Focus - Fill-in**: Program blocking access until payment = **Ransomware**.
  中文：blocks access until payment，就是 Ransomware。
- **Exam Focus - Fill-in**: Malicious code in Microsoft Word programs = **Macro Virus**.
  中文：Microsoft Word malicious code，答案 Macro Virus。
- **Exam Focus - Fill-in**: Potentially damaging program that alters a device without permission = **Virus**.
  中文：damaging program + alters device without permission，答案 Virus。
- **Exam Focus - Fill-in**: Program secretly collecting user information = **Spyware**.
  中文：secretly collects information，答案 Spyware。
- **Exam Focus - Fill-in**: Software displaying advertisements = **Adware**.
  中文：display advertisements，答案 Adware。
- **Exam Focus - Fill-in**: Program bypassing security controls = **Backdoor**.
  中文：bypass security controls，答案 Backdoor。
- **Exam Focus - MCQ**: Malware that spreads automatically across networks without user action = **Worm**.
  中文：自动传播、不需要用户操作，答案 Worm。
- **Exam Focus - MCQ**: Malware hidden in a legitimate program = **Trojan Horse**.
  中文：隐藏/伪装成合法程序，答案 Trojan Horse。

## Internet and Network Attacks

- **Botnet (僵尸网络)**: a group of compromised computers or mobile devices connected to a network.
  中文：僵尸网络是一组被入侵并连接在网络中的设备。
- **Zombie PC (僵尸电脑)**: a compromised computer or device used by an attacker.
  中文：僵尸电脑是被攻击者控制的电脑或设备。
- **Denial-of-Service / DoS attack (拒绝服务攻击)**: disrupts access to an Internet service.
  中文：DoS 通过干扰服务，让用户无法访问网站或网络服务。
- **Distributed Denial-of-Service / DDoS attack (分布式拒绝服务攻击)**: a larger-scale DoS attack using multiple computers or networks.
  中文：DDoS 是更大规模的 DoS，使用多台设备一起攻击。
- **Exam Focus - Fill-in**: Group of compromised computers controlled by a hacker = **Botnet**.
  中文：group of compromised computers，答案 Botnet。
- **Exam Focus - Fill-in**: Large-scale attack meant to shut down machines or networks = **DDoS attack**.
  中文：large-scale shut down machines/networks，答案 DDoS。

## Antivirus and Virus Signatures

- **Antivirus software (防病毒软件)** was originally developed to detect and remove viruses, and also protects against worms and Trojan horses.
  中文：防病毒软件用来检测和删除病毒，也能防蠕虫和木马。
- **Virus Signature (病毒特征码)** is the specific binary pattern of a virus's machine code, also called a virus definition.
  中文：病毒特征码是病毒机器码中的特定二进制模式，也叫病毒定义。
- Antivirus programs look for virus signatures to identify viruses.
  中文：防病毒软件通过查找特征码识别病毒。
- **Exam Focus - Short Answer**: Antivirus protection process:
  中文：简答题按流程写：
  1. Scan files for viruses.
     中文：扫描文件。
  2. Detect suspicious files.
     中文：检测可疑文件。
  3. Block the threat.
     中文：阻止威胁。
  4. Quarantine infected files.
     中文：隔离感染文件。
  5. Remove or repair infected files.
     中文：删除或修复感染文件。

## Preventive Measures

- Install antivirus software on all computers.
  中文：所有电脑安装防病毒软件。
- Install a personal firewall program.
  中文：安装个人防火墙。
- Never open email attachments unless they are from a trusted source.
  中文：不打开不可信来源的邮件附件。
- Delete infected email attachments immediately.
  中文：发现附件感染后立即删除。
- Scan removable media.
  中文：扫描 U 盘等可移动设备。
- Check downloaded programs for viruses, worms, and Trojan horses.
  中文：检查下载程序是否含病毒、蠕虫、木马。
- Never start a computer with removable media.
  中文：不要用可移动介质启动电脑。
- Set macro security in applications so macros can be enabled or disabled.
  中文：设置宏安全级别，控制是否启用宏。
- Use VPN on public Wi-Fi to improve privacy.
  中文：公共 Wi-Fi 下用 VPN 保护隐私。
- Install updates regularly to patch vulnerabilities.
  中文：定期更新系统，修补漏洞。
- **Exam Focus - Short Answer**: Methods to secure computers/devices include 2FA, strong unique passwords, VPN, antivirus, firewall, secure websites, updates, and user education.
  中文：简答题可以任选写：2FA、强密码、VPN、防病毒、防火墙、安全网站、更新、用户教育。

## System Failure and Backup

- **System Failure (系统故障)** is prolonged malfunction of a computer, caused by aging hardware, natural disasters, or electrical power disturbances.
  中文：系统故障是电脑长时间无法正常工作，可能由硬件老化、自然灾害、电力问题造成。
- **Surge Protector (电涌保护器)** protects equipment from electrical power disturbances.
  中文：电涌保护器防止电力波动损坏设备。
- **Uninterruptible Power Supply / UPS (不间断电源)** provides power during power loss.
  中文：UPS 在断电时继续供电。
- **Backup (备份)** duplicates files, programs, or disks.
  中文：备份就是复制文件、程序或磁盘。
- **Full Backup (完整备份)** backs up all files.
  中文：完整备份备份所有文件。
- **Selective Backup (选择性备份)** backs up selected files.
  中文：选择性备份只备份选定文件。

## Digital Signature, Digital Certificate, SSL

- **Secure Site (安全网站)** uses encryption to secure data.
  中文：安全网站用加密保护数据。
- **Digital Signature (数字签名)** is encrypted code attached to an electronic message to verify the identity of the sender and help ensure the transaction details are not modified during transfer.
  中文：数字签名是附在电子消息上的加密代码，用来验证发送者身份，并确保传输中内容未被修改。
- **Digital Certificate (数字证书)** is a notice that guarantees a user or website is legitimate.
  中文：数字证书证明用户或网站是合法可信的。
- **Certificate Authority / CA (证书颁发机构)** issues and verifies digital certificates.
  中文：CA 负责签发和验证数字证书。
- **Secure Socket Layer / SSL (安全套接层)** encrypts data passing between a client and Internet server; web addresses beginning with **https** indicate secure connections.
  中文：SSL 加密客户端和服务器之间的数据；网址 https 表示安全连接。
- **Exam Focus - Short Answer**: Explain digital signature and digital certificate.
  中文：简答题：signature 验身份/防篡改；certificate 证明用户或网站合法。
- **Exam Focus - MCQ**: Digital signature ensures transaction details are not modified during transfer.
  中文：not modified during transfer，对应 Digital Signature。
- **Exam Focus - MCQ**: Digital certificate is issued by a **Certificate Authority (CA)**.
  中文：谁发数字证书？Certificate Authority。
- **Exam Focus - MCQ**: When a digital certificate expires, it becomes invalid and communication is no longer secure.
  中文：证书过期后无效，通信不再安全。

## Disaster Recovery Plan

- **Disaster Recovery Plan (灾难恢复计划)** is a written plan for restoring computer operations after a disaster.
  中文：灾难恢复计划是灾难后恢复电脑运作的书面计划。
- **Emergency Plan (紧急计划)**: steps taken immediately after disaster.
  中文：灾难刚发生后立即采取的步骤。
- **Backup Plan (备份计划)**: how backup files and equipment resume information processing.
  中文：说明如何用备份文件和设备恢复信息处理。
- **Recovery Plan (恢复计划)**: actions to restore full information processing operations.
  中文：恢复完整信息处理操作的行动。
- **Test Plan (测试计划)**: simulates disaster levels and records recovery ability.
  中文：模拟不同灾难程度，并记录恢复能力。
- **Exam Focus - Fill-in**: In disaster recovery, **Test Plan (测试计划)** simulates or tests recovery procedures.
  中文：simulates disaster/recovery procedures，答案 Test Plan。

## CIA Triad

- **CIA Triad (CIA 三元组)** means **Confidentiality (机密性)**, **Integrity (完整性)**, and **Availability (可用性)**.
  中文：CIA 三元组是网络安全三大目标：保密、完整、可用。
- **Exam Focus - MCQ**: CIA triad = Confidentiality, Integrity, Availability.
  中文：CIA 不要背成别的词，就是 Confidentiality、Integrity、Availability。

## Likely Answer Structure

For "Describe attacks and safeguards", write:

1. Attacks include malware, botnets/zombies, DoS, DDoS, backdoors, ransomware, spyware, and phishing-like threats.
   中文：先列攻击类型：恶意软件、僵尸网络、DoS/DDoS、后门、勒索、间谍软件等。
2. Safeguards include antivirus, firewall, strong passwords, 2FA, VPN, updates, scanning downloads/removable media, macro controls, and user education.
   中文：再列防护措施：防病毒、防火墙、强密码、双重验证、VPN、更新、扫描、宏控制、教育用户。
3. For recovery, use backups and a disaster recovery plan with emergency, backup, recovery, and test plans.
   中文：最后写恢复：备份 + 灾难恢复计划四部分。
