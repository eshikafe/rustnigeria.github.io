layout: post
title: "Generate a Blockchain Key Pair Address in Rust"
date: 2021-12-16 16:00:00 -0000
categories: Cryptography Blockchain

# Generate a Blockchain Key Pair Address in Rust

`Rust Nigeria Newsletter // December 15, 2021 // Boluwatife Ayodele`

###### tags: `Newsletter: Tutorial` `Blockchain` `Cryptography` `Bitcoin`

Hi, I'm Boluwatife Ayodele, a software engineer who loves Rust and blockchain development. You can reach out to me on [Twitter](https://twitter.com/yyceethetechiee), [LinkedIn](https://www.linkedin.com/in/boluwatife-ayodele-g/) Or [Github](https://github.com/YceeTheTECHie).

## A Brief Explanation

In this tutorial snippet, two crates were used namely: [Secp256k1](https://docs.rs/secp256k1/latest/secp256k1/) and [anyhow](https://crates.io/crates/anyhow).

`Secp256k1` is a Rust implementation of [the Pieter Wuille’s secp256k1 eliptic curve](https://github.com/sipa/secp256k1). The bitcoin network uses this eliptic curve for its public key generation algorithm too.

The `anyhow` crate is used for handling errors graciously in Rust.

## Code Snippet

```=rust=
use anyhow::Result;
use secp256k1::{
    rand::{rngs, SeedableRng},
    PublicKey, SecretKey,
};

pub fn create_keypair() -> Result<(SecretKey, PublicKey)> {
    let secp = secp256k1::Secp256k1::new();
    let mut rng = rngs::StdRng::seed_from_u64(6);
    Ok(secp.generate_keypair(&mut rng))
}

fn main() -> Result<()> {
    let keypair = create_keypair();
    println!("{:?}", keypair);
    Ok(())
}

// Ok((SecretKey(41455c67b47796b2201ae40ea891faee91131f5d8789160e22127af6215dc1f6),
// PublicKey(a648d2691a92fbb2cc37b4571fea0323f19765b74128d401869fd338f9767546f757b952ca5719858919c0bc598a014122ecf2dcba3199b404beba0dd59391f8)))

```

First, we declare a public function named `create_keypair()` which returns a public key and private (secret) key pair. We then initiate the `secp256k1` crate. On line 9 we used the random number generator `rng` on the `secp256k1` crate to generate a secure private key. On line 10, we generated the key-pairs by invoking the `generate_keypair` method which takes a rng from line 9.

The main function just makes a call to the `create_keypair()` function, and then prints the output.

Note: As you change the integer in `seed_from_u64`, you get a different set of private and public keys.

## Conclusion

To run this code, add the following lines to your `Cargo.toml` file

```=toml
[dependencies]

secp256k1 = {version = "0.20.3", features = ["rand"]}
anyhow = "1.0.47"
```

Open your terminal then execute `cargo run`.
