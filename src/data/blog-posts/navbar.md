---
title: Navbar
publishDate: 16 Jul 2023
description: A cool responsive navbar  with sveltekit and tailwind.
---

![Illustration of woman using a meditation app](/assets/blog/casual-life-3d-meditation-crystal.webp)

A responsive sidebar

## <a name="top"></a> Table of Contents

- [Intro](#Headings)
- [Setup](#Setup)
- [Pages + basic styling](#Pages)
- [Toggle logic](#Toggle)
- [Responsive CSS](#Responsive)
- [Background image](#Background)

---

# <a name="Intro"></a>Intro

This is a code I stole from Kevin Powell. Here's his navbar [tutorial.](https://youtu.be/HbBMp6yUXO0) He uses vanilla JavaScript and good old pure CSS. I'm using Sveltekit with Tailwind CSS for some parts. Also, this navbar design is inspired by [chanel's website.](https://www.chanel.com/us/) Finally, I'm featuring it on a tarot readings website, [NovaastraCo.](https://novastra.vercel.app) If this doesn't sound odd enough for you, keep reading; otherwise, read on anyway.

# <a name="Setup"></a>Setup

First, we'll create our Navbar component. Also get some svg for the shopping bag/cart, the hamburger and the closing/X icon, and store them in `src/lib/images`

```html
<!-- src/lib/components/Navbar.svelte -->
<script>
  import bag from '$lib/images/shopping-bag.svg'
</script>

<header>
  <div>
    <button />
    <div>
      <a href="/"><h1>NOVAASTRACO</h1></a>
    </div>
    <button><img class="w-5" src="{bag}" alt="shopping bag icon" /></button>
  </div>
  <nav>
    <button />
    <ul>
      <li><a href="/tarot">TAROT</a></li>
      <li>
        <a href="/astrology">ASTROLOGY</a>
      </li>
      <li><a href="/blog">BLOG</a></li>
      <li>
        <a href="/about">ABOUT NOVAASTRACO</a>
      </li>
    </ul>
  </nav>
</header>
```

![Unstyled navbar](/navbar1.png)

# <a name="Pages"></a>Pages + basic styling

Now let's make the pages for every link `src/routes/tarot/+page.svelte` And We'll add some basic styling with CSS and tailwind

```html
<script>
  import bag from '$lib/images/shopping-bag.svg'
</script>

<header class="p-4 border-b">
  <div class="flex justify-between items-center">
    <button class="burger bg-no-repeat bg-center w-5 aspect-square" />
    <div class="flex justify-center w-full">
      <a href="/" class="font-bold text-xl tracking-widest"
        ><h1>NOVAASTRACO</h1></a
      >
    </div>
    <button><img class="w-5" src="{bag}" alt="shopping bag icon" /></button>
  </div>
  <nav>
    <button
      class="absolute right-4 top-4 bg-no-repeat bg-center w-6 aspect-square"
    />
    <ul class="font-semibold">
      <li><a href="/tarot">TAROT</a></li>
      <li>
        <a href="/astrology">ASTROLOGY</a>
      </li>
      <li><a class="mr-8" href="/blog">BLOG</a></li>
      <li>
        <a href="/about">ABOUT NOVAASTRACO</a>
      </li>
    </ul>
  </nav>
</header>

<style>
  .burger {
    background-image: url(../images/burguesa.svg);
  }

  nav button {
    background-image: url(../images/icon-close.svg);
  }
</style>
```

![navbar with basic css styling](/navbar2.png)

# <a name="Toggle"></a>Toggle logic

Now let's make the toggle logic for the burger and X buttons, and also for the nav tag

```html
<script>
  let toggle = false
  const toggleButton = () => (toggle = !toggle)
</script>

<button on:click="{toggleButton}" class="burger" />

<nav class:toggle>
  <!-- X Button -->
  <button on:click="{toggleButton}" class="{toggle ? '' : 'hidden'}" />
</nav>

<style>
  .toggle {
    transform: translateX(0);
  }
</style>
```

# <a name="Responsive"></a>Responsive CSS

And we're ready for the fun part. We'll add the responsive CSS

```html
<script>
  import bag from '$lib/images/shopping-bag.svg'

  let toggle = false
  const toggleButton = () => (toggle = !toggle)
</script>

<header class="p-4 border-b lg:pt-6">
  <div class="flex justify-between items-center">
    <button
      on:click="{toggleButton}"
      class="burger bg-no-repeat bg-center w-5 aspect-square xl:hidden"
    />
    <div class="flex justify-center w-full">
      <a href="/" class="font-bold text-xl tracking-widest lg:text-4xl"
        ><h1>NOVAASTRACO</h1></a
      >
    </div>
    <button><img class="w-5" src="{bag}" alt="shopping bag icon" /></button>
  </div>
  <nav class:toggle>
    <button
      on:click="{toggleButton}"
      class="{toggle ? '' : 'hidden'} absolute right-4 top-4 bg-no-repeat bg-center w-6 aspect-square"
    />
    <ul class="font-semibold">
      <li><a href="/tarot">TAROT</a></li>
      <li>
        <a href="/astrology">ASTROLOGY</a>
      </li>
      <li><a class="mr-8" href="/blog">BLOG</a></li>
      <li>
        <a href="/about">ABOUT NOVAASTRACO</a>
      </li>
    </ul>
  </nav>
</header>

<style>
  .burger {
    background-image: url(../images/burguesa.svg);
  }

  ul {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    margin-top: 1.4rem;
  }

  nav button {
    background-image: url(../images/icon-close.svg);
  }

  .toggle {
    transform: translateX(0);
  }

  @media (max-width: 1280px) {
    nav {
      position: fixed;
      z-index: 1000;
      gap: 9rem;
      top: 0;
      left: 0;
      bottom: 0;
      padding-top: 3.7rem;
      padding-left: 1.3rem;
      padding-right: 9rem;
      transform: translateX(-100%);
      transition: transform 300ms ease-in-out;
      background: white;
    }

    ul {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
  }
</style>
```

![navbar with responsive css](/navbar3.png)

# <a name="Background"></a> Background image

We'll add a background image stored in `src/lib/images` to be able to see the sidebar in all its glory.

```html
<!-- src/routes/+page.svelte-->
<main class="h-screen">
  <h1 class="text-right text-white mr-2">main page</h1>
</main>

<style>
  main {
    background-image: url(../lib/images/space.jpg);
  }
</style>
```

```html
<!-- src/routes/astrology/+page.svelte-->
<main class="h-screen">
  <h1 class="text-right text-white mr-2">astrology page</h1>
</main>

<style>
  main {
    background-image: url(../../lib/images/space.jpg);
  }
</style>
```

![responsive sidebar](/navbar4.png)

And there you go, a responsive navbar with sveltekit and tailwind. But there's some homework for you, the logo isn't center because the bag icon is pushing it to the left. How would you fix that?
