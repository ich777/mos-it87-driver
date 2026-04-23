<template>
  <div>
    <h2 class="mb-4">{{ $t('plugin_it87_driver.title') }}</h2>
    <v-skeleton-loader v-if="loading" :loading="true" type="card" />
    <div v-else style="margin-bottom: 80px">
      <v-card v-if="driverInfo && driverInfo.package" class="mb-4 pa-0">
        <v-card-title>{{ $t('plugin_it87_driver.local_driver_package') }}</v-card-title>
        <v-card-text class="pa-4">
          <v-row dense>
            <v-col cols="6" md="3">
              <div class="text-caption text-medium-emphasis"><strong>{{ $t('plugin_it87_driver.plugin') }}</strong></div>
              <div class="text-body-2">{{ driverInfo.plugin || '-' }}</div>
            </v-col>
            <v-col cols="6" md="3">
              <div class="text-caption text-medium-emphasis"><strong>{{ $t('plugin_it87_driver.kernel') }}</strong></div>
              <div class="text-body-2">{{ driverInfo.kernel || '-' }}</div>
            </v-col>
            <v-col cols="12" md="6">
              <div class="text-caption text-medium-emphasis"><strong>{{ $t('plugin_it87_driver.package') }}</strong></div>
              <div class="text-body-2" style="word-break: break-all">{{ driverInfo.package || '-' }}</div>
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const PLUGIN_NAME = 'it87-driver';

const loading = ref(true);
const driverInfo = ref(null);

const getAuthHeaders = () => ({
  Authorization: 'Bearer ' + localStorage.getItem('authToken'),
});

const fetchDriverInfo = async () => {
  try {
    const res = await fetch(`/api/v1/mos/plugins/driver/${PLUGIN_NAME}`, {
      headers: getAuthHeaders(),
    });
    if (res.ok) {
      driverInfo.value = await res.json();
    }
  } catch (e) {
    console.error('Failed to fetch driver info:', e);
  }
};

onMounted(async () => {
  try {
    await fetchDriverInfo();
  } catch (e) {
    console.error('Failed to initialize:', e);
  } finally {
    loading.value = false;
  }
});
</script>
