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

- **Full-stack applications** - using Node.js, Rust, Python, JavaScript, React
- **ICP Community** - publishing examples and libraries
- **CodeGov** - decentralizing ICP governance

<br>
<br>

[github.com/ilbertt](https://github.com/ilbertt)

---

# Common Developer Challenges

Imagine you're building a full-stack app with a small team...

<div v-click class="w-full flex items-center justify-center">
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
- Payment processing
- ~1000 tx/s

</div>

---

# Where do we suffer together?

The main pain points of this POS app

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
class: "[&_li]:text-3xl [&_li]:mb-8"
---

# Pain points: Authentication

<br>
<br>
<br>

- Authentication providers
- Permissions
- Modularity

<figure class="absolute w-2/5 right-10 top-1/2 -translate-y-1/2 [&>figcaption]:text-[0.5rem] [&>figcaption]:text-center [&>figcaption]:opacity-50">
  <br>
  <br>
  <br>
  <img src="/auth-pain.png" class="w-full" />
  <figcaption>Security Issues and Future Challenges of Cloud Service Authentication - Scientific Figure on ResearchGate. Available from: <a href="https://www.researchgate.net/figure/Authentication-architecture-and-strategies_fig1_317213681" target="_blank">https://www.researchgate.net/figure/Authentication-architecture-and-strategies_fig1_317213681</a> [accessed 16 Jan 2025]</figcaption>
</figure>

---
transition: fade
---

# Where do we suffer together?

<br>
<br>

## Integrations

<img src="/traditional-full-stack-app.png" class="absolute w-5/12 right-10 top-1/2 -translate-y-1/2">

---
transition: fade
---

# Where do we suffer together?

<br>
<br>

## · Infrastructure management

<img src="/traditional-full-stack-app.png" class="absolute w-5/12 right-10 top-1/2 -translate-y-1/2">

---

# Authenticating the user

Let's integrate authentication in our app!

<div class="grid cols-2 mt-16 gap-x-16 gap-y-2 items-center [&>h3]:text-center">

### Frontend

### Backend

```ts
import { AuthClient } from "@dfinity/auth-client";

const authClient = await AuthClient.create();

authClient.login({
  identityProvider: "https://identity.ic0.app/",
  // ...
});

backend.update_user("blabla");
```

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
layout: fact
---

# Questions?

---
layout: center
class: text-center
---

# Can I have the slides?

<br>

<img src="/qr-slides.png" class="w-1/3 mx-auto" />

[kdn3b-iqaaa-aaaao-a3yqq-cai.icp0.io](https://kdn3b-iqaaa-aaaao-a3yqq-cai.icp0.io/)

<PoweredBySlidev mt-10 />
