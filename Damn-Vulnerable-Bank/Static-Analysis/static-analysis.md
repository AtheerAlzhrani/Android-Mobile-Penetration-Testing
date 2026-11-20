# Static Analysis

## Overview
Static analysis was performed on the Damn Vulnerable Bank (DVB) Android application using JADX to inspect application components, configurations, and source code.

## Tools
- JADX
- Android Manifest
- Mobexler

## Areas Reviewed
- Android application configuration
- Network security configuration
- Authentication and session management
- Local data storage
- Cryptographic implementation
- Password management
- Financial transactions
- API configuration
- Logging and information exposure

## Key Observations

| ID | Security Area | Observation |
|---|---|---|
| S-01 | Network Security | Cleartext traffic is permitted. |
| S-02 | Network Security | User-installed certificates are trusted. |
| S-03 | Data Protection | Application backup is enabled. |
| S-04 | Access Control | SendMoney activity is exported. |
| S-05 | Access Control | ViewBalance activity is exported. |
| S-06 | Deep Links | HTTP and HTTPS deep links are configured. |
| S-07 | Logging | Access token is written to Logcat. |
| S-08 | Storage | JWT is stored in SharedPreferences. |
| S-09 | Cryptography | Custom XOR encryption uses a hardcoded key. |
| S-10 | Transaction Security | Biometric authentication is used in the transfer flow. |
| S-11 | Input Validation | Transaction input validation requires further review. |
| S-12 | Logging | Transaction response data is logged. |
| S-13 | Session Management | Access token is not explicitly cleared after password changes. |
| S-14 | API Configuration | Backend URL is configurable and stored locally. |
| S-15 | Registration | No client-side input validation is visible in the registration method. |

## Preliminary Assessment

The static analysis identified several areas requiring further security assessment, particularly:

- Weak cryptographic implementation.
- Sensitive information handling.
- Exported Android activities.
- Network communication security.
- Authentication and session management.
- Transaction authorization and input validation.

These observations are preliminary and have not yet been confirmed as exploitable vulnerabilities.

## Next Phase

Dynamic analysis will be performed to validate the identified observations and investigate additional vulnerabilities.


## Evidence


- <img width="835" height="927" alt="image" src="https://github.com/user-attachments/assets/2252c13d-2362-4033-a855-c91ab4991272" />
- <img width="680" height="202" alt="image" src="https://github.com/user-attachments/assets/3969efce-5115-4604-9c05-3b85265f880f" />
- <img width="937" height="387" alt="image" src="https://github.com/user-attachments/assets/89642e51-2939-45e6-988a-1173862fb67d" />
- <img width="786" height="505" alt="image" src="https://github.com/user-attachments/assets/4420ada4-cdb5-4215-a6fc-03f359692e07" />
- <img width="931" height="767" alt="image" src="https://github.com/user-attachments/assets/ca05b5f3-04ca-45db-a3cf-7c133e6b4986" />
- <img width="942" height="931" alt="image" src="https://github.com/user-attachments/assets/e036ea9b-49fd-4c1c-8257-f358a9acd0ec" />
- <img width="936" height="686" alt="image" src="https://github.com/user-attachments/assets/3cf838b9-0f4d-4aeb-b079-0626473d3fbb" />










