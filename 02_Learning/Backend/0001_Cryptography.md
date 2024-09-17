---
documentation: https://nodejs.org/api/crypto.html
tags:
  - "#cryptography"
  - "#encryption"
  - "#decryption"
share_link: https://share.note.sx/mtzu073r#PTmbWm4oAaAZy8BR5O38BudAWQx3MJneAIGn2xdDK1A
share_updated: 2024-07-07T23:40:49+05:30
---
# What is cryptography

It is a way to just take a normal string of text there fore converting it to a cypher text with the help of a encryption key. The cyphered text cannot be read by anyone without the help of the correct encryption key.

```text
Text to cypher: "Hello i love my mom"
key: "jkhskjhfgjkhsdgfjkh"

Cyphered text: "hjkdkjhuiybmamn3rerieriuscmdfmsfkjtiuriyu4iyhweihfjkehfhj"
```

For understanding the cryptography we also need to understand the key concepts of cryptography such as **Hash**, **Key**, **Salt**, **Sign**

#### **Difference between hashing and encryption:**
> **Encryption is a two-way function where information is scrambled in such a way that it can be unscrambled later.** **Hashing is a one-way function where data is mapped to a fixed-length value**. Hashing is primarily used for authentication.

# What is HASH

> ***Chop & Mix***
> It takes a input string of any length and returns a cyphered text with a fixed length using various hashing algorithms like **MD5**, **SHA256**, **ARGON2** and many more.
> It will return always the same output if it is provided with the same input

```js
/** 
* How to hash using the native libraries from the node.js
*/
const { createHash } = require("crypto");

function hash(input) {
  return createHash("sha256")
    .update(input.toString())
    .digest("hex"); // can be also base64 which would look like this `.digest("base64")`
}

const hashedPassword = hash("secret-password-1234")
console.log(hashedPassword)
```

![[Pasted image 20240707214720.png]]

## What is SALT

> In cryptography, a salt is **random data fed as an additional input to a one-way function that hashes data, a password or passphrase**. Salting helps defend against attacks that use precomputed tables (e.g. rainbow tables), by vastly growing the size of table needed for a successful attack.

```js
const { randomBytes, scryptSync, timingSafeEqual } = require("crypto");

function generateSalt() {
  return randomBytes(16).toString("hex");
}

function generateHash(password, salt) {
  let hash = scryptSync(password, salt, 64).toString("hex");
  hash = `${salt}:${hash}`; //so that the salt can be retractable for the verification of the hash
  return hash;
}

function verifyHash(password, original) {
  const [salt, originalHash] = original.split(":");
  const originalBuffer = Buffer.from(originalHash, "hex");
  const newBuffer = scryptSync(password, salt, 64)
  
  return timingSafeEqual(newBuffer, originalBuffer); //it is to prevent the timing attack done by the attackers
}

  

const salt = generateSalt();
const hashedPassword = generateHash("secret-password-1234", salt);

console.log(hashedPassword);
/**
* output - 43129647efe8e02be076bc533bbb18a6:f424b6429cf586022a1019ed307a4a6a40201f9094d2c57b8024a7612c6b531c7babb8b1e068de4c9f93680d9395d2a995c517fac7feb55490a6a2b920c83d40
* where the first part before the colon is the salt and the rest is the actual hash
*/
  
  

const isCorrect = verifyHash("secret-password-1234", hashedPassword);
console.log("Is the password correct? - ", isCorrect ? "Yes" : "No");
/**
* Is the password correct? -  Yes
*/
```

> **Foot note:** What is a timing attack? 
> A timing attack is ==a type of side-channel attack in cryptography that attempts to compromise a cryptosystem by analyzing how long it takes to execute cryptographic algorithms==. The attacker gains information that is indirectly leaked by the application, such as response times, power consumption, or acoustic emissions, and uses it for malicious purposes, such as guessing a user's password. 
> ![[Pasted image 20240707220750.png]]


## What is HMAC(Hash-based Message Authentication Code)

> Hash-based message authentication code (or HMAC) is **a cryptographic authentication technique that uses a hash function and a secret key**. With HMAC, you can achieve authentication and verify that data is correct and authentic with shared secrets, as opposed to approaches that use signatures and asymmetric cryptography.
> It can be achieved with the help of libraries like JWT.

```js
const { createHmac } = require("crypto");

const password = "secret-pass-123";
const key = "my-secret";

const hmac = createHmac("sha256", key).update(password).digest("hex");
console.log(hmac)
```

One important thing to notice is if we create two HMAC with the same password but with two different secret keys then the has will be two different hashes.

## What is Symmetric Encryption

> [Symmetric encryption](https://www.cryptomathic.com/news-events/blog/differences-between-hash-functions-symmetric-asymmetric-algorithms) is a type of [encryption key management solution](https://www.cryptomathic.com/products/key-management) where only one key (a secret key) is used to both encrypt and decrypt electronic data. The entities communicating via symmetric encryption must exchange the key so that it can be used in the decryption process. This encryption method differs from asymmetric encryption where a pair of keys - one public and one private - is used to encrypt and decrypt messages.

![[Pasted image 20240707222008.jpg]]

```js
const { createCipheriv, createDecipheriv, randomBytes } = require("crypto");

const message = "Hello World";
const key = randomBytes(32);
const iv = randomBytes(16);

const cipher = createCipheriv("aes256", key, iv)
const encrypted = cipher.update(message, "utf8", "hex") + cipher.final("hex");

console.log("Encrypted: ", encrypted); // Encrypted:  2080c95b309cb8bb840e273a1ea7529e

  
const decipher = createDecipheriv("aes256", key, iv);
const decrypted = decipher.update(encrypted, "hex", "utf8") + decipher.final("utf8");

console.log("Decrypted: ", decrypted); // Decrypted:  Hello World
```

## What is keypairs

It is just a simple pair of keys, one is publicKey which can be shared publicly to anyone on an asymmetric encryption to and the privateKey is for not sharing with everyone.
==Data encrypted with the public key can only be decrypted with the private key. TLS (or SSL), the protocol that makes HTTPS possible, relies partially on asymmetric encryption.==

```js
const { generateKeyPairSync } = require("crypto");

const { privateKey, publicKey } = generateKeyPairSync("rsa", {
  modulusLength: 2048,
  publicKeyEncoding: {
    type: "spki",
    format: "pem"
  },
  privateKeyEncoding: {
    type: "pkcs8",
    format: "pem"
  }
})


console.log("Public key: \n", publicKey);
/** 
* Public key: 
* -----BEGIN PUBLIC KEY-----
* MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAks5713CsZcpc5Bjq1HEe
* g/T7DvBJ7VaL5EO3R4R1WWVTbkMOHPMqa8GuTCCaEy3i49dMZHHDRUe2b4qIrdHA
* itvyU8swF0mtWivNXi6i2NQXh9kucOuykVeshjxAOWKWN5UJ4h+KqCKv8Zr1o/ID
* DLnM1yc31Dz+/xfo0mpSziQVY/fbuRDYpx+YDkRQj4dKq//1bcwEGwMJUx4QtvpJ
* oHEsCPr0kPB+0FrCbnwo5wlESeDFW3lPjCI+0195vXeDtaaByYkQJGc4u933sFkb
* yMEFPRbhcp3wgTSuPYqwdOz2AAV2UHv9E2fCE6OdIVVfHCp5NovuoSb3ocwxEJY3
* awIDAQAB
* -----END PUBLIC KEY-----
*/

console.log("Private key: \n", privateKey);
/** 
* Private key:
*  -----BEGIN PRIVATE KEY-----
* MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCSznvXcKxlylzk
* GOrUcR6D9PsO8EntVovkQ7dHhHVZZVNuQw4c8yprwa5MIJoTLeLj10xkccNFR7Zv
* ioit0cCK2/JTyzAXSa1aK81eLqLY1BeH2S5w67KRV6yGPEA5YpY3lQniH4qoIq/x
* mvWj8gMMuczXJzfUPP7/F+jSalLOJBVj99u5ENinH5gORFCPh0qr//VtzAQbAwlT
* HhC2+kmgcSwI+vSQ8H7QWsJufCjnCURJ4MVbeU+MIj7TX3m9d4O1poHJiRAkZzi7
* 3fewWRvIwQU9FuFynfCBNK49irB07PYABXZQe/0TZ8ITo50hVV8cKnk2i+6hJveh
* zDEQljdrAgMBAAECggEAARj+IAw9nb03mJT/HHuECOSKBACT7Oxau2guNKCu5+40
* A30I2/qNdKTMEtGjlUUgjyeK8K1REnGI0aitgO8yi1c9ppa8U1A/tY7iSDP9D7X2
* PxPGnx2EBkYrig1lRYiRKvU4T7KArOUlf57y+zjSAQRanbkzV6jlFy8slHYrDFOB
* 1zusB6HqwEWuaKDLU+BZPAst9VkbB6Qs+glxgWp6PtECI1oZzakGwrRZ6AeodlK7
* Uci5IApbqIS+C+Zr4m6s6mk3oF3W+NHdMJwrZIZDXQ/BauATsQAbaZMSKPvxR0GW
* qeGfVRWUIbF8PJuR0RDZkjmfSxB5KCBMLPPa7qVXAQKBgQDEoH1YbZtrD000x0bg
* jGsy3umoXQx2iD+4/DNtZg1G2/6p2DdRj5sYdAp2igrxmbAO1O1M2mYYXqe1qo4w
* JsEEcly3x4MCpX5x3NrA8vU0BkgPdahi3qyy/SDYZ3wIfit8UZZ3sGvSgFAs4F/X
* wyKPMY3CfwOuZXmxNw08oywBsW6mSvCJob7RU09FE9CQ+NoDlWDISz7UV0/heX4r
* KIATn48uKwKBgEHCYulWDuppParvEpc6nwduYbq7E9X4j0cwoYpu3PXb0XnAJBAU
* 9QvikzU9yZcvjSAIuiw/xnFUBsbM+azE6TyxeqzD/t69tmIiOM7a8oKpryPsd5pJ
* WnyqB3gYc/TrLWPwbWAuEoFeBHJdv/AXjLtS9NYnJWaKxplfwm7XZ6CBAoGAMU5A
* GSeXemArCrlk9iKSe2b443Wh86c4yIpHFRL8iQe0rCQ6LeF+lpf4wG4r2D11tNBg
* 1WJwAFprWtKIIt07V1+4o0vtu5KzlTT5U0sLMKMnRfOzYr260mudTIqC6q7mQfrR
* iJofFsi3ws4PH2GHZ+PRP2GOn7GBlIyMDYPZoaUCgYEAjehy3o29bJDgUpZ/EMAt
* ARnF190PxGE/Ym7JYs9ERUAz6YmsvzyXoAbPoznQClH3Od3fhjIgF9KFtgxg8hZ0
* CGrK82t+cOnXG1Z69YE1NuAugXIvzHXKPQ7EbMVE/3/Kum+vEY79qrqxEuXdiA6/
* zOBDGExK1V5PaTfDuSduxLE=
* -----END PRIVATE KEY-----
*/
```

## Asymmetric Encryption

Asymmetric encryption, also known as public key encryption, uses a **public key-private key pairing**: data encrypted with the public key can only be decrypted with the private key. TLS (or SSL), the protocol that makes HTTPS possible, relies partially on asymmetric encryption.

```js
const { generateKeyPairSync, privateDecrypt, publicEncrypt } = require("crypto");

const { privateKey, publicKey } = generateKeyPairSync("rsa", {
  modulusLength: 2048,
  publicKeyEncoding: {
    type: "spki",
    format: "pem",
  },
  privateKeyEncoding: {
    type: "pkcs8",
    format: "pem",
  },
});

const message = "Hello world!";

const encrypted = publicEncrypt(
  publicKey,
  Buffer.from(message, "utf8")
).toString("hex");  

console.log("Encrypted: ", encrypted);

const decrypted = privateDecrypt(
  privateKey,
  Buffer.from(encrypted, "hex")
).toString("utf8");

console.log("Decrypted: ", decrypted);
```


## What is signing

Signing of data **works to authenticate the sender of the data and tends to implement a form of encryption in its process**. The process of signing emails, sensitive data, and other information has become necessary, as it verifies the identity of the sender and ensures the data has not been altered in transit.

In cryptography, signing is ==a technique that uses a digital signature algorithm to verify the authenticity of data, such as files, emails, or sensitive information==. Signing ensures that the data is reliable, safe, and hasn't been tampered with.

```js
const { generateKeyPairSync, createSign, createVerify } = require("crypto");
  

const { privateKey, publicKey } = generateKeyPairSync("rsa", {
  modulusLength: 2048,
  publicKeyEncoding: {
    type: "spki",
    format: "pem",
  },
  privateKeyEncoding: {
    type: "pkcs8",
    format: "pem",
  },
});
  
const message = "Hello world!";
const signer = createSign("rsa-sha256");
signer.update(message);
const signature = signer.sign(privateKey, "hex");

console.log("Singature: ", signature);

const verifier = createVerify('rsa-sha256')
verifier.update(message);
const isVerified = verifier.verify(publicKey, signature, "hex");

console.log("Verified signature: ", isVerified ? "Yes" : "No");
```

## Hybrid Encryption

Combining the asymmetric encryption with public and private key with the **AES** encryption makes a more versatile and short encrytped string as compared to the Public and Private key encryption

```js
function encryptData(publicKey, data) {
  const aesKey = crypto.randomBytes(32);
  const iv = crypto.randomBytes(16);
  const cipher = crypto.createCipheriv('aes-256-cbc', aesKey, iv);
  let encryptedData = cipher.update(data, 'utf8', 'base64');

  encryptedData += cipher.final('base64');

  const encryptedAesKey = crypto.publicEncrypt(publicKey, aesKey); 

  return {
    encryptedData,
    encryptedAesKey: encryptedAesKey.toString('base64'),
    iv: iv.toString('base64')
  };
}

const encrypted = encryptData(publicKey, message);


console.log('Encrypted Data:', encrypted.encryptedData);
console.log('Encrypted AES Key:', encrypted.encryptedAesKey);
console.log('Initialization Vector:', encrypted.iv);


function decryptData(privateKey, encryptedData, encryptedAesKey, iv) {
  const aesKey = crypto.privateDecrypt(privateKey, Buffer.from(encryptedAesKey, 'base64'));
  const decipher = crypto.createDecipheriv('aes-256-cbc', aesKey, Buffer.from(iv, 'base64'));
  let decryptedData = decipher.update(encryptedData, 'base64', 'utf8');

  decryptedData += decipher.final('utf8');
  
  return decryptedData;
}

const decrypted = decryptData(privateKey, encrypted.encryptedData, encrypted.encryptedAesKey, encrypted.iv);
console.log('Decrypted Data:', decrypted);
```