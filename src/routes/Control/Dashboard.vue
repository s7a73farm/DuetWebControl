<template>
	<v-row>
		<v-col xs="12" sm="8" md="8" lg="9" xl="9">
			<movement-panel class="mb-3"></movement-panel>
			<extrude-panel></extrude-panel>
			<fan-panel></fan-panel>
		</v-col>
		<v-col xs="4" sm="4" md="4" lg="3" xl="3">
			<webcam-panel></webcam-panel>
			<macro-list></macro-list>
		</v-col>
	</v-row>
</template>

<script>
'use strict'

import { mapState } from 'vuex'

import { registerRoute } from '..'
import { MachineMode } from '../../store/machine/modelEnums.js'

export default {
	computed: {
		...mapState('machine/model', {
			atxPower: state => state.state.atxPower,
			machineMode: state => state.state.machineMode
		}),
		isFFForUnset() {
			return !this.machineMode || (this.machineMode === MachineMode.fff);
		}
	},
	install() {
		// Register a route via Control -> Dashboard
		registerRoute(this, {
			Control: {
				Dashboard: {
					icon: 'mdi-view-dashboard',
					caption: 'menu.control.dashboard',
					path: '/'
				}
			}
		});
	}
}
</script>
