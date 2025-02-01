<script setup>
import { ref, onMounted, computed } from 'vue'
import MainCard from '@/components/MainCard.vue';
import InfoCard from '@/components/InfoCard.vue';
import IconWork from '@/components/icons/IconWork.vue';
import IconStudy from '@/components/icons/IconStudy.vue';
import IconPlay from '@/components/icons/IconPlay.vue';
import IconSelfCare from '@/components/icons/IconSelfCare.vue';
import IconExercise from '@/components/icons/IconExercise.vue';
import IconSocials from '@/components/icons/IconSocial.vue';

const cards = ref([]);
const activeTimeframe = ref('daily');

const cardStyles = {
  Work: { color: "var(--light-red)", icon: IconWork },
  Play: { color: "var(--soft-blue)", icon: IconPlay },
  Study: { color: "var(--light-pink)", icon: IconStudy },
  Exercise: { color: "var(--lime-green)", icon: IconExercise },
  Social: { color: "var(--violet)", icon: IconSocials },
  "Self Care": { color: "var(--soft-orange)", icon: IconSelfCare }
}

onMounted(async () => {
  try {
    const response = await fetch('data.json');

    if (!response.ok) {
      console.error('Oops! Something went wrong.')
      return;
    }

    const data = await response.json()
    cards.value = data;
  } catch (error) {
    console.error('Fetch error:', error)
  }
})

function setCurrentPeriod(period) {
  if(period === "daily") {
    return "last day"
  } else if (period === "weekly") {
    return "last week"
  } else {
    return "last month"
  }
}

const filteredCards = computed(() =>
  cards.value.map(card => ({
    title: card.title,
    current: card.timeframes[activeTimeframe.value].current,
    previous: card.timeframes[activeTimeframe.value].previous,
    period: setCurrentPeriod(activeTimeframe.value),
    color: cardStyles[card.title]?.color || "hsl(0, 0%, 50%)",
    icon: cardStyles[card.title]?.icon || null,
  }))
)

const updateTimeframe = (newTimeframe) => {
  activeTimeframe.value = newTimeframe
}
</script>


<template>
  <div class="dashboard">
    <MainCard
      :activeTimeframe="activeTimeframe"
      @update-timeframe="updateTimeframe"
    />

    <InfoCard
      v-for="(card, index) in filteredCards"
      :key="index"
      :title="card.title"
      :current="card.current"
      :previous="card.previous"
      :period="card.period"
      :color="card.color"
      :icon="card.icon"
    />
  </div>
</template>

<style scoped>
  .dashboard {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    gap: 24px;
    width: 100%;
  }

  @media (min-width: 768px) {
    .dashboard {
      gap: 30px;
      grid-template-areas:
      "main-card main-card main-card "
      "info-card info-card info-card "
      "info-card info-card info-card";
      grid-template-columns: repeat(3, 1fr);
    }
  }

  @media (min-width: 1024px) {
    .dashboard {
      grid-template-columns: repeat(4, 1fr);
      grid-template-areas:
      "main-card info-card info-card info-card"
      "main-card info-card info-card info-card";
    }
  }
</style>
