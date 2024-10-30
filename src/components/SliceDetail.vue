<template>
  <div ref="outerEl" @mousedown.stop>
    <div class="text-start execution-memory-node">
      <header class="mt-0 d-flex">
        <FontAwesomeIcon
          fixed-width
          :icon="faPizzaSlice"
          class="text-secondary py-1"
        ></FontAwesomeIcon>
        <span class="text-body px-1">
          Slice : {{ memoryDetails[SliceProp.SLICE_NUM] }}
        </span>
      </header>
      <header class="mb-2 d-flex justify-content-between">
        <h4
          class="overflow-hidden btn btn-light text-start py-0 px-0 d-flex"
          @click.prevent.stop="showDetails = !showDetails"
        >
          <span class="text-secondary">
            <FontAwesomeIcon
              fixed-width
              :icon="faChevronUp"
              v-if="showDetails"
            ></FontAwesomeIcon>
            <FontAwesomeIcon
              fixed-width
              :icon="faChevronDown"
              v-else
            ></FontAwesomeIcon>
          </span>
          <span> </span>
          ExecutorMemory
        </h4>
      </header>

      <div
        v-if="showDetails"
        class="d-flex flex-column justify-content-around px-3"
      >
        <span
          v-if="
            memoryDetails.ExecutorMemory?.[ExecutorMemoryEnum.AVERAGE_MEMORY]
          "
          class="text-secondary"
        >
          average memory :
          {{ memoryDetails.ExecutorMemory[ExecutorMemoryEnum.AVERAGE_MEMORY] }}
        </span>
        <span v-else class="text-secondary">average memory : N/A</span>

        <span
          v-if="
            memoryDetails.ExecutorMemory?.[
              ExecutorMemoryEnum.NUMBER_OF_WORKER_THREADS
            ]
          "
          class="text-secondary"
        >
          Number of worker threads :
          {{
            memoryDetails.ExecutorMemory[
              ExecutorMemoryEnum.NUMBER_OF_WORKER_THREADS
            ]
          }}
        </span>
        <span v-else class="text-secondary"
          >Number of worker threads : N/A</span
        >

        <span
          v-if="
            memoryDetails.ExecutorMemory?.[ExecutorMemoryEnum.MAXIMUM_MEMORY]
          "
          class="text-secondary"
        >
          Maximum memory :
          {{ memoryDetails.ExecutorMemory[ExecutorMemoryEnum.MAXIMUM_MEMORY] }}
        </span>
        <span v-else class="text-secondary">Maximum memory : N/A</span>
      </div>

      <span v-if="memoryDetails.WorkMemory" class="text-secondary mt-3 px-3">
        WorkMemory : {{ memoryDetails.WorkMemory }}
      </span>
      <span v-else class="text-secondary mt-3 px-3">WorkMemory : N/A</span>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref } from "vue"
import {
  faChevronDown,
  faChevronUp,
  faPizzaSlice,
} from "@fortawesome/free-solid-svg-icons"
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome"
import { ExecutorMemoryEnum, SliceProp } from "@/enums"
import type { Slice } from "@/interfaces" // 确保引入 Slice 接口

// 确保 Props 接口使用 Slice 类型
interface Props {
  memoryDetails: Slice
}

const props = defineProps<Props>()
const memoryDetails = reactive<Slice>(props.memoryDetails)
const showDetails = ref<boolean>(false)

const outerEl = ref<Element | null>(null)
</script>
