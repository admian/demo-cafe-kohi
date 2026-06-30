<script setup lang="ts">
import { ref } from 'vue'

const menuItems = [
  { name: 'Espresso', price: '$3.50', desc: 'Single origin, double shot' },
  { name: 'Pour Over', price: '$5.00', desc: 'Ethiopian Yirgacheffe, hand brewed' },
  { name: 'Matcha Latte', price: '$5.50', desc: 'Ceremonial grade, oat milk' },
  { name: 'Cold Brew', price: '$4.50', desc: '18-hour steep, smooth & bold' },
  { name: 'Seasonal Pastry', price: '$4.00', desc: 'Rotating selection from local bakers' },
  { name: 'Breakfast Set', price: '$12.00', desc: 'Coffee + pastry + fresh fruit' },
]

const hours = [
  { day: 'Mon – Fri', time: '7:00 AM – 6:00 PM' },
  { day: 'Saturday', time: '8:00 AM – 7:00 PM' },
  { day: 'Sunday', time: '8:00 AM – 4:00 PM' },
]

const toast = ref<string | null>(null)
const reserveName = ref('')
const reserveEmail = ref('')

let toastTimer: number | undefined

function scrollTo(id: string) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}

function showToast(message: string) {
  toast.value = message
  if (toastTimer) window.clearTimeout(toastTimer)
  toastTimer = window.setTimeout(() => {
    toast.value = null
  }, 3200)
}

function handleReserve(source: string) {
  showToast(`Thanks for your interest! (${source}) — This is a portfolio demo.`)
  scrollTo('visit')
}

function handleMenuClick(name: string) {
  showToast(`${name} — available daily. Portfolio demo only.`)
}

function scrollTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function handleReservationSubmit() {
  if (!reserveName.value.trim() || !reserveEmail.value.trim()) {
    showToast('Please enter your name and email.')
    return
  }
  showToast(`Reservation request received for ${reserveName.value.trim()} — demo form only.`)
  reserveName.value = ''
  reserveEmail.value = ''
}
</script>

<template>
  <div class="min-h-screen bg-[#faf6f1] text-[#3d2e24]">
    <!-- Toast -->
    <div
      v-if="toast"
      role="status"
      class="fixed bottom-6 left-1/2 z-[100] max-w-sm -translate-x-1/2 rounded-xl border border-[#c4956a]/40 bg-white px-5 py-3 text-sm text-[#3d2e24] shadow-xl"
    >
      {{ toast }}
    </div>

    <!-- Nav -->
    <header class="fixed top-0 z-50 w-full bg-[#faf6f1]/90 backdrop-blur-md">
      <div class="mx-auto flex max-w-5xl items-center justify-between px-6 py-5">
        <button
          type="button"
          class="font-serif text-2xl font-semibold tracking-tight"
          @click="scrollTop"
        >
          Kōhī House
        </button>
        <nav class="hidden items-center gap-8 font-sans text-sm text-[#6b5a4e] md:flex">
          <button type="button" class="transition hover:text-[#3d2e24]" @click="scrollTo('menu')">Menu</button>
          <button type="button" class="transition hover:text-[#3d2e24]" @click="scrollTo('about')">Our Story</button>
          <button type="button" class="transition hover:text-[#3d2e24]" @click="scrollTo('visit')">Visit</button>
        </nav>
        <button
          type="button"
          class="font-sans rounded-full bg-[#3d2e24] px-5 py-2 text-sm font-medium text-[#faf6f1] transition hover:bg-[#5c4a3d]"
          @click="handleReserve('Nav')"
        >
          Reserve a table
        </button>
      </div>
    </header>

    <!-- Hero -->
    <section class="relative px-6 pb-20 pt-28 md:pt-36">
      <div class="mx-auto grid max-w-5xl items-center gap-12 md:grid-cols-2">
        <div>
          <p class="font-sans text-sm font-medium uppercase tracking-[0.2em] text-[#a08060]">
            Est. 2019 · Portland
          </p>
          <h1 class="mt-4 font-serif text-5xl font-semibold leading-[1.1] md:text-6xl">
            Slow coffee.<br />Warm mornings.
          </h1>
          <p class="mt-6 font-sans text-lg leading-relaxed text-[#6b5a4e]">
            A quiet corner for thoughtful brews, seasonal pastries, and the kind of
            mornings that don't need to rush anywhere.
          </p>
          <div class="mt-8 flex flex-wrap gap-4 font-sans">
            <button
              type="button"
              class="rounded-full bg-[#c4956a] px-7 py-3 text-sm font-semibold text-white transition hover:bg-[#b38459]"
              @click="scrollTo('menu')"
            >
              View menu
            </button>
            <button
              type="button"
              class="rounded-full border border-[#3d2e24]/20 px-7 py-3 text-sm font-semibold transition hover:bg-[#3d2e24]/5"
              @click="scrollTo('visit')"
            >
              Find us
            </button>
          </div>
        </div>
        <div class="relative">
          <div class="aspect-[4/5] overflow-hidden rounded-3xl bg-gradient-to-br from-[#d4b896] to-[#a08060] shadow-2xl">
            <div class="flex h-full flex-col items-center justify-center p-8 text-center text-white">
              <div class="mb-6 flex h-24 w-24 items-center justify-center rounded-full bg-white/20 text-5xl backdrop-blur">
                ☕
              </div>
              <p class="font-serif text-2xl font-medium">Single Origin</p>
              <p class="mt-2 font-sans text-sm text-white/80">Ethiopia · Guji Zone · Natural Process</p>
            </div>
          </div>
          <div class="absolute -bottom-4 -left-4 rounded-2xl bg-white px-5 py-4 shadow-lg font-sans">
            <p class="text-xs text-[#a08060]">Today's roast</p>
            <p class="font-semibold">Guji Natural</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Menu -->
    <section id="menu" class="scroll-mt-24 bg-[#3d2e24] px-6 py-20 text-[#faf6f1]">
      <div class="mx-auto max-w-5xl">
        <div class="text-center">
          <p class="font-sans text-sm uppercase tracking-[0.2em] text-[#c4956a]">What we serve</p>
          <h2 class="mt-3 font-serif text-4xl font-semibold">The Menu</h2>
        </div>
        <div class="mt-14 grid gap-6 sm:grid-cols-2 lg:grid-cols-3">
          <button
            v-for="item in menuItems"
            :key="item.name"
            type="button"
            class="rounded-2xl border border-white/10 bg-white/5 p-6 text-left transition hover:bg-white/10"
            @click="handleMenuClick(item.name)"
          >
            <div class="flex items-start justify-between gap-4">
              <h3 class="font-serif text-xl font-medium">{{ item.name }}</h3>
              <span class="font-sans shrink-0 text-[#c4956a] font-semibold">{{ item.price }}</span>
            </div>
            <p class="mt-2 font-sans text-sm text-[#faf6f1]/60">{{ item.desc }}</p>
          </button>
        </div>
      </div>
    </section>

    <!-- About -->
    <section id="about" class="scroll-mt-24 px-6 py-20">
      <div class="mx-auto grid max-w-5xl items-center gap-12 md:grid-cols-2">
        <div class="aspect-square overflow-hidden rounded-3xl bg-gradient-to-br from-[#e8ddd0] to-[#c4956a]/40">
          <div class="flex h-full items-center justify-center font-serif text-6xl text-[#3d2e24]/20">
            珈琲
          </div>
        </div>
        <div>
          <p class="font-sans text-sm uppercase tracking-[0.2em] text-[#a08060]">Our story</p>
          <h2 class="mt-3 font-serif text-4xl font-semibold leading-tight">
            Crafted with care, served with intention
          </h2>
          <p class="mt-6 font-sans leading-relaxed text-[#6b5a4e]">
            Kōhī House started as a weekend pop-up and grew into a neighborhood gathering place.
            We source directly from small farms, roast in small batches, and believe great coffee
            is as much about the moment as the cup.
          </p>
          <p class="mt-4 font-sans leading-relaxed text-[#6b5a4e]">
            Every drink is made to order. Every pastry is baked fresh. Every visit is meant to feel
            like a small pause in a busy day.
          </p>
          <div class="mt-8 flex gap-8 font-sans">
            <div>
              <p class="text-3xl font-bold text-[#c4956a]">12+</p>
              <p class="text-sm text-[#6b5a4e]">Origin partners</p>
            </div>
            <div>
              <p class="text-3xl font-bold text-[#c4956a]">4.9★</p>
              <p class="text-sm text-[#6b5a4e]">Google rating</p>
            </div>
            <div>
              <p class="text-3xl font-bold text-[#c4956a]">100%</p>
              <p class="text-sm text-[#6b5a4e]">Compostable cups</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Visit -->
    <section id="visit" class="scroll-mt-24 bg-[#f0ebe3] px-6 py-20">
      <div class="mx-auto max-w-5xl">
        <div class="grid gap-12 md:grid-cols-2">
          <div>
            <p class="font-sans text-sm uppercase tracking-[0.2em] text-[#a08060]">Visit us</p>
            <h2 class="mt-3 font-serif text-4xl font-semibold">Find Kōhī House</h2>
            <address class="mt-6 font-sans not-italic leading-relaxed text-[#6b5a4e]">
              2847 Hawthorne Blvd<br />
              Portland, OR 97214<br />
              United States
            </address>
            <p class="mt-4 font-sans text-[#6b5a4e]">
              <a href="tel:+15035550142" class="hover:text-[#3d2e24]">(503) 555-0142</a>
              ·
              <a href="mailto:hello@kohihouse.demo" class="hover:text-[#3d2e24]">hello@kohihouse.demo</a>
            </p>
            <div class="mt-8 space-y-3 font-sans">
              <div
                v-for="h in hours"
                :key="h.day"
                class="flex justify-between border-b border-[#3d2e24]/10 pb-2 text-sm"
              >
                <span class="font-medium">{{ h.day }}</span>
                <span class="text-[#6b5a4e]">{{ h.time }}</span>
              </div>
            </div>
          </div>
          <div class="flex flex-col justify-center">
            <div class="rounded-3xl border border-[#3d2e24]/10 bg-white p-8 shadow-sm">
              <h3 class="font-serif text-2xl font-semibold">Reserve a table</h3>
              <p class="mt-2 font-sans text-sm text-[#6b5a4e]">
                Weekends fill up fast. Book ahead for groups of 4+.
              </p>
              <form class="mt-6 space-y-4 font-sans" @submit.prevent="handleReservationSubmit">
                <input
                  v-model="reserveName"
                  type="text"
                  placeholder="Your name"
                  class="w-full rounded-xl border border-[#3d2e24]/15 bg-[#faf6f1] px-4 py-3 text-sm outline-none focus:border-[#c4956a]"
                />
                <input
                  v-model="reserveEmail"
                  type="email"
                  placeholder="Email address"
                  class="w-full rounded-xl border border-[#3d2e24]/15 bg-[#faf6f1] px-4 py-3 text-sm outline-none focus:border-[#c4956a]"
                />
                <button
                  type="submit"
                  class="w-full rounded-xl bg-[#3d2e24] py-3 text-sm font-semibold text-[#faf6f1] transition hover:bg-[#5c4a3d]"
                >
                  Request reservation
                </button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="border-t border-[#3d2e24]/10 px-6 py-10">
      <div class="mx-auto flex max-w-5xl flex-col items-center justify-between gap-4 font-sans text-sm text-[#6b5a4e] sm:flex-row">
        <p>© 2026 Kōhī House. Portfolio demo project.</p>
        <div class="flex gap-6">
          <button type="button" class="hover:text-[#3d2e24]" @click="showToast('Follow @kohihouse_demo — portfolio demo only.')">
            Instagram
          </button>
          <button type="button" class="hover:text-[#3d2e24]" @click="showToast('Like us on Facebook — portfolio demo only.')">
            Facebook
          </button>
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.font-serif {
  font-family: "Playfair Display", Georgia, serif;
}
</style>
