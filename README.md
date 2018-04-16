# GoogleAuthenticator
##Introduction
This Rust crate can be used to interact with the Google Authenticator mobile app for 2-factor-authentication.
This Rust crates can generate secrets, generate codes, validate codes and present a QR-Code for scanning the secret.
It implements TOTP according to RFC6238
More about Google GoogleAuthenticator see:
https://en.wikipedia.org/wiki/Google_Authenticator
[![Build Status](https://travis-ci.org/hanskorg/google-authenticator-rust.svg?branch=master)](https://travis-ci.org/hanskorg/google-authenticator-rust)
![Build Status](https://img.shields.io/crates/v/google-authenticator.svg)
## Usage
Add this to your `Cargo.toml`:

```toml
[dependencies]
google-authenticator = "0.1.4"
```
## Examples
```rust
    use google_authenticator::GoogleAuthenticator;
    let secret = "I3VFM3JKMNDJCDH5BMBEEQAW6KJ6NOE3";
    let auth = GoogleAuthenticator::new();
    //secret = auth.create_secret(32).as_str();
    let code = auth.get_code(secret,0).unwrap();

    if auth.verify_code(secret, code, 1, 0) {
        println!("match!");
    }
```
## Get qrcode for Secret
### get form url
```rust
    let auth = GoogleAuthenticator::new();
    let secret = "I3VFM3JKMNDJCDH5BMBEEQAW6KJ6NOE3";
    auth.qr_code_url(secret,"qr_code","name",200,200,'H'));

```
### *get qrcode for svg*
Change `Cargo.toml` to
```toml
    [dependencies.google-authenticator]
    version = "0.1.4"
    default-features = false
    features = ["with-qrcode"]
```
```rust
    use google_authenticator::GoogleAuthenticator;
    let secret = "I3VFM3JKMNDJCDH5BMBEEQAW6KJ6NOE3";
    let auth = GoogleAuthenticator::new();
    let code = auth.get_code(secret,0).unwrap();

    println!("{}",auth.qr_code(secret,"qr_code","name",200,200,'H')));
```

## FAQ
> You can post a new issue for help.