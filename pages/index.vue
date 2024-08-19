<script setup lang="ts">
import { ArrowRight, ArrowLeft } from 'lucide-vue-next'
const route = useRoute()

onMounted(() => {
  useGsap.to('.title', { rotation: 3, duration: 1 })
})

</script>

<template>
  <div class="h-screen relative text-center">
    <div class="bg-red-500 bg-cover opacity-30 bg-center h-full w-full top-0 absolute"
      style="background-image: url(https://media.themoviedb.org/t/p/w533_and_h300_bestv2/dvBCdCohwWbsP5qAaglOXagDMtk.jpg);">
      <div class="h-full bg-gradient-to-b from-10% from-background/30  to-background/90 to-80%"></div>
    </div>
    <NavMenu />
    <div class="relative top-0 h-full ">
      <div class="absolute bottom-0 w-full min-h-[30%] left-0 p-5 ">
        <h1 class="text-4xl m-0 font-dhurjati title">Summary of our integrated capabilitie</h1>
        <h1 class="mb-5 font-black text-9xl align-top f font-dhurjati font-">000 : 00 : 00 : 00</h1>
        <div class="mt-12 max-w-xs mx-auto">
          <Button class="w-full">bonjour tois</Button>
          <p>
            <a href="/chat">chat</a>
            
          </p>
          <a href="/perplex">pp</a>
          <div class="flex justify-between mt-12 pb-4">
            <Button variant="outline" class="rounded-full p-2 bg-transparent aspect-square">
              <ArrowLeft class="size-8" />
            </Button>
            <Button variant="outline" class="rounded-full p-2 bg-transparent  aspect-square">
              <ArrowRight class="size-8" />
            </Button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

