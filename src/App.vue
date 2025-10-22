<template>
  <div>
    <Beverage 
      :isIced="currentTemp === 'Cold'" 
      :selectedBase="selectedBase"
      :selectedCreamer="selectedCreamer"
      :selectedSyrup="selectedSyrup"
    />
    
    <div class="controls">
      <!-- Temperature Selection -->
      <div class="control-group">
        <h3>Temperature</h3>
        <ul>
          <li>
            <template v-for="temp in temps" :key="temp">
              <label>
                <input
                  type="radio"
                  name="temperature"
                  :id="`r${temp}`"
                  :value="temp"
                  v-model="currentTemp"
                />
                {{ temp }}
              </label>
            </template>
          </li>
        </ul>
      </div>

      <!-- Base Beverage Selection -->
      <div class="control-group">
        <h3>Base Beverage</h3>
        <ul>
          <li v-for="base in bases" :key="base.id">
            <label>
              <input
                type="radio"
                name="base"
                :id="`base-${base.id}`"
                :value="base"
                v-model="selectedBase"
              />
              {{ base.name }}
            </label>
          </li>
        </ul>
      </div>

      <!-- Creamer Selection -->
      <div class="control-group">
        <h3>Creamer</h3>
        <ul>
          <li v-for="creamer in creamers" :key="creamer.id">
            <label>
              <input
                type="radio"
                name="creamer"
                :id="`creamer-${creamer.id}`"
                :value="creamer"
                v-model="selectedCreamer"
              />
              {{ creamer.name }}
            </label>
          </li>
        </ul>
      </div>

      <!-- Syrup Selection -->
      <div class="control-group">
        <h3>Syrup</h3>
        <ul>
          <li v-for="syrup in syrups" :key="syrup.id">
            <label>
              <input
                type="radio"
                name="syrup"
                :id="`syrup-${syrup.id}`"
                :value="syrup"
                v-model="selectedSyrup"
              />
              {{ syrup.name }}
            </label>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import Beverage from "./components/Beverage.vue";
import { temps, currentTemp, bases, creamers, syrups } from "./stores/beverage";
import type { BaseBeverageType, CreamerType, SyrupType } from "./stores/beverage";

// Initialize with default selections
const selectedBase = ref<BaseBeverageType>(bases.value[2]); // Coffee
const selectedCreamer = ref<CreamerType>(creamers.value[0]); // No Creamer
const selectedSyrup = ref<SyrupType>(syrups.value[0]); // No Syrup
</script>

<style lang="scss">
body,
html {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  background-color: #6e4228;
  background: linear-gradient(to bottom, #6e4228 0%, #956f5a 100%);
}
ul {
  list-style: none;
}

.controls {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  margin-top: 2rem;
  justify-content: center;
}

.control-group {
  background: rgba(255, 255, 255, 0.1);
  padding: 1rem;
  border-radius: 8px;
  min-width: 150px;
  
  h3 {
    color: white;
    margin: 0 0 1rem 0;
    font-size: 1.2rem;
  }
  
  ul {
    margin: 0;
    padding: 0;
  }
  
  li {
    margin: 0.5rem 0;
  }
  
  label {
    color: white;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    
    &:hover {
      color: #f0f0f0;
    }
  }
  
  input[type="radio"] {
    margin: 0;
  }
}
</style>
