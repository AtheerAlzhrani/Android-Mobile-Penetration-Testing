# Dynamic Analysis

## 1. Overview

Dynamic analysis was performed on the Damn Vulnerable Bank (DVBA) Android application to examine runtime behavior, network communication, API security, and WebView functionality.

**Application:** Damn Vulnerable Bank  
**Package:** `com.app.damnvulnerablebank`  
**Testing Device:** Google Pixel 8 Pro (Rooted)  
**Testing Environment:** Mobexler  
**Tools:** Burp Suite, ADB, Frida, Objection

## 2. Environment Setup

- Configured the rooted Android testing device.
- Established ADB connectivity.
- Configured Burp Suite as the device's HTTP proxy.
- Installed and configured Frida Server and Objection.
- Verified application installation and execution.

## 3. Network Traffic Analysis

Used Burp Suite to intercept and inspect application traffic.

Activities:
- Captured HTTP and HTTPS requests.
- Examined API endpoints and request parameters.
- Inspected server responses and HTTP status codes.
- Reviewed application network communication.

## 4. API Security Testing

Tested selected application API functionality, including:

- User authentication.
- Profile information.
- Password-related requests.
- Beneficiary management.
- JWT inspection.

Observed that some API responses returned HTTP 200 while the JSON response contained an application-level error status.

Beneficiary management was also tested by submitting multiple accounts. No enforced maximum limit was observed during testing. Further validation against business requirements is required before classifying this as a vulnerability.

## 5. Custom Encryption Analysis

Identified a custom encoding and obfuscation implementation in the application.

The implementation uses:

- Base64 encoding.
- Repeating-key XOR.
- A hardcoded key within the application.

A Python script was developed to reproduce the encryption and decryption process and generate test payloads.

**Observation:** The implementation provides obfuscation rather than secure encryption.

## 6. WebView and Deep Link Testing

### Affected Component

`com.app.damnvulnerablebank.CurrencyRates`

### Static Analysis Observations

The activity:
- Registers HTTP and HTTPS deep links for `xe.com`.
- Enables JavaScript in the WebView.
- Extracts a URL from the incoming intent.
- Passes the extracted URL directly to `WebView.loadUrl()`.

No URL validation or domain allowlisting was identified in the inspected source code.

### Dynamic Testing

Verified that the activity could be launched externally using an Android VIEW intent.

Tested the following URLs:

| Test | Result |
|---|---|
| `https://example.com` | Successful |
| `http://example.com` | Successful |
| `https://example.org` | Successful |

The application loaded all three external URLs inside its WebView.

### Security Observation

**Potential vulnerability:** Unvalidated Deep Link URL Loading in WebView.

The activity accepts externally supplied URLs without apparent domain restrictions. This could allow an attacker to direct users to an attacker-controlled website inside the application.

Further investigation is required to establish the full security impact and severity.

### Evidence

- <img width="407" height="855" alt="image" src="https://github.com/user-attachments/assets/ca0845a1-3131-4c87-bb73-c2e5c0d86a08" />

- <img width="932" height="375" alt="image" src="https://github.com/user-attachments/assets/59946a68-5511-45be-b9a9-e8829ce578d8" />

- <img width="935" height="462" alt="image" src="https://github.com/user-attachments/assets/98e59cb3-9287-440a-a72e-78e082f9522c" />
- <img width="938" height="402" alt="Screenshot 2026-11-22 132219" src="https://github.com/user-attachments/assets/728a7a13-ce7f-458c-a5b0-6dcc0d66b4c4" />
- <img width="942" height="606" alt="Screenshot 2026-11-22 132136" src="https://github.com/user-attachments/assets/a7da5cda-668f-41ce-9713-9526aa098f9a" />



## 7. Current Findings and Observations

| Area | Observation | Status |
|---|---|---|
| Network Traffic | Application requests intercepted | Completed |
| API Testing | Selected API functionality examined | Completed |
| JWT | Token structure inspected | Completed |
| Custom Encryption | Base64 and XOR implementation identified | Completed |
| Beneficiary Management | Multiple accounts submitted | Tested |
| WebView Deep Link | External URL loading confirmed | Confirmed |




## 8. Conclusion

Dynamic analysis has provided insight into the application's runtime behavior, network communication, API functionality, custom encryption implementation, and WebView deep-link handling.

An unvalidated deep-link URL loading issue has been confirmed and documented for further security assessment.
