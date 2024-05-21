# IronHack-Lab4-AppSecurity - Implementing and Testing Application Security
This lab is designed to deepen participants’ understanding of application security by applying the theoretical knowledge they’ve acquired about SAST, DAST, cryptography, and secure data communications.

## Scenarios for Security Design:

### Scenario 1: Pseudo-Code for Authentication System

#### Pseudo-Code Example:
```
FUNCTION authenticateUser(username, password):
  QUERY database WITH username AND password
  IF found RETURN True
  ELSE RETURN False
```

#### Security Scanning Report: 

##### 1. Cleartext Password Storing
##### Overview
Do not store passwords in cleartext in your database. User databases are routinely hacked, leaked or gleaned through SQL injection, and if you are storing raw, plaintext passwords, that is instant game over for your login security.
##### Remediation
Hashing using a key derivation function, take the password and run it through a KDF, such as Argon2, bcrypt, scrypt or PBKDF2, turning the cleartext password into a long, random-looking string.

##### 2. SQL Injection Attacks
##### Overview
Security vulnerability that allows an attacker to interfere with the queries that an application makes to the database since the query is storing the username and password directly to the database.
##### Remediation
Use of Prepared Statements (with Parameterized Queries)

##### 3. Error Handling
##### Overview
Returning only true or false as a response in the functios could fall into Boolean-based (content-based) Blind SQLi 
##### Remediation
Correct handling of responses and errors

```
FUNCTION authenticateUser(username, password):
  HASH password 
  QUERY database WITH username AND password_hashed
  IF found RETURN success_obj 
  ELSE RETURN error_handling
```

### Scenario 2: JWT Authentication Schema

#### Design Outline

```
DEFINE FUNCTION generateJWT(userCredentials):
  IF validateCredentials(userCredentials):
    SET tokenExpiration = currentTime + 3600 // Token expires in one hour
    RETURN encrypt(userCredentials + tokenExpiration, secretKey)
  ELSE:
    RETURN error
```

#### JWT Authentication Design Document:
The function is missing the Standard JWT Authentication that consists: 
- The header: consists of two parts—the token type, which is JWT, and a signing algorithm, such as HMAC-SHA256 or RSA
- The payload: contains the claims—in other words, the statements about an entity (typically, the user) and additional data
- The signature: used to verify the JWT's integrity
```
DEFINE FUNCTION generateJWT(userCredentials):
  IF validateCredentials(userCredentials):
    SET tokenExpiration = currentTime + 3600 // Token expires in one hour
    RETURN jwt.builder()
            .setSubject(userCredentials.username + tokenExpiration)
            .sign(SignatureAlgorithm.HS256, secretKey);
    ELSE:
      RETURN new BadRequestError("Login error");

```

### Scenario 3: Secure Data Communication Plan

#### Outline for Data Protection:
```
PLAN secureDataCommunication:
  IMPLEMENT SSL/TLS for all data in transit
  USE encrypted storage solutions for data at rest
  ENSURE all data exchanges comply with HTTPS protocols
```

#### Data Protection Strategy Document
```
PLAN secureDataCommunication:
  IMPLEMENT SSL/TLS for all data in transit
  USE encrypted storage solutions for data at rest
  ENSURE all data exchanges comply with HTTPS protocols
```
