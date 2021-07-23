<template>
	<header class="topbar-wrap" :class="{ 'collapsed': header.collapsed }">
		<div class="container">

			<!-- main topbar row with logo and buttons -->
			<div class="topbar-main flex-row flex-middle flex-stretch">

				<!-- topbar logo -->
				<div class="topbar-logo">
					<h1 class="text-primary-hover clickable" @click="setRoute( '/' )">
						<i class="icon-chart-line"></i> <span class="text-uppercase text-clip if-medium">Binance
							Watch</span>
					</h1>
				</div>

				<!-- topbar top tokens -->
				<div class="topbar-prices flex-row flex-middle flex-1" v-if="options.prices.header">
					
				</div>

				<!-- topbar buttons and menu -->

				<div class="topbar-menu text-nowrap">


					<SelectMenu class="topbar-dropdown" v-model="watchOptions.priceType" @change="formChange">
						<option value="change">English</option>
						<option value="gain">Vietnamese</option>
					</SelectMenu>
					<Dropdown class="topbar-dropdown" :class="{ 'alert-bubble': hasBubble }">
						<button slot="trigger" class="topbar-btn">Hi Test1<a class="icon-down-open"></a></button>
						<ul slot="list">
							<li class="heading">
								<span class="form-label">Main Navigation</span>
							</li>
							<li class="clickable text-bright-hover text-nowrap" @click="setRoute( '/index' )">
								<i class="icon-chart-line iconLeft"></i> index
							</li>
							<li class="clickable text-bright-hover text-nowrap" @click="setRoute( '/' )">
								<i class="icon-chart-line iconLeft"></i> Live Ticker
							</li>
							<li class="clickable text-bright-hover text-nowrap" @click="setRoute( '/news' )">
								<i class="icon-feedback iconLeft"></i> Twitter News <span class="text-grey"
									v-if="newsCount">({{ newsCount }})</span>
							</li>
							<li class="clickable text-bright-hover text-nowrap" @click="setRoute( '/alarms' )">
								<i class="icon-alarm iconLeft"></i> Saved Alarms <span class="text-grey"
									v-if="alarmsData.length">({{ alarmsData.length }})</span>
							</li>
							<li class="clickable text-bright-hover text-nowrap" @click="setRoute( '/history' )">
								<i class="icon-clock iconLeft"></i> Recent History <span class="text-grey"
									v-if="historyData.length">({{ historyData.length }})</span>
							</li>
							<li class="clickable text-bright-hover text-nowrap" @click="setRoute( '/trade' )">
								<i class="icon-percent iconLeft"></i> Trade Bot
							</li>
							<li class="clickable text-bright-hover text-nowrap" @click="setRoute( '/options' )">
								<i class="icon-config iconLeft"></i> App Options
							</li>
							<li class="clickable text-bright-hover text-nowrap" @click="setRoute( '/about' )">
								<i class="icon-help iconLeft"></i> App Info
							</li>
						</ul>
					</Dropdown>

				</div>
			</div>

		</div>
	</header>
</template>

<script>
	import Dropdown from "./Dropdown.vue";
	import watchPresets from "../configs/watchPresets";
	import Watcher from "../modules/watcher";
	import SelectMenu from "./SelectMenu.vue";
	// component
	export default {
		// component list
		components: { Dropdown, SelectMenu },

		// component props
		props: {
			header: {
				type: Object,
				default() {
					return {};
				},
			},
			options: {
				type: Object,
				default() {
					return {};
				},
			},
			priceData: {
				type: Array,
				default() {
					return [];
				},
			},
			historyData: {
				type: Array,
				default() {
					return [];
				},
			},
			alarmsData: {
				type: Array,
				default() {
					return [];
				},
			},
			newsEntries: {
				type: Array,
				default() {
					return [];
				},
			},
			tickerStatus: { type: Number, default: 0 },
			tickerTime: { type: String, default: "" },
		},

		// component data
		data() {
			return {
				watching: false,
				watchOptions: {
					market: "BTC", // market pair
					priceType: "change", // change, gain, loss
					priceChange: "2", // change percent
					priceCheck: "below", // above, below
					price: "", // custom price limit
					volumeType: "gain", // change, gain, loss
					volumeChange: "1", // change percent
					volumeCheck: "above", // above, below
					volume: "", // custom volume limit
					changeCheck: "above", // above, below
					change: "0", // custom 24h percent change
					volatilityCheck: "below", // above, below
					volatility: "0", // custom volatility limit
					dangerCheck: "below", // above, below
					danger: "0", // custom danger limit
					timeCheck: "less", // more, less
					timeLimit: "10", // limit change by time (mins)
					filterType: "deny", // deny, allow
					filterText: "", // csv tokens str
				},
			};
		},

		// computed methods
		formChange(e) {
			//this.watchPreset = '';
			//this.buildSnapshot();
			//this.$notify.flush();
		},
		computed: {
			// compute number of active alarms for all tokens
			alarmsCount() {
				return this.alarmsData.filter((e) => e.active).length | 0;
			},

			// compute number of "new" history entries
			historyCount() {
				return this.historyData.filter((e) => e.isNew).length | 0;
			},

			// compute number of "new" news entries
			newsCount() {
				return this.newsEntries.filter((e) => e.isNew).length | 0;
			},

			// check if alert button should be visible
			hasBubble() {
				return this.historyCount || this.newsCount;
			},

			// get top 3 usdt coins based on volume
			marketPrices() {
				let market = this.options.prices.market || "USDT";
				let list = this.priceData.filter((p) => p.market === market);
				return this.$utils.sort(list, "percent", "desc").slice(0, 3);
			},
		},

		// custom methods
		methods: {
			// set app url route
			setRoute(route) {
				this.$router.setRoute(route);
			},

			// toggle socket connection
			toggleConnection() {
				if (this.tickerStatus) {
					this.$binance.stopTickerStream();
				} else {
					this.$binance.startTickerStream(true);
				}
			},
		},

		// on component created
		created() {
			this.$bus.on("priceWatch", (status) => {
				this.watching = status;
			});
		},
	};
</script>

<style lang="scss">
	// topbar wrapper
	.topbar-wrap {
		display: block;
		position: fixed;
		left: 0;
		top: 0;
		width: 100%;
		background-color: $colorDocumentLight;
		z-index: ($zindexElements + 10);

		// main topbar container
		.topbar-main {
			height: $topbarHeight;

			// topbar logo
			.topbar-logo {
				h1 {
					font-size: 150%;
					line-height: 1em;
					text-transform: uppercase;
				}
			}

			// top asset prices
			.topbar-prices {
				font-size: 80%;
				line-height: 1.1em;
				letter-spacing: 0;
				font-weight: normal;

				&>div {
					margin-left: $padSpace / 1.5;
					padding-left: $padSpace / 1.5;
					border-left: $lineWidth $lineStyle $lineColor;
				}

				@media #{$screenSmall} {
					letter-spacing: 1px;

					&>div {
						margin-left: $padSpace;
						padding-left: $padSpace;
					}
				}
			}

			// button/links
			.topbar-btn {
				display: inline-block;
				margin: 0 0 0 0.5em;
				font-size: 180%;
				line-height: 1em;
				color: $colorDefault;

				&.pulse {
					animation: pulseFade 1s linear infinite;
				}

				&:before {
					opacity: 1;
				}

				&:hover:before {
					opacity: 0.8;
				}
			}

			// dropdown component
			.topbar-dropdown {
				display: inline-block;
				position: relative;
			}
		}

		// collapsed mode
		&.collapsed {
			transform: translateY(-#{$topbarHeight});
		}
	}
</style>