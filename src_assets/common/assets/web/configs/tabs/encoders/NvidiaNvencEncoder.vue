<script setup>
import { ref } from 'vue'
import Checkbox from "../../../Checkbox.vue";

const props = defineProps([
  'platform',
  'config',
])

const config = ref(props.config)
</script>

<template>
  <div id="nvidia-nvenc-encoder" class="config-page">
    <!-- Performance preset -->
    <div class="mb-3">
      <label for="nvenc_preset" class="form-label">{{ $t('config.nvenc_preset') }}</label>
      <select id="nvenc_preset" class="form-select" v-model="config.nvenc_preset">
        <option value="1">P1 {{ $t('config.nvenc_preset_1') }}</option>
        <option value="2">P2</option>
        <option value="3">P3</option>
        <option value="4">P4</option>
        <option value="5">P5</option>
        <option value="6">P6</option>
        <option value="7">P7 {{ $t('config.nvenc_preset_7') }}</option>
      </select>
      <div class="form-text">{{ $t('config.nvenc_preset_desc') }}</div>
    </div>

    <!-- Two-pass mode -->
    <div class="mb-3">
      <label for="nvenc_twopass" class="form-label">{{ $t('config.nvenc_twopass') }}</label>
      <select id="nvenc_twopass" class="form-select" v-model="config.nvenc_twopass">
        <option value="disabled">{{ $t('config.nvenc_twopass_disabled') }}</option>
        <option value="quarter_res">{{ $t('config.nvenc_twopass_quarter_res') }}</option>
        <option value="full_res">{{ $t('config.nvenc_twopass_full_res') }}</option>
      </select>
      <div class="form-text">{{ $t('config.nvenc_twopass_desc') }}</div>
    </div>

    <!-- Spatial AQ -->
    <Checkbox class="mb-3"
              id="nvenc_spatial_aq"
              locale-prefix="config"
              v-model="config.nvenc_spatial_aq"
              default="false"
    ></Checkbox>

    <!-- Single-frame VBV/HRD percentage increase -->
    <div class="mb-3">
      <label for="nvenc_vbv_increase" class="form-label">{{ $t('config.nvenc_vbv_increase') }}</label>
      <input type="number" min="0" max="400" class="form-control" id="nvenc_vbv_increase" placeholder="0"
             v-model="config.nvenc_vbv_increase" />
      <div class="form-text">
        {{ $t('config.nvenc_vbv_increase_desc') }}<br>
        <br>
        <a href="https://en.wikipedia.org/wiki/Video_buffering_verifier">VBV/HRD</a>
      </div>
    </div>

    <!-- Miscellaneous options -->
    <div class="mb-3 accordion">
      <div class="accordion-item">
        <h2 class="accordion-header">
          <button class="accordion-button" type="button" data-bs-toggle="collapse"
                  data-bs-target="#panelsStayOpen-collapseOne">
            {{ $t('config.misc') }}
          </button>
        </h2>
        <div id="panelsStayOpen-collapseOne" class="accordion-collapse collapse show"
             aria-labelledby="panelsStayOpen-headingOne">
          <div class="accordion-body">
            <!-- NVENC Realtime HAGS priority -->
            <Checkbox v-if="platform === 'windows'"
                      class="mb-3"
                      id="nvenc_realtime_hags"
                      locale-prefix="config"
                      v-model="config.nvenc_realtime_hags"
                      default="true"
            >
              <br>
              <br>
              <a href="https://devblogs.microsoft.com/directx/hardware-accelerated-gpu-scheduling/">HAGS</a>
            </Checkbox>

            <!-- Prefer lower encoding latency over power savings -->
            <Checkbox v-if="platform === 'windows'"
                      class="mb-3"
                      id="nvenc_latency_over_power"
                      locale-prefix="config"
                      v-model="config.nvenc_latency_over_power"
                      default="true"
            ></Checkbox>

            <!-- Present OpenGL/Vulkan on top of DXGI -->
            <Checkbox v-if="platform === 'windows'"
                      class="mb-3"
                      id="nvenc_opengl_vulkan_on_dxgi"
                      locale-prefix="config"
                      v-model="config.nvenc_opengl_vulkan_on_dxgi"
                      default="true"
            ></Checkbox>

            <!-- NVENC H264 CAVLC -->
            <Checkbox class="mb-3"
                      id="nvenc_h264_cavlc"
                      locale-prefix="config"
                      v-model="config.nvenc_h264_cavlc"
                      default="false"
            ></Checkbox>

            <!-- NVENC Intra Refresh -->
            <div>
              <label for="nvenc_h264_cavlc" class="form-label">{{ $t('config.nvenc_intra_refresh') }}</label>
              <select id="nvenc_h264_cavlc" class="form-select" v-model="config.nvenc_intra_refresh">
                <option value="disabled">{{ $t('_common.auto') }}</option>
                <option value="enabled">{{ $t('_common.enabled') }}</option>
              </select>
              <div class="form-text">{{ $t('config.nvenc_intra_refresh_desc') }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
