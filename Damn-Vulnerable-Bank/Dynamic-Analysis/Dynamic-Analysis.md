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

- Screenshot: `deeplink-evidence.png`
- Static source: `CurrencyRates.java`
- Manifest: `AndroidManifest.xml`

## 7. Current Findings and Observations

| Area | Observation | Status |
|---|---|---|
| Network Traffic | Application requests intercepted | Completed |
| API Testing | Selected API functionality examined | Completed |
| JWT | Token structure inspected | Completed |
| Custom Encryption | Base64 and XOR implementation identified | Completed |
| Beneficiary Management | Multiple accounts submitted | Tested |
| WebView Deep Link | External URL loading confirmed | Confirmed |
| WebView Security | Additional security checks required | In Progress |

## 8. Remaining Activities

- Investigate exported activities and their security implications.
- Continue REST API security testing.
- Investigate sensitive information disclosure.
- Examine WebView security settings and potential attack scenarios.
- Validate potential findings and assess their severity.
- Collect additional screenshots and supporting evidence.

## 9. Conclusion

Dynamic analysis has provided insight into the application's runtime behavior, network communication, API functionality, custom encryption implementation, and WebView deep-link handling.

An unvalidated deep-link URL loading issue has been confirmed and documented for further security assessment.
