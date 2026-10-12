<template>
  <div class="home">
    <van-nav-bar title="智能旅游助手" fixed placeholder />

    <div class="main-content">
      <van-notice-bar
        left-icon="warning-o"
        text="基于AI的智能景点介绍与行程规划系统"
        color="#d48806"
        background="#fffbe6"
      />

      <div class="section">
        <div class="section-title">规划你的旅程</div>
        <van-cell-group inset>
          <van-field
            label="目的地"
            :value="selectedCity || '请选择城市'"
            is-link
            readonly
            placeholder="请选择城市"
            @click="showCityPicker = true"
          />
          <van-field label="预算(元)" placeholder="请输入预算金额" />
          <van-field label="天数" placeholder="请输入天数" />
        </van-cell-group>
        <van-button type="primary" block round class="plan-btn">开始规划</van-button>
      </div>

      <div class="section">
        <div class="section-title">快捷入口</div>
        <div class="quick-entry">
          <div class="entry-item">
            <div class="entry-icon entry-icon--chat">
              <van-icon name="chat-o" />
            </div>
            <span>AI 对话</span>
          </div>
          <div class="entry-item">
            <div class="entry-icon entry-icon--user">
              <van-icon name="user-o" />
            </div>
            <span>我的</span>
          </div>
        </div>
      </div>

      <div class="section">
        <div class="section-title">热门目的地</div>
        <div class="city-grid">
          <van-tag
            v-for="city in cities"
            :key="city"
            round
            class="city-tag"
            @click="pickCity(city)"
          >{{ city }}</van-tag>
        </div>
      </div>
    </div>

    <van-popup v-model:show="showCityPicker" round position="bottom" class="city-popup">
      <div class="city-popup-header">
        <span class="city-popup-title">选择目的地</span>
        <van-icon name="cross" class="city-popup-close" @click="showCityPicker = false" />
      </div>
      <div class="city-popup-body">
        <div class="city-group">
          <div class="city-group-title">热门城市</div>
          <div class="city-grid">
            <van-tag
              v-for="city in cities"
              :key="city"
              round
              class="city-tag"
              :class="{ 'city-tag--active': selectedCity === city }"
              @click="pickCity(city)"
            >{{ city }}</van-tag>
          </div>
        </div>
        <div class="city-group">
          <div class="city-group-title">全部城市</div>
          <div class="city-grid">
            <van-tag
              v-for="city in allCities"
              :key="city"
              round
              class="city-tag"
              :class="{ 'city-tag--active': selectedCity === city }"
              @click="pickCity(city)"
            >{{ city }}</van-tag>
          </div>
        </div>
      </div>
    </van-popup>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const showCityPicker = ref(false)
const selectedCity = ref('')

const cities = ['北京', '上海', '广州', '深圳', '成都', '杭州', '西安', '重庆']
const allCities = [
  '北京', '上海', '广州', '深圳', '成都', '杭州', '西安', '重庆',
  '南京', '武汉', '苏州', '长沙', '天津', '青岛', '厦门', '大理',
  '丽江', '三亚', '桂林', '昆明', '拉萨', '哈尔滨', '大连', '郑州',
]

const pickCity = (city) => {
  selectedCity.value = city
  showCityPicker.value = false
}
</script>

<style scoped>
.home {
  padding-bottom: 60px;
  min-height: 100vh;
  background: #f5f5f5;
}

.main-content {
  padding: 12px 16px;
}

.section {
  margin-top: 20px;
}

.section-title {
  font-size: 16px;
  font-weight: 600;
  color: #323233;
  margin-bottom: 12px;
  padding-left: 4px;
}

:deep(.van-cell-group--inset) {
  margin: 0;
  border-radius: 8px;
  overflow: hidden;
}

.plan-btn {
  margin-top: 16px;
  height: 48px;
  font-size: 16px;
  background: linear-gradient(135deg, #4a90e2, #357abd);
  border: none;
}

.quick-entry {
  display: flex;
  gap: 12px;
}

.entry-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  padding: 24px 0;
  background: #fff;
  border-radius: 8px;
  font-size: 14px;
  color: #323233;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.04);
}

.entry-icon {
  width: 52px;
  height: 52px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 26px;
  color: #fff;
}

.entry-icon--chat {
  background: linear-gradient(135deg, #667eea, #764ba2);
}

.entry-icon--user {
  background: linear-gradient(135deg, #f093fb, #f5576c);
}

.city-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.city-tag {
  padding: 6px 20px;
  font-size: 14px;
  background: #fff;
  color: #646566;
  border: 1px solid #ebedf0;
  cursor: pointer;
  transition: all 0.2s;
}

.city-tag:active {
  transform: scale(0.95);
}

.city-tag--active {
  background: #4a90e2;
  color: #fff;
  border-color: #4a90e2;
}

.city-popup {
  max-height: 70vh;
  border-top-left-radius: 16px;
  border-top-right-radius: 16px;
  overflow: hidden;
}

.city-popup-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px;
  border-bottom: 1px solid #ebedf0;
}

.city-popup-title {
  font-size: 16px;
  font-weight: 600;
  color: #323233;
}

.city-popup-close {
  font-size: 20px;
  color: #969799;
  cursor: pointer;
}

.city-popup-body {
  padding: 16px;
  max-height: calc(70vh - 56px);
  overflow-y: auto;
}

.city-group {
  margin-bottom: 20px;
}

.city-group:last-child {
  margin-bottom: 0;
}

.city-group-title {
  font-size: 14px;
  font-weight: 500;
  color: #969799;
  margin-bottom: 12px;
}
</style>
