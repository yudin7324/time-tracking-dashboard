<script setup>
  import avatar from '@/assets/images/image-jeremy.png';

  defineProps({
    activeTimeframe: String
  })

  const emit = defineEmits(['update-timeframe'])

  const timeframes = ['daily', 'weekly', 'monthly']
</script>

<template>
  <div class="main-card">
    <div class="main-card__info">
      <div class="main-card__avatar">
        <img :src="avatar" alt="avatar" />
      </div>
      <div>
        <div class="main-card__subtitle">Report for</div>
        <h1 class="main-card__title">Jeremy Robson</h1>
      </div>
    </div>
    <div class="main-card__links">
      <button
        class="main-card__link"
        v-for="timeframe in timeframes"
        :key="timeframe"
        :class="{ active: activeTimeframe === timeframe }"
        @click="emit('update-timeframe', timeframe)"
        type="button"
        aria-label="filter-button"
      >
        {{ timeframe }}
      </button>
    </div>
  </div>
</template>

<style scoped>
  .main-card {
    display: flex;
    flex-direction: column;
    background-color: var(--dark-blue);
    border-radius: 15px;
    overflow: hidden;
  }

  @media (min-width: 768px) {
    .main-card {
      grid-area: main-card;
    }
  }

  .main-card__info {
    display: flex;
    align-items: center;
    flex-grow: 1;
    padding: 32px 29px;
    border-radius: 15px;
    background: #5747EA;
    gap: 17px;
  }

  @media (min-width: 768px) {
    .main-card__info {
      flex-direction: column;
      align-items: flex-start;
      padding: 34px 32px;
      gap: 17px;
    }
  }

  .main-card__avatar {
    height: 78px;
    width: 78px;
    min-width: 78px;
    border-radius: 50%;
    border: 3px solid var(--color-white);
    overflow: hidden;
    box-shadow: 0 4px 4px 0 rgba(0, 0, 0, 0.25);
  }

  .main-card__avatar img {
    object-fit: cover;
    width: 100%;
    height: 100%;
  }

  .main-card__subtitle {
    font-size: 15px;
    color: var(--pale-blue);
  }

  .main-card__title {
    font-weight: 300;
    font-size: 40px;
    margin-top: 3px;
  }

  .main-card__links {
    display: flex;
    align-items: center;
    justify-content: space-around;
    gap: 21px;
    padding: 24px 25px;
  }

  @media (min-width: 768px) {
    .main-card__links {
      flex-direction: column;
      align-items: flex-start;
      padding: 26px 32px 33px 32px;
    }
  }

  .main-card__link {
    display: inline-block;
    font-size: 18px;
    color: var(--desaturated-blue);
    transition: color 0.3s ease-in-out;
    text-decoration: none;
    text-transform: capitalize;
  }

  .main-card__link:hover, .active {
    color: var(--color-white);
  }
</style>
