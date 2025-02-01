<script setup>
  import IconEllipsis from "./icons/IconEllipsis.vue";

  defineProps({
    title: { type: String },
    current: { type: Number },
    previous: { type: Number },
    period: {type: String },
    icon: { type: Object, default: null },
    color: {type: String },
  })
</script>

<template>
  <div class="info-card">
    <component class="info-card__icon" :is="icon" ></component>
    <div class="info-card__content">
        <div class="info-card__heading">
          <div class="info-card__title">{{ title }}</div>
          <button type="button" aria-label="button" class="info-card__btn">
            <IconEllipsis/>
          </button>
        </div>
        <div class="info-card__time">
          <div class="info-card__time-current">{{ current }}hrs</div>
          <div class="info-card__time-period">{{ period }} - {{ previous }}</div>
        </div>
    </div>
  </div>
</template>

<style scoped>
  .info-card {
    position: relative;
    display: flex;
    flex-direction: column;
    padding-top: 38px;
    background-color: v-bind(color);
    border-radius: 15px;
    overflow: hidden;
  }

  @media (min-width: 768px) {
    .info-card {
      padding-top: 45px;
    }
  }

  .info-card__icon {
    position: absolute;
    z-index: 1;
    right: 11px;
    top: -8px;
  }

  .info-card__content {
    position: relative;
    z-index: 2;
    border-radius: 15px;
    background-color: var(--dark-blue);
    padding: 28px 24px;
    height: 100%;
    cursor: pointer;
    transition: all 0.3s ease-in-out;
  }

  @media (min-width: 768px) {
    .info-card__content {
      padding: 29px 30px 32px 30px;
    }
  }

  .info-card__content:hover {
    background-color: var(--blue);
  }

  .info-card__title {
    font-weight: 500;
    font-size: 18px;
  }

  .info-card__heading {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .info-card__time {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: 6px;
  }

  @media (min-width: 768px) {
    .info-card__time {
      flex-direction: column;
      align-items: flex-start;
      gap: 8px;
      margin-top: 24px;
    }
  }

  .info-card__time-current {
    font-weight: 300;
    font-size: 32px;
    line-height: 1.303;
  }

  @media (min-width: 768px) {
    .info-card__time-current {
      font-size: 56px;
    }
  }

  .info-card__time-period {
    font-weight: 400;
    font-size: 15px;
    color: var(--pale-blue);
  }

  .info-card__btn svg {
    transition: all 0.3s ease-in-out;
    fill: var(--pale-blue);
  }

  .info-card__btn:hover svg {
    fill: var(--color-white);
  }
</style>
