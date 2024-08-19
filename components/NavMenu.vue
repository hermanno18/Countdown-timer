<script setup lang="ts">
import { ref } from 'vue'
import { Mail, Linkedin, Twitter, Github, X } from 'lucide-vue-next'

const isVisible = ref(false)
const isMenuVisible = ref(false)
const navContainer = ref()

const navigation = [
  { text: 'Accueil', route: '/' },
  { text: 'Créer', route: '/creer' },
  { text: "C'est quoi ce site ?", route: '/about' },
  { text: 'Me connaître', route: '/me' }
]

const toggleMenu = () => {
  if (isVisible.value) {
    // Fermeture du menu
    isMenuVisible.value = false
    isVisible.value = false
  } else {
    // Ouverture du menu
    isVisible.value = true
    isMenuVisible.value = true
  }
}

const onEnter = (el: Element, done: () => void) => {
  const tl = useGsap.timeline({ onComplete: done })
  const listItems = el.querySelectorAll('li')

  tl.to(el, {
    borderRadius: 25,
    duration: 0.2,
  }).to(el, {
    height: "calc(100vh - 3rem)",
    width: "calc(100vw - 3rem)",
    borderRadius: 25,
    duration: 0.5,
    ease: 'power2.inOut',
  }).to(el, {
    height: "100vh",
    top: 0,
    right: 0,
    width: "100vw",
    borderRadius: 0,
    duration: 0.5,
    ease: 'power2.inOut',
  }).from(listItems, {
    opacity: 0,
    x: -50,
    duration: 0.5,
    stagger: 0.1,
    ease: 'power2.out'
  }, "-=0.3") // Commence l'animation des puces légèrement avant la fin de l'animation du conteneur
}

const onLeave = (el: Element, done: () => void) => {
  const tl = useGsap.timeline({ onComplete: done })
  const listItems = el.querySelectorAll('li')

  tl.to(el, {
    height: "calc(100vh - 3rem)",
    width: "calc(100vw - 3rem)",
    borderRadius: 25,
    top: '1.25rem',
    right: "1.25rem",
    duration: 0.5,
    ease: 'power2.inOut',
  }, "-=0.2")
    .to(listItems, {
      opacity: 0,
      x: -50,
      duration: 0.3,
      stagger: 0.05,
      ease: 'power2.in'
    }).to(el, {
      height: "3rem",
      width: "3rem",
      duration: 0.5,
      ease: 'power2.inOut',
    }).to(el, {
      borderRadius: 999,
      duration: 0.2,
    })
}
</script>

<template>
  <header class="relative">
    <Transition @enter="onEnter" @leave="onLeave" :css="false">
      <div v-if="isVisible" ref="navContainer"
        class="size-12 right-5 top-5 rounded-full z-10 bg-background/95 absolute backdrop-blur-md overflow-hidden flex items-center justify-center">
        <nav id="navMenu" class="text-start p-5 w-fit">
          <ul class="flex flex-col justify-center gap-7 text-5xl overflow-hidden">
            <li v-for="(link, index) in navigation" :key="link.route" :data-index="index">
              {{ link.text }}
            </li>
          </ul>
          <div class="mt-16 space-x-5">
            <Button variant="outline" class="sdf">
              <Twitter class="w-4 h-4 mr-2" />
            </Button>
            <Button variant="outline" class="space-x-2">
              <Mail class="w-4 h-4 " /> <span>-</span> <span>Email</span>
            </Button>
            <Button variant="outline" class="space-x-2">
              <Linkedin class="w-4 h-4 " /> <span>-</span> <span>LinkedIn</span>
            </Button>
            <Button variant="outline" class="space-x-2">
              <Github class="w-4 h-4 " /> <span>-</span> <span>Github</span>
            </Button>
          </div>
        </nav>
      </div>
    </Transition>
    <Button id="menuToggler" @click="toggleMenu"
      class="title border border-background z-10 size-12 shadow shadow-foreground rounded-full !absolute top-5 right-5 overflow-hidden p-3">
      <X class="size-8" />
    </Button>
  </header>
</template>