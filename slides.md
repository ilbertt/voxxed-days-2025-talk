---
theme: default
title: Building Full-Stack, Secure, and Scalable Applications Without the Infrastructure Headache
author: Luca Bertelli
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-up
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
colorSchema: light
fonts:
  # basically the text
  sans: Robot
  # use with `font-serif` css class from UnoCSS
  serif: Robot Slab
  # for code blocks, inline code, etc.
  mono: Fira Code
download: true
---

# Building Full-Stack, Secure, and Scalable Applications Without the Infrastructure Headache

Luca Bertelli - ilbert

<img src="/ic-logo.png" class="h-6 absolute bottom-5 left-5" />

<style>
.slidev-layout {
  background: rgb(106,133,241);
  background: linear-gradient(90deg, rgba(106,133,241,1) 0%, rgba(197,114,239,1) 100%);
  color: #fff;
}
h1 {
  background-color: unset;
  background-image: unset;
  -webkit-background-clip: unset;
  -moz-background-clip: unset;
  -webkit-text-fill-color: currentColor;
  -moz-text-fill-color: currentColor;
}
</style>

---

# Who is ilbert?

## Freelance full-stack software developer, blockchain enthusiast.

<br>

Main focus:

- **Full-stack applications** - using Node.js, Rust, Python, JavaScript (React)
- **ICP Community** - publishing examples and libraries
- **CodeGov** - decentralizing ICP governance

<br>
<br>

[github.com/ilbertt](https://github.com/ilbertt)

---
transition: fade
---

# Common Developer Challenges

Imagine you're building a full-stack app with a small team...

<div v-click class="w-full flex items-center justify-center">
  <img
    src="/traditional-full-stack-app-empty.png"
    class="w-5/12 aspect-square mt-2"
  />
</div>

---

# Common Developer Challenges

Imagine you're building a full-stack app with a small team...

<div class="w-full flex items-center justify-center">
  <img
    src="/traditional-full-stack-app.png"
    class="w-5/12 aspect-square mt-2"
  />
</div>

---
layout: two-cols-header
class: "[&_ul]:mt-3"
---

# Building a Full-Stack App

Imagine you're building a full-stack app with a small team...

::left::

<div v-click>

## Specs

<span class="text-2xl">Point of Sale (POS) app for local businesses</span>

</div>

::right::

<div v-click>

## Requirements

- Login with privacy
- Multi-chain crypto payments
- No wallet extensions

</div>

---

# Where do we suffer together?

How hard is it to build a POS app

<br>
<br>

<v-clicks>

- Authentication
- Integrations
- Infrastructure management

</v-clicks>

<img
  v-click
  src="/traditional-full-stack-app.png"
  class="w-1/3 aspect-square mt-2 absolute right-20 top-1/2 -translate-y-1/2"
/>

---
transition: fade
---

# Suffer no more!

There's a solution for every challenge

<div v-click class="w-[250px] h-[250px] side-image-container absolute left-20 top-40">
  <img
    src="/internet-identity.webp"
    class="!h-[calc(100%+4px)] -mt-1"
  />
</div>

<div v-click class="w-[300px] h-[220px] side-image-container absolute right-20 top-28">
  <img
    src="/chain-key-cryptography.webp"
    class="!h-[calc(100%+4px)] -mt-1"
  />
</div>

<div v-click class="w-[300px] h-[200px] side-image-container absolute left-1/2 -translate-x-1/2 bottom-20">
  <img src="/canisters.webp" />
</div>

<div v-after class="absolute left-0 bottom-8 text-center w-full">

### An astronaut, a key and a bucket walk into a bar...

</div>

---
layout: two-cols-header
class: "[&_h1]:text-2xl [&_h1]:mb-3"
---

# Suffer no more!

Key ingredients

<br>
<br>

::left::

<div class="relative">

- Authentication
- Integrations
- Infrastructure management

<mdi-arrow-right-thin class="absolute size-8 right-0 top-1/2 -translate-y-1/2 mt-1" />

</div>

::right::

<div class="mt-1 [&_svg]:text-[#c572ef]">
  <h1>Internet Identity <mdi-robot /></h1>
  <h1>Chain-Key cryptography <mdi-key-variant /></h1>
  <h1>Canisters <mdi-pail /></h1>
</div>

---
transition: fade
layout: two-cols-header
---

# Authenticating the user - Internet Identity

Let's integrate authentication in our app!

::left::

<div v-click>

- Passwordless authentication
- Privacy preserving
- Multi device

</div>

::right::

<div v-after class="w-[300px] h-[300px] side-image-container">
  <img
    src="/internet-identity.webp"
    class="!h-[calc(100%+4px)] -mt-1"
  />
</div>

---
layout: two-cols-header
class: "[&_h3]:text-center [&_h3]:mb-4"
---

# Authenticating the user - Internet Identity

Show me the code

::left::

### Frontend

```ts
import { AuthClient } from "@dfinity/auth-client";

const authClient = await AuthClient.create();

authClient.login({
  identityProvider: "https://identity.ic0.app/",
  // ...
});

backend.update_user("blabla");
```

::right::

<div v-click>

### Backend

```rust
use ic_cdk::{update, caller};

#[update]
fn update_user(input: String) {
  let calling_principal = caller();

  // your permissions logic

  // your business logic
}
```

</div>

---
transition: fade
layout: two-cols-header
---

# Managing Payments - Chain-Key Cryptography

Handle multiple crypto currencies in a secure way

::left::

<div v-click>

- Threshold signatures (34 nodes)
- Derive one key per user
- Multi-chain interaction

</div>

::right::

<div v-after class="w-[450px] h-[230px] side-image-container">
  <img
    src="/chain-key-cryptography.webp"
    class="!h-[calc(100%+4px)] -mt-1"
  />
</div>

---
layout: two-cols-header
class: "-translate-y-10 [&_h3]:text-center [&_h3]:mb-4"
---

# Managing Payments - Chain-Key Cryptography

Show me the code

::left::

### Backend

```rust {all|10|14|all}
use ic_cdk::{update, caller};
use ic_cdk::api::management_canister::ecdsa::{
  sign_with_ecdsa, SignWithEcdsaArgument,
};

#[update]
async fn sign(message: String) {
  let request = SignWithEcdsaArgument {
    message_hash: sha256(&message).to_vec(),
    derivation_path: caller(), // <- (non-)custodial wallet
    // ...
  };

  let (response,) = sign_with_ecdsa(request).await;

  // your business logic
}
```

::right::

<div v-click>

### Frontend

```ts
const transactionData = { /* ... */ };
backend.sign(transactionData);
```

</div>

---
layout: two-cols-header
---

# Managing Infrastructure - Canisters

Keep the infrastructure up and running

::left::

- Stateful serverless
- Interoperable
- Certified data

::right::

<div v-after class="w-[450px] h-[250px] side-image-container">
  <img src="/canisters.webp" />
</div>

---
class: "[&_h2]:text-center [&_h2]:text-5xl"
---

# Managing Infrastructure

Keep the infrastructure up and running

<div v-click class="absolute w-full left-0 top-1/2 -translate-y-1/2 text-center">

## Forget about infrastructure :))

</div>

---
transition: fade
---

# The Internet Computer

Building on the shoulders of giants

<img src="/icp.png" />

---

# The Internet Computer

37 subnets, 1300+ nodes

<img src="/icp-dashboard.png" />

<div class="text-center">

[dashboard.internetcomputer.org](https://dashboard.internetcomputer.org/)

</div>

---
transition: fade
layout: center
class: text-center
---

# Let's try it out now!

<img src="/qr-identity.png" class="qr-code-image" />

<br>

[Internet Identity](https://identity.ic0.app/)

---
transition: fade
layout: center
class: text-center
---

# Let's try it out now!

<img src="/qr-oisy.png" class="qr-code-image" />

<br>

[Oisy](https://oisy.com)

---
layout: center
class: text-center
---

# Let's try it out now!

<img src="/qr-openchat.png" class="qr-code-image" />

<br>

[OpenChat group](https://oc.app/group/tk4yx-liaaa-aaaac-agqwq-cai/?ref=23jsk-vqaaa-aaaar-acx3q-cai)

---
layout: fact
---

# Questions?

---
layout: center
class: text-center
---

# Can I have the slides?

<img src="/qr-slides.png" class="qr-code-image" />

<br>

[Source code](https://github.com/ilbertt/voxxed-days-2025-talk)

<PoweredBySlidev mt-4 />
