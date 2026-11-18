# Static Analysis Report – TrainingApp

## 1. Assessment Overview

| Item | Details |
|---|---|
| Application | TrainingApp |
| Package Name | `com.ecardsandkeys` |
| Assessment Type | Android Static Analysis |
| Analysis Tool | JADX |
| Status | Completed – Preliminary Review |

## 2. Objectives

- Inspect the Android application structure and source code.
- Review application permissions and manifest configurations.
- Identify potential security weaknesses.
- Examine WebView and deep-link implementation.

## 3. Methodology

Static analysis was performed by decompiling the APK using JADX and reviewing the following components:

- `AndroidManifest.xml`
- `WebviewActivity.java`
- `activity_webview.xml`

## 4. Security Observations

### 4.1 Application Debugging Enabled

**Evidence:**
```xml
android:debuggable="true"
```

**Observation:** Debugging is enabled in the application manifest.

**Potential Risk:** May expose application internals and facilitate debugging or runtime inspection.

**Recommendation:** Disable debugging in production builds.

### 4.2 Application Backup Enabled

**Evidence:**
```xml
android:allowBackup="true"
```

**Observation:** Application backup is enabled.

**Potential Risk:** Application data may be exposed through accessible backup mechanisms, depending on Android version and backup configuration.

**Recommendation:** Review backup requirements and disable backups if they are not necessary.

### 4.3 Cleartext Traffic Allowed

**Evidence:**
```xml
android:usesCleartextTraffic="true"
```

**Observation:** The application permits cleartext network traffic.

**Potential Risk:** Sensitive information transmitted over HTTP may be exposed to interception.

**Recommendation:** Enforce HTTPS and disable cleartext traffic.

### 4.4 WebView JavaScript Enabled

**Evidence:**
```java
webSettings.setJavaScriptEnabled(true);
```

**Observation:** JavaScript execution is enabled in the application's WebView.

**Potential Risk:** Unsafe URL handling or untrusted content could increase the risk of WebView-based attacks.

**Recommendation:** Enable JavaScript only when required and restrict WebView content to trusted sources.

### 4.5 Potentially Unvalidated WebView URLs

**Evidence:**
```java
String url = data.getQueryParameter("link");
webview.loadUrl(url);
```

**Observation:** A URL is extracted from a deep-link parameter and passed to `loadUrl()` without visible URL allowlist validation in the reviewed method.

**Potential Risk:** An attacker may attempt to supply an untrusted URL if the deep-link functionality is externally accessible and enabled.

**Recommendation:** Validate URL schemes, hosts, and destinations against a strict allowlist.

### 4.6 SSL Certificate Error Handling

**Evidence:**
```java
handler.proceed();
```

**Observation:** The application provides an option to continue when an SSL certificate error occurs.

**Potential Risk:** Users may proceed to websites with invalid or untrusted certificates.

**Recommendation:** Cancel SSL-error connections instead of allowing users to bypass certificate validation.

### 4.7 Custom Deep Link

**Evidence:**
```xml
<data
    android:scheme="eck"
    android:host="trainingapp.com"/>
```

**Observation:** The application registers a custom deep-link scheme.

**Potential Risk:** Improper input validation or insecure intent handling may expose application functionality.

**Recommendation:** Validate incoming intents and restrict accepted parameters and destinations.

## 5. Additional Configuration Observations

| Configuration | Value |
|---|---|
| Minimum SDK | 16 |
| Target SDK | 29 |
| Compile SDK | 29 |
| Internet Permission | Declared |
| Network State Permission | Declared |

The minimum and target SDK versions should be reviewed against current Android security requirements.

## 6. Evidence

Screenshots and supporting evidence will be added during the assessment.

- [ ] AndroidManifest.xml
- [ ] JADX source code review
- [ ] WebView implementation
- [ ] Deep-link configuration
- [ ] Dynamic testing results

## 7. Conclusion

The static analysis identified several security-relevant configurations and implementation patterns requiring further investigation.

These observations are preliminary and have not yet been confirmed as exploitable vulnerabilities.

## 8. Next Steps

- Complete the remaining source-code review.
- Investigate deep-link preference handling.
- Perform dynamic analysis using Burp Suite.
- Inspect WebView behavior and URL validation.
- Validate findings and document reproducible evidence.
