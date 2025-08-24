<template>
  <div id="app" class="container py-5 d-flex justify-content-center align-items-center min-vh-100">
    <Transition name="slide-left" mode="out-in">
      <div
        v-if="step === 1"
        key="step-1"
        class="card shadow-lg p-4 w-100 text-center"
        @touchstart="handleTouchStart"
        @touchend="handleTouchEnd"
        @touchcancel="handleTouchEnd"
      >
        <div class="card-body">
          <h1 class="card-title text-pink mb-4">
            Hey, {{ herName }}! I have a question for you. 😉
          </h1>
          <img
            :src="herPhoto"
            alt="A photo of her"
            class="img-fluid rounded-circle mb-4 card-image"
          />
          <p class="lead mb-4">Let's start something new. Swipe to see my idea!</p>
          <button @click="nextStep" class="btn btn-primary btn-lg fw-bold rounded-pill shadow-sm">
            Ready!
          </button>
        </div>
      </div>

      <div
        v-else-if="step === 2"
        key="step-2"
        class="card shadow-lg p-4 w-100 text-center"
        @touchstart="handleTouchStart"
        @touchend="handleTouchEnd"
        @touchcancel="handleTouchEnd"
      >
        <div class="card-body">
          <h1 class="card-title text-pink mb-4">I was thinking we could...</h1>
          <img
            :src="funPhoto"
            alt="A photo of a fun activity"
            class="img-fluid rounded mb-4 card-image"
          />
          <div class="bg-light-pink p-3 rounded mb-4">
            <p class="mb-0 fs-5">
              <strong>What:</strong> A fun afternoon doing something new together. ✨
            </p>
          </div>
          <p class="fst-italic text-secondary mt-3">
            (You'll want to wear some comfortable pants and shoes for this.)
          </p>
          <button @click="nextStep" class="btn btn-secondary btn-lg fw-bold rounded-pill mt-3">
            Keep going!
          </button>
        </div>
      </div>

      <div
        v-else-if="step === 3"
        key="step-3"
        class="card shadow-lg p-4 w-100 text-center"
        @touchstart="handleTouchStart"
        @touchend="handleTouchEnd"
        @touchcancel="handleTouchEnd"
      >
        <div class="card-body">
          <h1 class="card-title text-pink mb-4">First, let's talk details...</h1>
          <img
            :src="smPhoto"
            alt="A photo of SM City Cabanatuan"
            class="img-fluid rounded mb-4 card-image"
          />
          <div class="bg-light-pink p-3 rounded mb-4">
            <p class="mb-1 fs-5"><strong>When:</strong> This Saturday at 1 PM</p>
          </div>
          <button @click="nextStep" class="btn btn-secondary btn-lg fw-bold rounded-pill mt-3">
            Got it!
          </button>
        </div>
      </div>

      <div
        v-else-if="step === 4"
        key="step-4"
        class="card shadow-lg p-4 w-100 text-center"
        @touchstart="handleTouchStart"
        @touchend="handleTouchEnd"
        @touchcancel="handleTouchEnd"
      >
        <div class="card-body">
          <h1 class="card-title text-pink mb-4">So, why SM?</h1>
          <p class="lead mb-4">
            It's a great spot because it's convenient and there's so much to do. We can grab food,
            hang out in the cool A/C, and there are a lot of fun activities all in one place.
          </p>
          <button @click="nextStep" class="btn btn-secondary btn-lg fw-bold rounded-pill mt-3">
            Makes sense!
          </button>
        </div>
      </div>

      <div v-else-if="step === 5" key="step-5" class="card shadow-lg p-4 w-100 text-center">
        <div class="card-body">
          <h1 class="card-title text-pink mb-4">Just one more thing...</h1>
          <p class="lead mb-4">Would you prefer that I pick you up, or should we meet at SM?</p>
          <div class="d-grid gap-3">
            <button
              @click="selectMeetup('SM Cabanatuan')"
              class="btn btn-primary btn-lg fw-bold rounded-pill shadow-sm"
            >
              I'll meet you there!
            </button>
            <button
              @click="selectMeetup('I\'ll pick you up!')"
              class="btn btn-outline-secondary rounded-pill"
            >
              You can pick me up!
            </button>
          </div>
        </div>
      </div>

      <div v-else-if="step === 6" key="step-6" class="card shadow-lg p-4 w-100 text-center">
        <div class="card-body">
          <h1 class="card-title text-pink mb-4">So, what do you say?</h1>
          <img :src="proposalPhoto" alt="A cute cat" class="img-fluid rounded mb-4 card-image" />
          <div class="d-grid gap-3">
            <button
              @click="acceptDate"
              class="btn btn-primary btn-lg fw-bold rounded-pill shadow-sm"
            >
              Owkie!
            </button>
            <button @click="declineDate" class="btn btn-outline-secondary rounded-pill">
              No, thank you.
            </button>
          </div>
        </div>
      </div>

      <div
        v-else-if="step === 7"
        key="step-7"
        class="card text-center shadow-lg p-4 w-100 animate__animated animate__rubberBand"
      >
        <div class="card-body">
          <h1 class="card-title text-success mb-3">YES! Can't wait to meet you! 🥳</h1>
          <p class="lead mb-4">This is going to be so much fun.</p>
          <img
            :src="catGif"
            alt="A celebratory cat gif"
            class="img-fluid rounded mb-4 card-image"
          />
          <div class="bg-light-green p-3 rounded text-start">
            <p class="mb-1"><strong>What:</strong> A fun afternoon doing something new together</p>
            <p class="mb-1"><strong>When:</strong> This Saturday at 1 PM</p>
            <p class="mb-1"><strong>Where:</strong> {{ finalLocation }}</p>
            <p class="fst-italic text-secondary mt-3">(Seriously, comfy shoes. 😉)</p>
          </div>
        </div>
      </div>

      <div v-else-if="step === 8" key="step-8" class="card shadow-lg p-4 w-100 text-center">
        <div class="card-body">
          <h1 class="card-title text-pink mb-4">Are you sure? 🥺</h1>
          <img :src="sadMeme1" alt="Sad meme" class="img-fluid rounded mb-4 card-image" />
          <div class="d-grid gap-3">
            <button
              @click="acceptDate"
              class="btn btn-primary btn-lg fw-bold rounded-pill shadow-sm"
            >
              Wait... yes!
            </button>
            <button @click="declineAgain" class="btn btn-outline-secondary rounded-pill">
              Still no.
            </button>
          </div>
        </div>
      </div>

      <div v-else-if="step === 9" key="step-9" class="card shadow-lg p-4 w-100 text-center">
        <div class="card-body">
          <h1 class="card-title text-pink mb-4">Wait, but why? I'm literally going to cry. 😭</h1>
          <img :src="sadMeme2" alt="Crying meme" class="img-fluid rounded mb-4 card-image" />
          <div class="d-grid gap-3">
            <button
              @click="acceptDate"
              class="btn btn-primary btn-lg fw-bold rounded-pill shadow-sm"
            >
              Fine, you win. Yes!
            </button>
            <button @click="lastDecline" class="btn btn-outline-secondary rounded-pill">
              I'm sorry, no.
            </button>
          </div>
        </div>
      </div>

      <div v-else-if="step === 10" key="step-10" class="card shadow-lg p-4 w-100 text-center">
        <div class="card-body">
          <h1 class="card-title text-pink mb-4">Okay, I get it. I'll just be over here. 💔</h1>
          <img :src="sadMeme3" alt="Dramatic sad meme" class="img-fluid rounded mb-4 card-image" />
          <button @click="resetApp" class="btn btn-secondary mt-4">Start Over</button>
        </div>
      </div>
    </Transition>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import 'animate.css'

import herPhoto from './images/les.jpg'
import smPhoto from './images/sm-cab.jpg'
import funPhoto from './images/cute-cat.jpg'
import proposalPhoto from './images/fun-cat.jpg'
import sadMeme1 from './images/sad-meme-1.jpg'
import sadMeme2 from './images/sad-meme-2.webp'
import sadMeme3 from './images/sad-meme-3.webp'
import catGif from './images/cat.gif'

const herName = 'Les'

const step = ref<number>(1)
const touchStartX = ref<number>(0)
const finalLocation = ref<string>('SM Cabanatuan')

const handleTouchStart = (event: TouchEvent): void => {
  touchStartX.value = event.touches[0].clientX
}

const handleTouchEnd = (event: TouchEvent): void => {
  const touchEndX = event.changedTouches[0].clientX
  const swipeDistance = touchStartX.value - touchEndX

  const swipeThreshold = 50

  if (swipeDistance > swipeThreshold && step.value < 5) {
    nextStep()
  }
}

const nextStep = (): void => {
  step.value++
}

const selectMeetup = (location: string): void => {
  finalLocation.value = location
  step.value = 6 // Move to the final question card
}

const acceptDate = (): void => {
  step.value = 7
}

const declineDate = (): void => {
  step.value = 8
}

const declineAgain = (): void => {
  step.value = 9
}

const lastDecline = (): void => {
  step.value = 10
}

const resetApp = (): void => {
  step.value = 1
}
</script>

<style>
/* Custom styles */
.text-pink {
  color: #ff69b4;
}
.bg-light-pink {
  background-color: #fff0f5;
}
.bg-light-green {
  background-color: #f0fff0;
}
.min-vh-100 {
  min-height: 100vh;
}
.card-image {
  max-width: 250px;
  max-height: 250px;
  object-fit: cover;
}
.btn-secondary {
  --bs-btn-bg: #888;
  --bs-btn-border-color: #888;
}

/* Vue Transition Styles for swiping effect */
.slide-left-enter-active,
.slide-left-leave-active {
  transition: all 0.5s ease-in-out;
}

.slide-left-enter-from,
.slide-left-leave-to {
  opacity: 0;
  transform: translateX(100%);
}

.slide-left-leave-from,
.slide-left-enter-to {
  opacity: 1;
  transform: translateX(0);
}
</style>
