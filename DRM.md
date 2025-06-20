# DRM(Digital Rights Management) Policy term

### ❓ What is DRM and why is it used?
- ✅ DRM (Digital Rights Management) is a technology used to protect digital content (like video, audio, or eBooks) from unauthorized access, copying, or redistribution. It's crucial for OTT platforms to control how, where, and by whom the content is consumed.

#### ❓ What are the major DRM systems?
✅ Popular DRM systems include:
- Google Widevine – for Android, Chrome
- Microsoft PlayReady – for Windows, Xbox
- Apple FairPlay – for iOS, macOS, Safari
- Pallycon – multi-DRM SaaS provider (supports Widevine, PlayReady, FairPlay)

#### ❓ What is Multi-DRM?
- ✅ Multi-DRM refers to using a single workflow to support multiple DRM schemes. It allows content to be played across platforms/devices that support different DRM systems.

## 🔐 DRM Workflow

### ❓ What is the role of a license server in DRM?
- ✅ The license server securely issues decryption keys (licenses) to the client after validating device and user credentials. It enforces playback rights and restrictions.

### ❓ What is an SPC in DRM?
- ✅ SPC (Service Provider Certificate) is used by a client (like an app) to authenticate itself with the license server. It contains the public key and identity of the service.

### ❓ What is a CAPC in DRM?
- ✅ CAPC (Content Access Policy Certificate) defines the rules for how the protected content can be used—e.g., play duration, resolution limit, expiration, etc.

### ❓ What is a license token?
- ✅ A license token is a signed object issued by your backend that specifies what content can be played, by whom, and for how long. It accompanies the license request.

## 🔐 Content Encryption

### ❓ How is content encrypted for DRM?
- ✅ Video/audio files are encrypted using AES-128 or AES-CTR algorithms during packaging. Only users with valid licenses (decryption keys) can play them.

### ❓ What is key rotation in DRM?
- ✅ Key rotation means using different encryption keys for different segments of a video (e.g., every 10 seconds). This improves security and mitigates key leaks.

### ❓ What is CENC?
- ✅ CENC (Common Encryption) is a standard allowing content to be encrypted once but used with multiple DRM systems, thanks to shared encryption parameters.

## 📱 Playback & Platform

### ❓ How does DRM playback work on iOS (FairPlay)?
App gets the FairPlay application certificate.
Generates an SPC (license request) and sends it to the license server.
Receives a CKC (license response) with keys.
AVFoundation handles decryption and playback.

### ❓ What are spc, ckc, and certificate in FairPlay?
- **spc** – Secure Playback Context (license request)
- **ckc** – Content Key Context (license response)
- **certificate** – Authenticates your app to the license server
  
### ❓ What is Widevine L1 vs L3?
- **L1:** Hardware-backed DRM, supports HD/UHD playback.
- **L3:** Software-only DRM, limited to SD playback and lower security.

## 🛡️ Security & Protection

### ❓ What is a Secure Video Path (SVP)?
- ✅ SVP ensures that decrypted video is never accessible in memory, instead passing through a trusted hardware pipeline to the display.

### ❓ How does DRM prevent screen recording?
- DRM systems enforce OS-level restrictions using HDCP(High-bandwidth Digital Content Protection) is one mechanism used to achieve this., display restrictions, or hardware playback paths to block or distort content during screen recording.

### ❓ How is offline playback protected?
- The license is stored securely on the device (encrypted) and has strict expiry, usage, and device-binding policies enforced by DRM.

## 🧪 Policy & Playback Control

### ❓ What kind of policies can DRM enforce?
- Playback resolution
- Expiration time
- Device limit
- Download or stream only
- Geo-restriction
- HDCP enforcement

###❓ What is the difference between persistent and non-persistent licenses?
Persistent: License is stored and reused for offline playback.
Non-persistent: License is valid only for the current session or stream.
❓ How does key delivery ensure security?
Keys are delivered via secure protocols (HTTPS), and encrypted using public/private key cryptography. Devices authenticate using certificates (SPC).
🧰 Backend & Packaging

❓ What is used to package encrypted content?
Shaka Packager
MP4Box (GPAC)
ffmpeg with DRM support
AWS MediaConvert, Bitmovin, or Axinom
❓ What is CPIX?
✅ CPIX (Content Protection Information Exchange) is an XML-based standard for sharing encryption keys and policies between content preparation and DRM license servers.
💡 Bonus

❓ What is Clear Key?
✅ Clear Key is a basic form of DRM where encryption keys are shared directly (not securely). It’s only used for testing or non-production scenarios.
❓ What is forensic watermarking?
✅ Forensic watermarking embeds unique, invisible identifiers in each playback stream. If leaked, it can be traced back to a specific user or session.
🧠 Real-World Scenarios

❓ How do you revoke content access after it’s downloaded?
Use license expiry or server-driven revocation policies (e.g., "kill switch"). The app checks validity before playback.
❓ How do you prevent access from rooted/jailbroken devices?
Use SDK-based tamper checks, secure boot verification, and DRM systems that restrict playback on compromised environments.
If you'd like this exported as a Markdown file for direct use in your GitHub README, I can generate that for you too. Just let me know!


## 🔐 SPC — Service Provider Certificate

**SPC** is typically a certificate issued to a DRM license or content service provider (CSP) like Pallycon or your OTT platform.
It authenticates the service to a DRM key/license server.
It includes cryptographic information (like a public key) used to sign or encrypt messages.
🧠 Used For:
Signing license requests
Establishing a trust relationship between client apps and DRM servers
Identifying the platform/service requesting content

## 🔐 CAPC — Content Access Policy Certificate (or Content Access Protection Certificate)

**CAPC** is a certificate or token that defines the content access policy.
It tells the DRM system how the content can be used — whether it can be:
Downloaded
Streamed
Played on specific devices
Limited by time (expiry), resolution, screen recording, etc.
🧠 Used For:
Enforcing usage rules for protected content
Defining content-level rights
Providing client apps with permission constraints
📦 Where You Might See SPC and CAPC

In DRM SDKs (e.g., Pallycon, Widevine Modular DRM), these are usually used when:
Generating license requests
Playing protected content
Setting up encryption during content packaging
For example, in Pallycon SDK (iOS/tvOS):
The SPC might be part of a request to the license server.
The CAPC (along with a license token) defines what playback is allowed and must match the player/device profile.


### ✅ Summary
| Term     | Full Form                         | Role in DRM                                |
| -------- | --------------------------------- | ------------------------------------------ |
| **SPC**  | Service Provider Certificate      | Authenticates your service to DRM provider |
| **CAPC** | Content Access Policy Certificate | Defines usage rules and rights for content |

