# Dynamic Analysis

## Environment
- **Device:** Android
- **Testing Environment:** Mobexler
- **Proxy:** Burp Suite
- **Instrumentation:** Frida
- **Application:** TrainingApp
- **Package:** `com.ecardsandkeys`

## Testing Activities
- Verified application installation and launch.
- Confirmed successful execution of `LoginActivity`.
- Configured Burp Suite for network traffic inspection.
- Captured an HTTP registration request.
- Successfully launched TrainingApp through Frida.
- Established a Frida instrumentation session.
- Verified Java runtime availability (`Java.available = true`).
  
## Results
- Application launches successfully.
- Registration request was captured in Burp Suite.
- No corresponding server response was observed.
- Login and registration testing remain incomplete due to an application error.

## Status
**In Progress** — Further investigation of network connectivity and runtime behavior is required.

## Evidence
- <img width="737" height="362" alt="image" src="https://github.com/user-attachments/assets/23683c3d-c95c-4487-b456-d4ba7ba83b87" />

- <img width="790" height="355" alt="image" src="https://github.com/user-attachments/assets/5eb8cac8-1d66-4e8b-8aa4-ec37606b821f" />


-  <img width="817" height="102" alt="image" src="https://github.com/user-attachments/assets/01c4f86c-3804-49f1-980b-3ad6f935ba70" />

-  <img width="767" height="472" alt="image" src="https://github.com/user-attachments/assets/ed08c2ad-9fa2-405e-9873-658b0e4da858" />

