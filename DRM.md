# DRM(Digital Rights Management) Policy term

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

