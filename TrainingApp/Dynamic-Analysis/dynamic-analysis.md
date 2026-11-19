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
- Prepared Frida for runtime analysis.

## Results
- Application launches successfully.
- Registration request was captured in Burp Suite.
- No corresponding server response was observed.
- Login and registration testing remain incomplete due to an application error.

## Status
**In Progress** — Further investigation of network connectivity and runtime behavior is required.

## Evidence
- [ ] Application launch
- [ ] Burp Suite request capture
- [ ] Frida runtime inspection
- [ ] Authentication testing
