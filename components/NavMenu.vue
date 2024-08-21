<script setup lang="ts">
import { ref } from 'vue'
import { Mail, Linkedin, Twitter, Github, X , ChevronRight, ChevronsRight} from 'lucide-vue-next'

const isVisible = ref(false)
const navContainer = ref()

const navigation = [
  { text: 'Home', route: '/' },
  { text: 'Create', route: '/creer' },
  { text: "What is this site ?", route: '/about' },
  { text: 'Know me', route: '/me' }
]

const toggleMenu = () => {
  if (isVisible.value) {
    // Fermeture du menu
    isVisible.value = false
  } else {
    // Ouverture du menu
    isVisible.value = true
  }
}

const onEnter = (el: Element, done: () => void) => {
  const tl = useGsap.timeline({ onComplete: done })
  const listItems = el.querySelectorAll('li')
  const buttons = el.querySelectorAll('.buttons button')

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
  }, "-=0.3") 
  .from(buttons, {
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
  const buttons = el.querySelectorAll('.buttons button')

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
    })
    .to(buttons, {
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
          <ul class="flex flex-col justify-center gap-6  overflow-hidden">
            <li v-for="(link, index) in navigation" :key="link.route" :data-index="index">
              <nuxt-link to="/" href="" class=" overflow-clip duration-200 delay-500 hover:translate-x-4 group flex w-fit gap-3 items-center">
                <div class="mt-2 flex ">
                  <ChevronRight class="m-0  translate-x-0 group-hover:-translate-x-full transition-transform delay-150 duration-150 ease-in-out" />
                  <ChevronsRight class="absolute -translate-x-full group-hover:-translate-x-0 delay-150 transition-transform duration-150 ease-in-out m-0" />
                </div>
                <span class="text-4xl sm:text-5xl  li" >
                  {{ link.text }}
                </span>
              </nuxt-link>
            </li>
          </ul>
          <div class="mt-16 space-x-5 buttons">
            <Button variant="outline" class="">
              <div class="flex items-center  gap-2">
                <Twitter class="w-4 h-4 " />
              </div>
            </Button>
            <Button variant="outline" class="">
              <div class="flex items-center  gap-2">
                <Mail class="w-4 h-4 " /> <span class="hidden sm:inline-flex">-</span> <span class="hidden min-[455px]:inline-flex" >Email</span>
              </div>
            </Button>
            <Button variant="outline" class="">
              <div class="flex items-center  gap-2">
                <Linkedin class="w-4 h-4 " /> <span class="hidden sm:inline-flex">-</span> <span class="hidden min-[455px]:inline-flex">LinkedIn</span>
              </div>
            </Button>
            <Button variant="outline" class="">
              <div class="flex items-center  gap-2">
                <Github class="w-4 h-4 " /> <span class="hidden sm:inline-flex">-</span> <span class="hidden min-[455px]:inline-flex">Github</span>
              </div>
            </Button>

          </div>
        </nav>
      </div>
    </Transition>
    <Button id="menuToggler" @click="toggleMenu"
      class="title border border-background z-10 size-16 shadow shadow-foreground rounded-full !absolute top-5 right-5 overflow-hidden ">
      <X class="size-8" />
    </Button>
  </header>
</template>