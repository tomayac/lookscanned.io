<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="5" md="4" lg="3">
        <ScanSettingsCard
          @update:pdfSource="(url) => (pdfSource = url)"
          @update:page="(page) => (previewPage = page)"
          @action:preview="preview"
          v-model:config="config"
        />
      </v-col>

      <v-col cols="12" sm="7" md="8" lg="9">
        <SideBySidePreview
          :pdfSource="pdfSource"
          :page="previewPage"
          :config="previewConfig"
        />
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts" setup>
import type { ProcessConfig } from "@/utils/makeScanned";
import { defaultConfig } from "@/utils/makeScanned";
import SideBySidePreview from "@/components/preview/SideBySidePreview.vue";
import ScanSettingsCard from "@/components/ScanSettings/ScanSettingsCard.vue";
import { ref } from "vue";

const pdfSource = ref("/examples/pdfs/test.pdf");
const config = ref(defaultConfig);
const previewConfig = ref(
  JSON.parse(JSON.stringify(config.value)) as ProcessConfig
);
const previewPage = ref(1);

function preview() {
  previewConfig.value = JSON.parse(
    JSON.stringify(config.value)
  ) as ProcessConfig;
}
</script>
