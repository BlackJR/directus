<script setup lang="ts">
import { computed } from 'vue';
import LatencyIndicator from './latency-indicator.vue';
import { useServerStore } from '@/stores/server';

const serverStore = useServerStore();

const name = computed(() => serverStore.info?.project?.project_name);
const descriptor = computed(() => serverStore.info?.project?.project_descriptor);
</script>

<template>
	<div class="project-info">
		<latency-indicator />
		<div class="name-container">
			<v-text-overflow class="name" :text="name" placement="bottom" />
			<v-text-overflow v-if="descriptor" class="descriptor" :text="descriptor" placement="bottom" />
		</div>
	</div>
</template>

<style lang="scss" scoped>
.project-info {
	position: relative;
	display: flex;
	align-items: center;
	width: 100%;
	height: calc(60px + var(--theme--navigation--project--border-width));
	padding-left: 20px;
	color: var(--theme--navigation--project--foreground);
	text-align: left;
	background: var(--theme--navigation--project--background);
	border-bottom: var(--theme--navigation--project--border-width) solid var(--theme--navigation--project--border-color);

	.name-container {
		flex-grow: 1;
		width: 100px;
		margin-left: 12px;
		line-height: 1.3;
		margin-right: 8px;
	}

	.name {
		font-family: var(--theme--navigation--project--font-family);
	}

	.descriptor {
		color: var(--theme--foreground-subdued);
	}
}
</style>
