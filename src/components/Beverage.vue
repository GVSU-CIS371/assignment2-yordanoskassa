<template>
  <Mug>
    <Cold v-if="isIced" />
    <Hot v-else />
    <Contents>
      <!-- Conditional rendering based on customer selections -->
      <template v-slot:top>
        <!-- Show creamer only if not "No Cream" -->
        <Creamer 
          v-if="hasCreamer"
          :creamer="selectedCreamer"
          :class="{ 'no-gap': !hasSyrup }"
        />
      </template>
      <template v-slot:mid>
        <!-- Show syrup only if not "No Syrup" -->
        <Syrup 
          v-if="hasSyrup"
          :syrup="selectedSyrup"
        />
      </template>
      <template v-slot:bottom>
        <!-- Base beverage is always shown -->
        <Base :base="selectedBase" />
      </template>
    </Contents>
  </Mug>
</template>
<script setup lang="ts">
import { computed } from "vue";
import Contents from "./Contents.vue";
import Mug from "./Mug.vue";
import Syrup from "./Syrup.vue";
import Base from "./Base.vue";
import Creamer from "./Creamer.vue";
import Hot from "./Hot.vue";
import Cold from "./Cold.vue";

import type { BaseBeverageType, CreamerType, SyrupType } from "../stores/beverage";

type Props = {
  isIced: boolean;
  selectedBase: BaseBeverageType;
  selectedCreamer: CreamerType;
  selectedSyrup: SyrupType;
};
const props = defineProps<Props>();

// Computed properties for conditional rendering logic
const hasCreamer = computed(() => props.selectedCreamer.name !== "No Creamer");
const hasSyrup = computed(() => props.selectedSyrup.name !== "No Syrup");
</script>

<style scoped>
/* When there's no syrup, creamer should be directly on top of base beverage */
.no-gap {
  margin-bottom: 0 !important;
  transform: translateY(200%) !important;
}
</style>
