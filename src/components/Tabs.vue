<template>
  <section class="tabs">
    <div class="tabs-title">
      <div
        class="tabs-title__btn"
        :class="{ 'tabs-title__active': activeTab === i }"
        v-for="(tab, i) in tabsInfo"
        :key="i"
        @click="activeTab = i"
        @keydown="activeTab = i"
      >
        {{ tab.title }}
      </div>
    </div>
    <div class="additional divider-bottom" v-if="additionalInfo.length">
      <div class="additional-item" v-for="(item, i) in additionalInfo" :key="i">
        <div class="additional-item__stats">{{ item.value }}</div>
        <div class="additional-item__title">{{ item.title }}</div>
      </div>
    </div>
    <div class="tabs-info">
      {{ tabsInfo[activeTab].description }}
    </div>
  </section>
  <section class="mtabs">
    <div
      class="mtabs-item"
      v-for="(tab, i) in tabsInfo"
      :key="i"
      @click="activeTab = i"
      @keydown="activeTab = i"
    >
      <div
        class="mtabs-item__title"
        :class="{ 'mtabs-item__active': activeTab === i }"
      >
        {{ tab.title }}
      </div>
      <div class="cross" :class="{ active: activeTab === i }"></div>
      <div
        class="additional divider-bottom"
        v-if="activeTab === i && additionalInfo.length"
      >
        <div
          class="additional-item"
          v-for="(item, i) in additionalInfo"
          :key="i"
        >
          <div class="additional-item__stats">{{ item.value }}</div>
          <div class="additional-item__title">{{ item.title }}</div>
        </div>
      </div>
      <div class="tabs-info" v-if="activeTab === i">
        {{ tabsInfo[activeTab].description }}
      </div>
    </div>
  </section>
</template>

<script>
import tabs from '../data/tabs';

export default {
  name: 'TTabs',
  data() {
    return {
      tabsInfo: [],
      activeTab: 0,
    };
  },
  created() {
    this.tabsInfo = tabs;
  },
  computed: {
    additionalInfo() {
      return this.tabsInfo[this.activeTab].additionalInfo;
    },
  },
};
</script>

<style scoped lang="scss">
.tabs {
  @media (max-width: 769px) {
    display: none;
  }
}

.tabs-title {
  display: flex;
  justify-content: center;
}

.tabs-title {
  &__btn {
    width: 182px;
    height: 37px;
    display: flex;
    align-items: center;
    justify-content: center;
    text-transform: uppercase;
    font-weight: 600;
    font-size: 18px;
    border-bottom: 1px solid black;
    border-top: 1px solid black;
    border-left: 1px solid black;
    cursor: pointer;
    letter-spacing: 1.4px;
  }

  &__btn:last-of-type {
    border-right: 1px solid black;
  }

  &__active {
    color: #ffffff;
    background-color: #000000;
  }
}

.tabs-info {
  max-width: 640px;
  text-align: center;
  margin-top: 50px;
  font-size: 14px;
  @media (max-width: 769px) {
    margin-top: 10px;
  }
}
.additional {
  max-width: 640px;
  margin-top: 46px;
  display: flex;
  justify-content: center;
  position: relative;
  padding-bottom: 18px;

  @media (max-width: 769px) {
    max-width: 100%;
    margin-top: 12px;
  }

  &-item {
    margin: 0 30px;
    position: relative;
    @media (max-width: 768px) {
      margin: 0 15px;
    }

    &__stats {
      font-size: 52px;
      @media (max-width: 768px) {
        font-size: 32px;
      }
    }
    &__title {
      font-size: 23px;
      text-align: center;
      @media (max-width: 768px) {
        font-size: 14px;
      }
    }
  }
}
.divider-bottom:after {
  content: '';
  position: absolute;
  bottom: 0;
  width: 42px;
  height: 1px;
  border-bottom: 1px solid black;
}

.mtabs {
  @media (min-width: 768px) {
    display: none;
  }
  &-item {
    //padding: 8px 0px;
    position: relative;
  }
  &-item__title {
    display: flex;
    align-items: center;
    padding: 12px 16px;
    font-size: 14px;
    font-weight: 700;
    letter-spacing: 2px;
    text-transform: uppercase;
    border-bottom: 1px solid black;

    &.mtabs-item__active {
      border-bottom: none;
    }
  }
}
.cross {
  //margin-right: 15px;
  margin-top: 3px;
  position: absolute;
  right: 26px;
  top: 14px;
}

.cross:before,
.cross:after {
  content: '';
  position: absolute;
  top: 3px;
  border-top: 1px solid #3e474f;
  width: 8px;
  display: block;

  //margin-top: 18px;
  transition: 0.3s;
}

.cross:after {
  transform: rotate(90deg);
}
.cross.active {
  &:after {
    transform: rotate(0deg);
  }
  &:before {
    transform: rotate(180deg);
  }
}
</style>
