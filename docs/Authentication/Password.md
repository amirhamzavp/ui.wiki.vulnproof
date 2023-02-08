---
hide:
    - footer
---

# Password Authentication

This checklist is designed to ensure the security of passwords. It includes a series of steps and best practices for protecting user passwords and preventing unauthorized access to user accounts.

## 🍎 General Password Policies

| #️⃣  | ✅Items                                                                                                                                                                                                                                                      |                                          ⚠️Severity                                          |        🗡️Attacks         |                       🔗Sources                       |
| :-: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------: | :----------------------: | :---------------------------------------------------: |
|  1  | **<ins>Verify</ins>:** All authentication-related events must be logged, such as account lockout, account creation, account login, etc. </br> **<ins>Reason</ins>:** Helps in detecting and investigating security incidences                                |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |  `Insufficient Logging`  |                      [ACS](#ACS)                      |
|  2  | **<ins>Verify</ins>:** All user-supplied input i.e. passwords, usernames, PINs etc., should never be trusted and must be validated </br> **<ins>Reason</ins>:** Protect against injection or denial of service attacks                                       |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |       `Injection`        |                      [ACS](#ACS)                      |
|  3  | **<ins>Verify</ins>:** TLS (HTTPS) and `Strict-Transport-Security` header is enable for every authentication process </br> **<ins>Reason</ins>:** Network traffic is encrypted which helps prevent eavesdropping                                             |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |     `Eavesdropping`      |         [ACS](#ACS), [SP800-63B](#SP800-63B)          |
|  4  | **<ins>Verify</ins>:** Rate limiting mechanisms exist </br> **<ins>Reason</ins>:** Prevention against guessing and denial of service                                                                                                                         |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |  `Bruteforcing`, `DoS`   |                [SP800-63B](#SP800-63B)                |
|  5  | **<ins>Verify</ins>:** Password expiration is in place </br> **<ins>Reason</ins>:** Incase password leaks it is not active forever                                                                                                                           | <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px;">Medium </span> | `Impersonation`, `Theft` |         [ACS](#ACS), [SP800-63B](#SP800-63B)          |
|  6  | **<ins>Verify</ins>:** The application requires the user to reauthenticate for sensitive features such as payment, updating password or email etc.</br> **<ins>Reason</ins>:** Ensures that request is coming from the intended user                         |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |     `Impersonation`      |         [ACS](#ACS), [SP800-63B](#SP800-63B)          |
|  7  | **<ins>Verify</ins>:** User has the option to set a second or multi-factor authentication </br> **<ins>Reason</ins>:** Password leak won't have any impact because the second factor is still not compromised                                                |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   | `Impersonation`, `Theft` | [PSCS](#PSCS), [ASVS](#ASVS), [SP800-63B](#SP800-63B) |
|  8  | **<ins>Verify</ins>:** Re-authentication takes place after a period of inactivity </br> **<ins>Reason</ins>:** This helps to prevent unauthorized access to user accounts and sensitive information, even if a user's device or session has been compromised |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |     `Impersonation`      |         [ACS](#ACS), [SP800-63B](#SP800-63B)          |

## 🔨 Password Registration

| #️⃣  | ✅Items                                                                                                                                                                                                               |                                          ⚠️Severity                                           |                         🗡️Attacks                          |                      🔗Sources                      |
| :-: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------: | :--------------------------------------------------------: | :-------------------------------------------------: |
|  1  | **<ins>Verify</ins>:** A password is at least 8 characters in length </br> **<ins>Reason</ins>:** Protect against guessing since shorter passwords can be guessed                                                     |   <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   | `Bruteforcing` <span style="opacity:0">`xxxxxxxxxxx`</div> |       [ACS](#ACS), [NISP800-63B](#SP800-63B)        |
|  2  | **<ins>Verify</ins>:** A password's maximum length is at least 64 characters </br>**<ins>Reason</ins>:** Protect against password length DoS attacks                                                                  |  <span style="background-color:#6e9642; border-radius: 3px; padding: 2px 3px; ">Low </span>   |                           `DoS`                            | [ACS](#ACS), [ASVS](#ASVS), [SP800-63B](#SP800-63B) |
|  3  | **<ins>Verify</ins>:** All ASCII characters, Unicode, and white spaces are considered valid input </br> **<ins>Reason</ins>:** Allow users to create a complex password which will make it hard to guess              | <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px; ">Medium </span> |                       `Bruteforcing`                       |               [SP800-63B](#SP800-63B)               |
|  4  | **<ins>Verify</ins>:** Common or previously breached passwords are blocked </br>**<ins>Reason</ins>:** Protect against password guessing                                                                              | <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px; ">Medium </span> |                       `Bruteforcing`                       | [ACS](#ACS), [ASVS](#ASVS), [SP800-63B](#SP800-63B) |
|  5  | **<ins>Verify</ins>:** Reuse of old passwords is not allowed </br> **<ins>Reason</ins>:** Users are likely to use the same password across many websites, which can be a risk if one of those websites is compromised |  <span style="background-color:#6e9642; border-radius: 3px; padding: 2px 3px; ">Low </span>   |                       `Bruteforcing`                       |                         ⛔                          |
|  6  | **<ins>Verify</ins>:** The user is not asked to set password hints</br> **<ins>Reason</ins>:** Reveals information about the password, which makes it easier to guess                                                 |   <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |                       `Bruteforcing`                       |       [ASVS](#ASVS), [SP800-63B](#SP800-63B)        |
|  7  | **<ins>Verify</ins>:** The user is notified of an account set up via email </br> **<ins>Reason</ins>:** The user is aware of the use of their email on an external website                                            | <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px; ">Medium </span> |                      `Impersonation`                       |       [ASVS](#ASVS), [SP800-63B](#SP800-63B)        |

## 🚦Password Verification

| #️⃣  | ✅Items                                                                                                                                                                                                                                                                                      |                                              ⚠️Severity                                              |                        🗡️Attacks                        |                      🔗Sources                      |
| :-: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------: | :-----------------------------------------------------: | :-------------------------------------------------: |
|  1  | **<ins>Verify</ins>:** If account lockout is in place for the provided email, authentication process should not even start </br> **<ins>Reason</ins>:** Response time delays during authentication can reveal if an account exists in the database or not. This is also a waste of resources |    <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px; ">Medium </span>     | `Bruteforcing` <span style="opacity:0">`xxxxxxxx`</div> |                         ⛔                          |
|  2  | **<ins>Verify</ins>:** Error responses for failed login attempts are generic such as: <em>username or password is incorrect</em> </br> **<ins>Reason</ins>:** Too specific error messages can reveal information about the user's account                                                    |    <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px; ">Medium </span>     |                     `Bruteforcing`                      |                     [ACS](#ACS)                     |
|  3  | **<ins>Verify</ins>:** Response time for username and password checks during authentication should be the same </br> **<ins>Reason</ins>:** The difference in response time can indicate if credentials was found in the database or not                                                     |    <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px; ">Medium </span>     |                     `Bruteforcing`                      |                     [ACS](#ACS)                     |
|  4  | **<ins>Verify</ins>:** HTTP status codes during authentication are generic </br> **<ins>Reason</ins>:** Too specific error messages can reveal information about the user's account                                                                                                          | <span style="background-color:#4097c2; border-radius: 3px; padding: 2px 3px; ">Informational </span> |                     `Bruteforcing`                      |                     [ACS](#ACS)                     |
|  5  | **<ins>Verify</ins>:** The `secure` flag is set for all authentication cookies </br> **<ins>Reason</ins>:** The authentication cookie value is encrypted                                                                                                                                     |      <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>       |                 `Eavesdropping`, `XSS`                  |        [ACS](#ACS), [SP800-63B](#SP800-63B)         |
|  6  | **<ins>Verify</ins>:** Sensitive cookie data that is related to authentication is not being cached </br> **<ins>Reason</ins>:** Someone else can have access in case a device is left unattended or it gets stolen                                                                           |      <span style="background-color:#6e9642; border-radius: 3px; padding: 2px 3px; ">Low </span>      |                `Impersonation`, `Theft`                 | [ACS](#ACS), [ASVS](#ASVS), [SP800-63B](#SP800-63B) |
|  7  | **<ins>Verify</ins>:** An account is locked after a certain number of failed attempts </br> **<ins>Reason</ins>:** Rate limiting mechanism to prevent guessing                                                                                                                               |      <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>       |                     `Bruteforcing`                      |             [ACS](#ACS), [ASVS](#ASVS)              |
|  8  | **<ins>Verify</ins>:** The user is notified via email when an account lockout takes place </br> **<ins>Reason</ins>:** The user must be aware if someone tried to guess their account so they can change their password                                                                      |      <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>       |                     `Bruteforcing`                      |                         ⛔                          |
|  9  | **<ins>Verify</ins>:** Account lockout is not for a fixed time rather, it should increase exponentially with each failed login attempt </br> **<ins>Reason</ins>:** Rate limiting mechanism that makes it challenging for guessing attacks to occur                                          |    <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px; ">Medium </span>     |                     `Bruteforcing`                      |        [ACS](#ACS), [SP800-63B](#SP800-63B)         |
| 10  | **<ins>Verify</ins>:** The user is sent an email notification if login occurs from a different browser, device, IP, or geo-location </br> **<ins>Reason</ins>:** In case someone else logged into the user's account without their consent                                                   |      <span style="background-color:#6e9642; border-radius: 3px; padding: 2px 3px; ">Low </span>      |                     `Impersonation`                     |                     [ACS](#ACS)                     |

## 📦 Password Storage

| #️⃣  | ✅Items                                                                                                                                                                                                                            |                                        ⚠️Severity                                         |          🗡️Attacks          |                       🔗Sources                       |
| :-: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------: | :-------------------------: | :---------------------------------------------------: |
|  1  | **<ins>Verify</ins>:** Passwords are hashed before storing in the database </br> **<ins>Reason</ins>:** In case of a password leak, the hashed passwords won't allow access to an account                                          | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> | `Injection` `Impersonation` | [PSCS](#PSCS), [ASVS](#ASVS), [SP800-63B](#SP800-63B) |
|  2  | **<ins>Verify</ins>:** Only approved hashing algorithms are used </br> **<ins>Reason</ins>:** Unapproved hashing algorithms are insecure since they can be bypassed and clear text values can be extracted                         | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> |       `Bruteforcing`        | [PSCS](#PSCS), [ASVS](#ASVS), [SP800-63B](#SP800-63B) |
|  3  | **<ins>Verify</ins>:** Salt is used before hashing passwords </br> **<ins>Reason</ins>:** Makes passwords even more complex by adding additional characters to it. Also helps make same passwords used by multiple users different | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> |       `Bruteforcing`        | [PSCS](#PSCS), [ASVS](#ASVS), [SP800-63B](#SP800-63B) |
|  4  | **<ins>Verify</ins>:** Salt is at least 32 bits in size </br> **<ins>Reason</ins>:** Makes it challenging to be guessed                                                                                                            | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> |       `Bruteforcing`        | [PSCS](#PSCS), [ASVS](#ASVS), [SP800-63B](#SP800-63B) |
|  5  | **<ins>Verify</ins>:** Salt is unique for each password </br> **<ins>Reason</ins>:** When two users choose the same password, their hash won't be the same as each password is appended to a unique salt                           | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> |       `Bruteforcing`        | [PSCS](#PSCS), [ASVS](#ASVS), [SP800-63B](#SP800-63B) |
|  6  | **<ins>Verify</ins>:** Salt is generated by using secure random algorithms </br> **<ins>Reason</ins>:** Makes it hard to predict the value of the hash                                                                             | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> |       `Bruteforcing`        | [PSCS](#PSCS), [ASVS](#ASVS), [SP800-63B](#SP800-63B) |
|  7  | **<ins>Verify</ins>:** Peppering can be used in addition to salting </br> **<ins>Reason</ins>:** Adds additional security to the passwords. Preferred for sensitive accounts                                                       | <span style="background-color:#6e9642; border-radius: 3px; padding: 2px 3px;">Low </span> |       `Bruteforcing`        |                    [OPSCS](#PSCS)                     |
|  8  | **<ins>Verify</ins>:** If peppering is used, it is stored in a password vault </br> **<ins>Reason</ins>:** More secure than storing in the database                                                                                | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> |       `Bruteforcing`        |                    [OPSCS](#PSCS)                     |
|  9  | **<ins>Verify</ins>:** Pepper rotation policy is in place </br> **<ins>Reason</ins>:** In case of a leak, rotation policy will invalidate the older pepper                                                                         | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> |   `Bruteforcing`, `Theft`   |                    [OPSCS](#PSCS)                     |
| 10  | **<ins>Verify</ins>:** Pepper is produced by using secure random algorithms </br> **<ins>Reason</ins>:** Makes it challenging to guess the value                                                                                   | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> |       `Bruteforcing`        |                    [OPSCS](#PSCS)                     |

## 🔃 Password Reset

| #️⃣  | ✅Items                                                                                                                                                                                                                 |                                          ⚠️Severity                                           |                        🗡️Attacks                         |              🔗Sources               |
| :-: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------: | :------------------------------------------------------: | :----------------------------------: |
|  1  | **<ins>Verify</ins>:** The user is required to reauthenticate before a password reset </br> **<ins>Reason</ins>:** Ensures that the actual user is making a change, not someone else                                    |   <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   | `Impersonation` <span style="opacity:0">`xxxxxxxx`</div> | [ACS](#ACS), [SP800-63B](#SP800-63B) |
|  2  | **<ins>Verify</ins>:** The user is required to type the new password twice </br> **<ins>Reason</ins>:** Helps prevent typing mistakes mistakes                                                                          | <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px; ">Medium </span> |                            ⛔                            |       [SP800-63B](#SP800-63B)        |
|  3  | **<ins>Verify</ins>:** Email notification is sent to this user when a password change is successful </br> **<ins>Reason</ins>:** Incase the user did not authorize a password change, they should know someone else did | <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px; ">Medium </span> |                     `Impersonation`                      | [ACS](#ACS), [SP800-63B](#SP800-63B) |

!!! Warning "Continue ..."

     Verify that the new password must follows the [Password Registration](#password-registration) checklist

## 🤔 Forgot Password

When a user chooses forgot password, this can be done in multiple ways:

-   Generate a PIN that can be sent to the user with the provided email or phone number. This PIN needs to be confirmed before a password reset is allowed
-   Create a token and pass it into the query string, create a limited session around that unique URL, and send it to the user's email
-   Recovery/Backup codes can also be used to give access when the user forgets their password

</br>

The following items must be considered for using PINS, URL tokens or Backup Codes.

**PIN**

| #️⃣  | ✅Items                                                                                                                                                                                                                                                                    |                                          ⚠️Severity                                           |                        🗡️Attacks                        |   🔗Sources   |
| :-: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------: | :-----------------------------------------------------: | :-----------: |
|  1  | **<ins>Verify</ins>:** The PIN must be 6 to 12 digits long </br> **<ins>Reason</ins>:** Increase complexity which helps against guessing                                                                                                                                   |   <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   | `Bruteforcing` <span style="opacity:0">`xxxxxxxx`</div> | [FPCS](#FPCS) |
|  2  | **<ins>Verify</ins>:** The PIN is unique and is generated using secure random algorithms </br> **<ins>Reason</ins>:** Provides additional protection against guessing since a truly random value is hard to predict                                                        |   <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |                     `Bruteforcing`                      | [FPCS](#FPCS) |
|  3  | **<ins>Verify</ins>:** The PIN is sent to either email or phone number that the user provided </br> **<ins>Reason</ins>:** The possession of the PIN verifies their identity                                                                                               |   <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |                     `Impersonation`                     | [FPCS](#FPCS) |
|  4  | **<ins>Verify</ins>:** A limited time session is permitted for the PIN until it expires </br> **<ins>Reason</ins>:** In case the PIN leaks through an email/phone compromise, it is no longer active after a few minutes                                                   |   <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |                `Impersonation`, `Theft`                 | [FPCS](#FPCS) |
|  5  | **<ins>Verify</ins>:** Use [Password Storage](#password-storage) policies for hashing the PIN when it's being stored </br> **<ins>Reason</ins>:** Helps against database compromise or PIN leakage                                                                         |   <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |                         `Theft`                         | [FPCS](#FPCS) |
|  6  | **<ins>Verify</ins>:** A generic message is shown if the email provided exists or not such as: "A PIN is sent to the provided email if it exists in the database" </br> **<ins>Reason</ins>:** Too specific error messages can reveal information about the user's account | <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px; ">Medium </span> |                     `Bruteforcing`                      | [FPCS](#FPCS) |
|  7  | **<ins>Verify</ins>:** The PIN is checked for validity before the user can set the set a new password </br> **<ins>Reason</ins>:** The likelihood of a logic error is high when PIN validity check and password reset happen together                                      |   <span style="background-color:#6e9642; border-radius: 3px; padding: 2px 3px;">Low </span>   |             `Logic Error`, `Impersonation`              | [FPCS](#FPCS) |
|  8  | **<ins>Verify</ins>:** The PIN in invalidated once it has been used </br> **<ins>Reason</ins>:** Prevent the reuse of the PIN in case an attacker gets a hold of it                                                                                                        |   <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |                `Impersonation`, `Theft`                 | [FPCS](#FPCS) |

**URL Token**

| #️⃣  | ✅Items                                                                                                                                                                                                                 |                                          ⚠️Severity                                          |                         🗡️Attacks                          |   🔗Sources   |
| :-: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------: | :--------------------------------------------------------: | :-----------: |
|  1  | **<ins>Verify</ins>:** The token is generated using secure random algorithms </br> **<ins>Reason</ins>:** Protection against guessing since a random value is hard to predict                                           |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   | `Bruteforcing` <span style="opacity:0">`xxxxxxxxxxx`</div> | [FPCS](#FPCS) |
|  2  | **<ins>Verify</ins>:** Use [Password Storage](#password-storage) policies for hashing the token when it's being stored </br> **<ins>Reason</ins>:** Helps against database compromise or token leakage                  |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |                          `Theft`                           | [FPCS](#FPCS) |
|  3  | **<ins>Verify</ins>:** URL is hard-coded rather than relying on the host header </br> **<ins>Reason</ins>:** Protection against host header injection                                                                   | <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px;">Medium </span> |                           `HHi`                            | [FPCS](#FPCS) |
|  4  | **<ins>Verify</ins>:** The reset password page uses the Referrer Policy tag with the `noreferrer` value </br> **<ins>Reason</ins>:** Prevention against referrer leakage                                                | <span style="background-color:#ad8c07; border-radius: 3px; padding: 2px 3px;">Medium </span> |                     `Referrer Leakage`                     | [FPCS](#FPCS) |
|  5  | **<ins>Verify</ins>:** A limited session is allowed for the URL token before it expires </br> **<ins>Reason</ins>:** In case the token leaks through an email/phone compromise, is no longer active after a few minutes |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |                  `Impersonation`, `Theft`                  | [FPCS](#FPCS) |
|  6  | **<ins>Verify</ins>:** The token is checked for validity before the user can set the set a new password </br> **<ins>Reason</ins>:** Ensures that the request is coming from the intended user                          |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |                      `Impersonation`                       | [FPCS](#FPCS) |
|  7  | **<ins>Verify</ins>:** The token is invalidated once it has been used </br> **<ins>Reason</ins>:** Prevent the reuse of the token                                                                                       |  <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span>   |                  `Impersonation`, `Theft`                  | [FPCS](#FPCS) |

**Recovery/Backup Code**

Recovery/Backup code security checklist can be viewed [here](./MFA/Authenticator-Types.md#look-up-secrets)

!!! Warning "Continue ..."

    Once the user has been confirmed, then [Password Reset](#password-reset) checklist must be used

## ⚖️ Password Management

| #️⃣  | ✅Items                                                                                                                                                                                                                                                                                                    |                                        ⚠️Severity                                         |        🗡️Attacks        | 🔗Sources |
| :-: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------: | :---------------------: | :-------: |
|     | **<ins>Verify</ins>:** Regularly monitor log activity </br> **<ins>Reason</ins>:** To detect any suspicious activity such as multiple failed login attempts                                                                                                                                                | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> |     `Bruteforcing`      |    ⛔     |
|     | **<ins>Verify</ins>:** Third party software or libraries used for password authentication are updated to the most recent version and are regularly patched </br> **<ins>Reason</ins>:** Vulnerability in a third party resource can grant an attacker unauthorized access                                  | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> | `Vulnerable Dependency` |    ⛔     |
|     | **<ins>Verify</ins>:** Conduct regular security assessments, vulnerability scans, and penetration testing to identify vulnerabilities in custom and third-party code </br> **<ins>Reason</ins>:** Identify any security vulnerabilities that might have appeared in password authentication implementation | <span style="background-color:#de3a3c; border-radius: 3px; padding: 2px 3px">High </span> |  `Unauthorized Access`  |    ⛔     |

**🔗 Sources:**

Open Web Application Security Project (OWASP):

-   <a href="https://github.com/OWASP/ASVS/blob/master/4.0/en/0x11-V2-Authentication.md#v2-authentication" target="_blank" id="ASVS">[ASVS] Application Security Verification Standard - Authentication</a>
-   <a href="https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html" target="_blank" id="ACS">[ACS] Authentication Cheat Sheet</a>
-   <a href="https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html" target="_blank" id="PSCS">[PSCS] Password Storage Cheat Sheet</a>
-   <a href="https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html" target="_blank" id="FPCS">[FPCS] Forgot Password Cheat Sheet</a>

National Institute of Standards and Technology (NIST):

-   <a href="https://pages.nist.gov/800-63-3/sp800-63b.html#-5112-memorized-secret-verifiers" target="_blank" id="SP800-63B">[SP800-63B] 5.1.1.2 Memorized Secret Verifiers</a>