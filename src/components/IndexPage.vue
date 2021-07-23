<template>
	<main class="page-wrap" :class="{ 'collapsed': header.collapsed, 'opaque':
		header.opaque }">

		<!-- controls section -->

		<section class="push-bottom" v-if="!tweetsList.length">
			<div class="container">
				<div class="card pad-all flex-stretch">
					<div class="row">
						<div class="col-md-7 col-sm-7 col-xs-12 col-lg-7">
							<div class="row">
								<div class="col-md-4 push-top">
									<h6 class="text-primary text-center">Last</h6>
									<div class="text-center"><span class="text-grey">31,613.75000000 USDT</span></div>
								</div>
								<div class="col-md-4 push-top">
									<h6 class="text-primary text-center">24hr Low</h6>
									<div class="text-center"><span class="text-grey">31,613.75000000 USDT</span></div>
								</div>
								<div class="col-md-4 push-top">
									<h6 class="text-primary text-center">24hr High</h6>
									<div class="text-center"><span class="text-grey">31,613.75000000 USDT</span></div>
								</div>
							</div>
							<div class="row">
								<div class="col-md-4 push-top push-large">
									<h6 class="text-primary text-center">24hr Volume</h6>
									<div class="text-center"><span class="text-grey">31,613.75000000 USDT</span></div>
								</div>
								<div class="col-md-4 push-top push-large">
									<h6 class="text-primary text-center">24hr Change</h6>
									<div class="text-center"><span style="color:red">-1.058% </span></div>
								</div>
								<div class="col-md-4 push-top push-large">
									<h6 class="text-primary text-center">Server Time:</h6>
									<div class="text-center"><span class="text-grey">31,613.75000000 USDT</span></div>
								</div>
							</div>
						</div>
						<div class="col-md-5 col-sm-5 col-xs-12 col-lg-5">
							<div class="row">
								<div class="col-md-4">
									<h5 class="text-primary text-center">Last</h5>
									<div class="text-center"><span class="text-grey">31,613.75000000 USDT</span></div>
								</div>
								<div class="col-md-4">
									<h5 class="text-primary text-center">Last</h5>
									<div class="text-center"><span class="text-grey">31,613.75000000 USDT</span></div>
								</div>
								<div class="col-md-4">
									<h5 class="text-primary text-center">Last</h5>
									<div class="text-center"><span class="text-grey">31,613.75000000 USDT</span></div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</section>
		<!-- chart section -->
		<section class="push-bottom">
			<div class="container">

				<div class="card tablelist-wrap">
					<div class="row push-top push-large">
						<div class="col-md-7 mb-3 col-lg-7">
							<img class="img-fluid" src="public/images/btc-usdt-chart.jpg" />
						</div>
						<div class="col-md-5 mb-3 col-lg-5">
							<Tabs class="push-bottom">

								<!-- proxy -->
								<section btn-class="icon-network" btn-name="USDT Market" active>
									<section class="pagelist-wrap">
										<div class="container">
											<div class="pagelist-item flex-row flex-middle flex-stretch"
												v-if="USDTList.length">
												<div class="push-right text-clip flex-1"><span class="clickable"
													@click="$sorter.sortOrder( 'ticker', 'coin', 'asc' )">Coin</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'price', 'asc' )">Price</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'volume', 'desc' )">Volume</span></div>
												<div class="push-right text-clip flex-1"
													v-if="options.prices.chart"></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'change', 'desc' )">Change</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'name', 'desc' )">Name</span></div>
											</div>
											<div v-for="p in USDTList" class="pagelist-item flex-row
												flex-middle flex-stretch clickable" :class="p.style"
												@click.stop="setRoute( p.route )" :key="p.symbol">

												<div class="push-right text-clip flex-1">
													<span class="text-info">{{ p.coin }}</span>
												</div>

												<div class="push-right text-clip flex-1">
													 <span class="text-info">{{ p.price }}</span>
												</div>
												<div class="push-right text-clip flex-1 ">
													<span class="text-nowrap text-info">{{ p.volume }}</span>
												</div>

												<div class="push-right text-clip flex-1"> 
													<span class="text-nowrap item-color-buy">{{ p.change }}</span>
												</div>

												<div class="push-right text-clip flex-1 ">
													<span class="text-nowrap text-info">{{ p.name }}</span>
												</div>

											</div>

											<!-- if there are more items not included in list due to limit option -->
											

										</div>
									</section>
								</section>

								<!-- binance -->
								<section btn-class="icon-chart-line" btn-name="ETH Market">
									<section class="pagelist-wrap">
										<div class="container">
											<div class="pagelist-item flex-row flex-middle flex-stretch"
												v-if="ETHList.length">
												<div class="push-right text-clip flex-1"><span class="clickable"
													@click="$sorter.sortOrder( 'ticker', 'coin', 'asc' )">Coin</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'price', 'asc' )">Price</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'volume', 'desc' )">Volume</span></div>
												<div class="push-right text-clip flex-1"
													v-if="options.prices.chart"></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'change', 'desc' )">Change</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'name', 'desc' )">Name</span></div>
											</div>
											<div v-for="p in ETHList" class="pagelist-item flex-row
												flex-middle flex-stretch clickable" :class="p.style"
												@click.stop="setRoute( p.route )" :key="p.symbol">

												<div class="push-right text-clip flex-1">
													<span class="text-info">{{ p.coin }}</span>
												</div>

												<div class="push-right text-clip flex-1">
													 <span class="text-info">{{ p.price }}</span>
												</div>
												<div class="push-right text-clip flex-1 ">
													<span class="text-nowrap text-info">{{ p.volume }}</span>
												</div>

												<div class="push-right text-clip flex-1"> 
													<span class="text-nowrap item-color-buy">{{ p.change }}</span>
												</div>

												<div class="push-right text-clip flex-1 ">
													<span class="text-nowrap text-info">{{ p.name }}</span>
												</div>

											</div>

											<!-- if there are more items not included in list due to limit option -->
											

										</div>
									</section>
								</section>

								<!-- mailgun -->
								<section btn-class="icon-at" btn-name="BTC Market">
									<section class="pagelist-wrap">
										<div class="container">
											<div class="pagelist-item flex-row flex-middle flex-stretch"
												v-if="BTCList.length">
												<div class="push-right text-clip flex-1"><span class="clickable"
													@click="$sorter.sortOrder( 'ticker', 'coin', 'asc' )">Coin</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'price', 'asc' )">Price</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'volume', 'desc' )">Volume</span></div>
												<div class="push-right text-clip flex-1"
													v-if="options.prices.chart"></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'change', 'desc' )">Change</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'name', 'desc' )">Name</span></div>
											</div>
											<div v-for="p in BTCList" class="pagelist-item flex-row
												flex-middle flex-stretch clickable" :class="p.style"
												@click.stop="setRoute( p.route )" :key="p.symbol">

												<div class="push-right text-clip flex-1">
													<span class="text-info">{{ p.coin }}</span>
												</div>

												<div class="push-right text-clip flex-1">
													 <span class="text-info">{{ p.price }}</span>
												</div>
												<div class="push-right text-clip flex-1 ">
													<span class="text-nowrap text-info">{{ p.volume }}</span>
												</div>

												<div class="push-right text-clip flex-1"> 
													<span class="text-nowrap item-color-buy">{{ p.change }}</span>
												</div>

												<div class="push-right text-clip flex-1 ">
													<span class="text-nowrap text-info">{{ p.name }}</span>
												</div>

											</div>

											<!-- if there are more items not included in list due to limit option -->
											

										</div>
									</section>
								</section>

								<!-- telegram -->
								<section btn-class="icon-submit" btn-name="VNDO Market">
									<section class="pagelist-wrap">
										<div class="container">
											<div class="pagelist-item flex-row flex-middle flex-stretch"
												v-if="VNDOList	.length">
												<div class="push-right text-clip flex-1"><span class="clickable"
													@click="$sorter.sortOrder( 'ticker', 'coin', 'asc' )">Coin</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'price', 'asc' )">Price</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'volume', 'desc' )">Volume</span></div>
												<div class="push-right text-clip flex-1"
													v-if="options.prices.chart"></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'change', 'desc' )">Change</span></div>
												<div class="push-right text-clip flex-1"><span class="clickable"
														@click="$sorter.sortOrder( 'ticker', 'name', 'desc' )">Name</span></div>
											</div>
											<div v-for="p in VNDOList	" class="pagelist-item flex-row
												flex-middle flex-stretch clickable" :class="p.style"
												@click.stop="setRoute( p.route )" :key="p.symbol">

												<div class="push-right text-clip flex-1">
													<span class="text-info">{{ p.coin }}</span>
												</div>

												<div class="push-right text-clip flex-1">
													 <span class="text-info">{{ p.price }}</span>
												</div>
												<div class="push-right text-clip flex-1 ">
													<span class="text-nowrap text-info">{{ p.volume }}</span>
												</div>

												<div class="push-right text-clip flex-1"> 
													<span class="text-nowrap item-color-buy">{{ p.change }}</span>
												</div>

												<div class="push-right text-clip flex-1 ">
													<span class="text-nowrap text-info">{{ p.name }}</span>
												</div>

											</div>

											<!-- if there are more items not included in list due to limit option -->
											

										</div>
									</section>
								</section>
							</Tabs>
						</div>
					</div>
					<div class="row push-top push-large">
						<div class="col-md-6 col-sm-6 col-xs-6 col-lg-6">
							<section class="pagelist-wrap">
								<div class="container">
									<h1 class="label-color">Buy BTC</h1>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Your balance:</span>
										</div>
										<div class="push-right text-clip flex-1">
											 <span class=" label-color1">2,500.00000000 USDT
											</span>
										</div>
									</div>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Lowest ask:</span>
										</div>
										<div class="push-right text-clip flex-1">
											 <span class=" label-color1">31,020.00000000 USDT
											</span>
										</div>
									</div>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Amount BTC:</span>
										</div>
										<div class="push-right text-clip flex-1">
											<div class="form-input">
												<!-- <span class="text-grey push-right">{{ d.token }}</span> -->
												<input class=" push-right text-clip" />
												<!-- <button class="icon-copy text-primary-hover"  title="Copy" v-tooltip></button> -->
											</div>
										</div>
									</div>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Price Per BTC:</span>
										</div>
										<div class="push-right text-clip flex-1">
											<div class="form-input">
												<!-- <span class="text-grey push-right">{{ d.token }}</span> -->
												<input class=" push-right text-clip" />
												<button class=" text-primary-hover"  v-tooltip>USDT</button>
											</div>
										</div>
									</div>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Total:</span>
										</div>
										<div class="push-right text-clip flex-1">
											 <span class=" label-color1">0.00000000 USDT
											</span>
										</div>
									</div>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Fee (0.2%):</span>
										</div>
										<div class="push-right text-clip flex-1">
											 <span class=" label-color1">0.00000000 BTC
											</span>
										</div>
									</div>
									<!-- if there are more items not included in list due to limit option -->
								</div>
							</section>
						</div>
						<div class="col-md-6 col-sm-6 col-xs-6 col-lg-6">
							<section class="pagelist-wrap">
								<div class="container">
									<h1 class="label-color">Sell BTC</h1>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Your balance:</span>
										</div>
										<div class="push-right text-clip flex-1">
											 <span class=" label-color1">1,000.00000000 BTC
											</span>
										</div>
									</div>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Lowest ask:</span>
										</div>
										<div class="push-right text-clip flex-1">
											 <span class=" label-color1">32,249.18000000 USDT
											</span>
										</div>
									</div>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Amount BTC:</span>
										</div>
										<div class="push-right text-clip flex-1">
											<div class="form-input">
												<!-- <span class="text-grey push-right">{{ d.token }}</span> -->
												<input class=" push-right text-clip" />
												<!-- <button class="icon-copy text-primary-hover"  title="Copy" v-tooltip></button> -->
											</div>
										</div>
									</div>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Price Per BTC:</span>
										</div>
										<div class="push-right text-clip flex-1">
											<div class="form-input">
												<!-- <span class="text-grey push-right">{{ d.token }}</span> -->
												<input class=" push-right text-clip" />
												<button class=" text-primary-hover"  v-tooltip>USDT</button>
											</div>
										</div>
									</div>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Total:</span>
										</div>
										<div class="push-right text-clip flex-1">
											 <span class=" label-color1">0.00000000 USDT
											</span>
										</div>
									</div>
									<div  class="pagelist-item flex-row
										flex-middle flex-stretch clickable" >
										<div class="push-right text-clip flex-1">
											<span class=" label-color1">Fee (0.2%):</span>
										</div>
										<div class="push-right text-clip flex-1">
											 <span class=" label-color1">0.00000000 USDT
											</span>
										</div>
									</div>
									<!-- if there are more items not included in list due to limit option -->
								</div>
							</section>
						</div>
					</div>
					<div class="row push-top push-large">
						<div class="col-md-6 col-sm-6 col-xs-6 col-lg-6">
							<section class="pagelist-wrap">
								<div class="container">
									<h1 class="label-color">Sell orders</h1>
									<div class="pagelist-item flex-row flex-middle flex-stretch"
										v-if="SellOrderList.length">
										<div class="push-right text-clip flex-1"><span class="clickable"
											@click="$sorter.sortOrder( 'ticker', 'date', 'asc' )">Date</span></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'price', 'asc' )">Price</span></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'amount', 'desc' )">Amount (BTC)</span></div>
										<div class="push-right text-clip flex-1"
											v-if="options.prices.chart"></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'total', 'desc' )">Total (USDT)</span></div>
									</div>
									<div v-for="p in SellOrderList" class="pagelist-item flex-row
										flex-middle flex-stretch clickable" :class="p.style"
										@click.stop="setRoute( p.route )" :key="p.symbol">

										<div class="push-right text-clip flex-1">
											<span class="text-info">{{ p.date }}</span>
										</div>

										<div class="push-right text-clip flex-1">
											 <span class="text-info">{{ p.price }}</span>
										</div>
										<div class="push-right text-clip flex-1 ">
											<span class="text-nowrap text-info">{{ p.amount }}</span>
										</div>

										<div class="push-right text-clip flex-1"> 
											<span class="text-nowrap text-info">{{ p.total }}</span>
										</div>


									</div>

									<!-- if there are more items not included in list due to limit option -->
									

								</div>
							</section>
						</div>
						<div class="col-md-6 col-sm-6 col-xs-6 col-lg-6">
							<section class="pagelist-wrap">
								<div class="container">
									<h1 class="label-color">Buy orders</h1>
									<div class="pagelist-item flex-row flex-middle flex-stretch"
										v-if="BuyOrderList.length">
										<div class="push-right text-clip flex-1"><span class="clickable"
											@click="$sorter.sortOrder( 'ticker', 'date', 'asc' )">Date</span></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'price', 'asc' )">Price</span></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'amount', 'desc' )">Amount (BTC)</span></div>
										<div class="push-right text-clip flex-1"
											v-if="options.prices.chart"></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'total', 'desc' )">Total (USDT)</span></div>
									</div>
									<div v-for="p in BuyOrderList" class="pagelist-item flex-row
										flex-middle flex-stretch clickable" :class="p.style"
										@click.stop="setRoute( p.route )" :key="p.symbol">

										<div class="push-right text-clip flex-1">
											<span class="text-info">{{ p.date }}</span>
										</div>

										<div class="push-right text-clip flex-1">
											 <span class="text-info">{{ p.price }}</span>
										</div>
										<div class="push-right text-clip flex-1 ">
											<span class="text-nowrap text-info">{{ p.amount }}</span>
										</div>

										<div class="push-right text-clip flex-1"> 
											<span class="text-nowrap text-info">{{ p.total }}</span>
										</div>

									</div>

									<!-- if there are more items not included in list due to limit option -->
									

								</div>
							</section>
						</div>
					</div>
					<div class="row push-top push-large">
						<div class="col-md-6 col-sm-6 col-xs-6 col-lg-6">
							<section class="pagelist-wrap">
								<div class="container">
									<h1 class="label-color">Your current active orders</h1>
									<div class="pagelist-item flex-row flex-middle flex-stretch"
										v-if="CurrentActiveList.length">
										<div class="push-right text-clip flex-1"><span class="clickable"
											@click="$sorter.sortOrder( 'ticker', 'date', 'asc' )">Date</span></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
											@click="$sorter.sortOrder( 'ticker', 'type', 'asc' )">Type</span></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'price', 'asc' )">Price</span></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'amount', 'desc' )">Amount (BTC)</span></div>
										<div class="push-right text-clip flex-1"
											v-if="options.prices.chart"></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'total', 'desc' )">Total (USDT)</span></div>
									</div>
									<div v-for="p in CurrentActiveList" class="pagelist-item flex-row
										flex-middle flex-stretch clickable" :class="p.style"
										@click.stop="setRoute( p.route )" :key="p.symbol">

										<div class="push-right text-clip flex-1">
											<span class="text-info">{{ p.date }}</span>
										</div>
										<div class="push-right text-clip flex-1">
											<span :class="p.type=='Buy'?'item-color-buy':'item-color-sell'">{{ p.type }}</span>
									   </div>
										<div class="push-right text-clip flex-1">
											 <span class="text-info">{{ p.price }}</span>
										</div>
										<div class="push-right text-clip flex-1 ">
											<span class="text-nowrap text-info">{{ p.amount }}</span>
										</div>

										<div class="push-right text-clip flex-1"> 
											<span class="text-nowrap text-info">{{ p.total }}</span>
										</div>


									</div>

									<!-- if there are more items not included in list due to limit option -->
									

								</div>
							</section>
						</div>
						<div class="col-md-6 col-sm-6 col-xs-6 col-lg-6">
							<section class="pagelist-wrap">
								<div class="container">
									<h1 class="label-color">Trade History</h1>
									<div class="pagelist-item flex-row flex-middle flex-stretch"
										v-if="TradeList.length">
										<div class="push-right text-clip flex-1"><span class="clickable"
											@click="$sorter.sortOrder( 'ticker', 'date', 'asc' )">Date</span></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
											@click="$sorter.sortOrder( 'ticker', 'type', 'asc' )">Type</span></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'price', 'asc' )">Price</span></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'amount', 'desc' )">Amount (BTC)</span></div>
										<div class="push-right text-clip flex-1"
											v-if="options.prices.chart"></div>
										<div class="push-right text-clip flex-1"><span class="clickable"
												@click="$sorter.sortOrder( 'ticker', 'total', 'desc' )">Total (USDT)</span></div>
									</div>
									<div v-for="p in TradeList" class="pagelist-item flex-row
										flex-middle flex-stretch clickable" :class="p.style"
										@click.stop="setRoute( p.route )" :key="p.symbol">

										<div class="push-right text-clip flex-1">
											<span class="text-info">{{ p.date }}</span>
										</div>
										<div class="push-right text-clip flex-1">
											<span :class="p.type=='Buy'?'item-color-buy':'item-color-sell'">{{ p.type }}</span>
									   </div>
										<div class="push-right text-clip flex-1">
											 <span class="text-info">{{ p.price }}</span>
										</div>
										<div class="push-right text-clip flex-1 ">
											<span class="text-nowrap text-info">{{ p.amount }}</span>
										</div>

										<div class="push-right text-clip flex-1"> 
											<span class="text-nowrap text-info">{{ p.total }}</span>
										</div>


									</div>

									<!-- if there are more items not included in list due to limit option -->
									

								</div>
							</section>
						</div>
					</div>
				</div>

			</div>
		</section>

		<!-- fallback section -->


		<!-- news list -->
		<section class="pagelist-wrap" id="newspage-list">
			<div class="container">

				<div class="pagelist-item flex-row flex-top flex-stretch" v-for="t in
					tweetsList" :key="t.id">
					<div class="push-right" :class="{ 'alert-bubble': t.isNew }">
						<img class="img-round" :src="t.avatar" width="68" height="68"
							:alt="t.handle" />
					</div>
					<div class="flex-1">
						<div class="flex-row flex-space push-bottom">
							<h3 class="text-clip clickable" @click="openLink(
								'https://twitter.com/'+ t.handle )">
								<span class="text-primary-hover">{{ t.name }}</span>
								<small class="text-smaller text-grey-hover">@{{ t.handle }}</small>
							</h3>
							<div class="text-clip if-small">
								<a class="text-secondary-hover" :href="t.link" target="_blank"
									title="View tweet" v-tooltip>{{ t.time | toElapsed( 'ago',
									true ) }}</a> &nbsp;
								<button type="button" class="icon-close text-danger-hover"
									title="Delete" @click="deleteTweet( t.id )" v-tooltip></button>
							</div>
						</div>
						<div class="text-small text-wrap" v-html="tweetHtml( t.text )"></div>
					</div>
				</div>

			</div>
		</section>

	</main>
</template>

<script>
import Tabs from './Tabs.vue';
import Search from './Search.vue';
import Dropdown from './Dropdown.vue';
import Toggle from './Toggle.vue';
import files from '../modules/files';
import twitterAccounts from '../configs/twitterAccounts';

// component
export default {

  // component list
  components: { Search, Dropdown, Toggle, Tabs },

  // component props
  props: {
    header: { type: Object, default() { return {} } },
    options: { type: Object, default() { return {} }, required: true },
    sortData: { type: Object, default() { return {} }, required: true },
    priceData: { type: Array, default() { return [] }, required: true },
    newsHandlers: { type: Array, default() { return [] }, required: true },
    newsEntries: { type: Array, default() { return [] }, required: true },
  },

  // component data
  data() {
    return {
      // filter options
      searchStr: '',
      searchHandle: '',
      // coins data
      totalTokens: 0,
      chartData: [],
      chartSort: 'count',
      chartOrder: 'desc',
      // count data
      newCount: 0,
      maxCount: 50,
    }
  },

  // watchers
  watch: {

    // update chart when options change
    options() {
      this.updateChart();
    },

    // update chart data when new tokens load from socket api
    priceData() {
      if ( this.priceData.length > this.totalTokens ) {
        this.totalTokens = this.priceData.length;
        this.updateChart();
      }
    },

    // update chart data when tweets change
    newsEntries() {
      this.updateChart();
    },
  },

  // computed methods
  computed: {
	ETHList() {
      let { market } = this.options.prices;
      let { column, order } = this.sortData.ticker;

      let limit = parseInt( this.options.prices.limit ) | 0;
      let regex = ( this.searchStr.length > 1 ) ? new RegExp( '^('+ this.searchStr +')', 'i' ) : null;
      let count = this.priceData.length;
      let list  = [
		  			{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"}
				];

      // filter the list
      // sort the list
      list = this.$utils.sort( list, column, order );

      // update paging totals
      let total = list.length;
      
      return list;
    },
	CurrentActiveList() {
      let { market } = this.options.prices;
      let { column, order } = this.sortData.ticker;

      let limit = parseInt( this.options.prices.limit ) | 0;
      let regex = ( this.searchStr.length > 1 ) ? new RegExp( '^('+ this.searchStr +')', 'i' ) : null;
      let count = this.priceData.length;
      let list  = [
		  			{"date":"17/07 09:11","type":"Buy","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","type":"Buy","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","type":"Sell","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","type":"Buy","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","type":"Sell","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"}
				];
      // filter the list
      // sort the list
      list = this.$utils.sort( list, column, order );

      // update paging totals
      let total = list.length;
      
      return list;
    },
	TradeList() {
      let { market } = this.options.prices;
      let { column, order } = this.sortData.ticker;

      let limit = parseInt( this.options.prices.limit ) | 0;
      let regex = ( this.searchStr.length > 1 ) ? new RegExp( '^('+ this.searchStr +')', 'i' ) : null;
      let count = this.priceData.length;
      let list  = [
		  			{"date":"17/07 09:11","type":"Buy","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","type":"Buy","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","type":"Sell","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","type":"Buy","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","type":"Sell","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"}
				];
      // filter the list
      // sort the list
      list = this.$utils.sort( list, column, order );

      // update paging totals
      let total = list.length;
      
      return list;
    },
	SellOrderList() {
      let { market } = this.options.prices;
      let { column, order } = this.sortData.ticker;

      let limit = parseInt( this.options.prices.limit ) | 0;
      let regex = ( this.searchStr.length > 1 ) ? new RegExp( '^('+ this.searchStr +')', 'i' ) : null;
      let count = this.priceData.length;
      let list  = [
		  			{"date":"17/07 09:11","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"}
				];
      // filter the list
      // sort the list
      list = this.$utils.sort( list, column, order );

      // update paging totals
      let total = list.length;
      
      return list;
    },
	BuyOrderList() {
      let { market } = this.options.prices;
      let { column, order } = this.sortData.ticker;

      let limit = parseInt( this.options.prices.limit ) | 0;
      let regex = ( this.searchStr.length > 1 ) ? new RegExp( '^('+ this.searchStr +')', 'i' ) : null;
      let count = this.priceData.length;
      let list  = [
		  			{"date":"17/07 09:11","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"},
					{"date":"17/07 09:11","price":"31,676.62000000","amount":"0.00637800","total":"202.03348236"}
				];
      // filter the list
      // sort the list
      list = this.$utils.sort( list, column, order );

      // update paging totals
      let total = list.length;
      
      return list;
    },
	BTCList() {
      let { market } = this.options.prices;
      let { column, order } = this.sortData.ticker;

      let limit = parseInt( this.options.prices.limit ) | 0;
      let regex = ( this.searchStr.length > 1 ) ? new RegExp( '^('+ this.searchStr +')', 'i' ) : null;
      let count = this.priceData.length;
      let list  = [
		  			{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"}
				];

      // filter the list
      // sort the list
      list = this.$utils.sort( list, column, order );

      // update paging totals
      let total = list.length;
      
      return list;
    },
	VNDOList() {
      let { market } = this.options.prices;
      let { column, order } = this.sortData.ticker;

      let limit = parseInt( this.options.prices.limit ) | 0;
      let regex = ( this.searchStr.length > 1 ) ? new RegExp( '^('+ this.searchStr +')', 'i' ) : null;
      let count = this.priceData.length;
      let list  = [
		  			{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"}
				];

      // filter the list
      // sort the list
      list = this.$utils.sort( list, column, order );

      // update paging totals
      let total = list.length;
      
      return list;
    },
	USDTList() {
      let { market } = this.options.prices;
      let { column, order } = this.sortData.ticker;

      let limit = parseInt( this.options.prices.limit ) | 0;
      let regex = ( this.searchStr.length > 1 ) ? new RegExp( '^('+ this.searchStr +')', 'i' ) : null;
      let count = this.priceData.length;
      let list  = [
		  			{"coin":"BTC","price":"63,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"},
					{"coin":"BTC","price":"62,488.75000000","volume":"60,108.03801000","change":"-1.058%","name":"Bitcoin"}
				];

      // filter the list
      // sort the list
      list = this.$utils.sort( list, column, order );

      // update paging totals
      let total = list.length;
      
      return list;
    },

    // get sorted chart list
    chartList() {
      let { column, order } = this.sortData.sentiment;
      let list = this.chartData.slice(); // copy
      list = this.$utils.sort( list, column, order ); // sort
      return list;
    },

    // get filtered list
    tweetsList() {
      let { fullword, fullcase } = this.options.search;
      let list = this.newsEntries.slice(); // copy

      if ( this.searchHandle ) {
        list = list.filter( t => t.handle === this.searchHandle );
      }
      if ( this.searchStr && this.searchStr.length > 1 ) {
        list = this.$utils.search( list, 'text', this.searchStr, fullword, fullcase );
      }
      if ( this.options.news.max ) {
        list = list.slice( 0, this.options.news.max );
      }
      return list;
    },

    // build twitter accounts list from handler list with checking indicator
    accountsList() {
      let list = this.newsHandlers.map( tw => {
        let { uid, handle, name, avatar, url, last, fetching, error } = tw.getData();
        let active = ( handle === this.searchHandle );
        let count = this.newsEntries.filter( t => t.handle === handle ).length;
        return { uid, handle, name, avatar, url, last, error, active, fetching, count };
      });
      return this.$utils.sort( list, 'count', 'desc' );
    },

    // sort-by label for buttons, etc
    filterLabel() {
      let l = this.newsHandlers.length;
      let t = this.newsHandlers.filter( tw => tw.handle === this.searchHandle ).shift();
      if ( t && t.handle ) return '@'+ t.handle;
      return 'All Sources ('+ l +')';
    },

    // calculate default message for sentiment chart
    sentimentInfoText() {
      // no twitter handles to fetch from
      if ( !this.newsHandlers.length ) {
        return 'Not tracking any Twitter accounts, use the Sources menu above to track accounts...';
      }
      // option enabled, but no token data loaded yet
      if ( this.options.news.enabled && !this.priceData.length ) {
        return 'Currently waiting for tokens to load from the Binance socket API...';
      }
      // option enabled, but no tweets data loaded yet
      if ( this.options.news.enabled && !this.newsEntries.length ) {
        return 'Currently waiting for tweets data to load for tracked Twitter accounts...';
      }
      // option to fetch disabled and there are no tweets to scan
      if ( !this.options.news.enabled && !this.newsEntries.length ) {
        return 'No tweets loaded, use the <i class="icon-config"></i> Gear icon to enable fetching.';
      }
    },
  },

  // custom methods
  methods: {

    // open external link
    openLink( link ) {
      window.open( link, '_blank' );
    },

    // apply options
    saveOptions() {
      this.$opts.saveOptions( this.options );
    },

    // apply filters
    applyFilters( search, handle ) {
      this.searchStr = String( search || '' ).trim();
      this.searchHandle = String( handle || '' ).trim();
    },

    // reset filters
    resetFilters() {
      this.searchStr = '';
      this.searchHandle = '';
    },

    // scan tweets against list of tokens from api and build sentiment analysis data for chart
    updateChart() {
      let { fullword, fullcase } = this.options.search;
      let tokens = [];
      let data = [];

      // build unique list of tokens from binance api
      this.priceData.forEach( p => {
        if ( tokens.filter( t => t.token === p.token ).length ) return;
        let { token, name } = p;
        let asset = ( token === 'BTC' ) ? 'USDT' : 'BTC';
        let route = '/symbol/'+ token + asset;
        tokens.push( { token, name, route } );
      });
      // add other things to the list
      if ( this.priceData.length ) {
        tokens.push( { token: 'Crypto', name: 'Cryptocurrency', route: '/symbol/BTCUSDT' } );
        tokens.push( { token: 'XBT', name: 'BTC Contract', route: '/symbol/BTCUSDT' } );
      }
      // build sentiment
      tokens.forEach( p => {
        let token  = p.token;
        let name   = p.name;
        let route  = p.route;
        let search = token +'|'+ name;
        let list   = this.$utils.search( this.newsEntries, 'text', search, fullword, fullcase );
        let count  = list.length;
        if ( !count ) return;
        let text   = list.reduce( ( a, t ) => a += ' '+ t.text, '' ).trim();
        let sdata  = this.$sentiment.analyze( text );
        let { score, positive, negative, comparative, sign, word, styles, sentiment } = sdata;
        data.push( { token, name, search, route, count, score, styles, sentiment } );
      });
      // calculate percent
      let max = data.reduce( ( m, d ) => d.count > m ? d.count : m, 0 );
      this.chartData = data.map( d => {
        let ratio = ( max > 0 ) ? ( d.count / max ) : 0.1;
        let barPercent = Math.round( ratio * 100 );
        let barColor = 'bg-grey';
        if ( barPercent > 20 ) { barColor = 'bg-bright'; }
        if ( barPercent > 40 ) { barColor = 'bg-secondary'; }
        if ( barPercent > 60 ) { barColor = 'bg-primary'; }
        return Object.assign( d, { barPercent, barColor } );
      });
    },

    // convert links inside a tweet into html
    tweetHtml( text ) {
      return this.$utils.linkUrl( text );
    },

    // when a new entry is added to news list
    onNewsEntry( tweet ) {
      let { time, handle, name, text, avatar, link } = tweet;
      let secs    = ( Date.now() - time ) / 1000;
      let mins    = Math.floor( secs / 60 );
      let elapsed = this.$utils.elapsed( secs );
      let isaway  = ( !document.hasFocus() );
      let isnew   = ( Math.floor( secs / 60 ) <= 60 ); // within 1hr

      // remove html and urls from tweet text
      text = this.$utils.stripHtml( text, true );
      if ( !text ) return;

      // show tweet notification only if enabled and away
      if ( this.options.news.notify && isnew && isaway ) {
        text = 'Tweeted '+ elapsed +' ago... \n\n' + text;
        this.$notify.add( '@'+ handle, text, avatar, link );
      }
      // always send notification via api if enabled
      if ( this.options.news.send ) {
        let info = `<a href="${ link }">${ text }</a>`;
        this.$messenger.add( name, info, avatar );
      }
    },

    // export list of account handles as json file
    exportAccounts() {
      let list = this.newsHandlers.map( t => t.handle );
      files.exportData( 'binance_watch_news_sources', list );
    },

    // import list of account handles from json file
    importAccounts() {
      files.importData( accounts => {
        let total = accounts.length | 0;
        let saved = this.$news.importAccounts( accounts, true, true );
        this.$bus.emit( 'showNotice', 'Imported '+ saved +'/'+ total +' twitter accounts.', 'success' );
      });
    },

    // fetch tweets for an account by handle
    fetchByHandle( handle ) {
      if ( this.$news.fetchByHandle( handle ) ) {
        this.$bus.emit( 'showNotice', 'Fetching latest tweets from @'+ handle +'...', 'success' );
      }
    },

    // remove single tweet from list by id
    deleteTweet( id ) {
      if ( !this.$news.blockTweet( id ) ) return;
      this.$bus.emit( 'showNotice', 'News entry has been removed.', 'success' );
    },

    // flush list of saved tweets from store
    flushTweets() {
      if ( !confirm( 'Remove all news entries?' ) ) return;
      this.$news.flushTweets();
      this.$bus.emit( 'showNotice', 'All news entries have been deleted.', 'success' );
    },

    // handle adding accounts from a form
    accountFormHandler( e ) {
      if ( !e || !e.target ) return;

      let handle = String( e.target.handle.value || '' ).replace( /[^\w]+/g, '' ).trim();
      if ( !handle ) return this.$bus.emit( 'showNotice', 'Please enter a valid twitter handle.', 'warning' );

      let added = this.$news.trackAccount( handle, true, true );
      if ( added ) { this.$bus.emit( 'showNotice', 'Started tracking tweets from @'+ handle +'.', 'success' ); }
      else { this.$bus.emit( 'showNotice', 'Could not add account @'+ handle +'.', 'warning' ); }

      this.resetFilters();
      e.target.reset();
    },

    // remove instance of Twitter handler from list
    removeTwitterHandler( handle ) {
      if ( !confirm( 'Stop tracking tweets from @'+ handle +'?' ) ) return;

      let removed = this.$news.untrackAccount( handle );
      if ( removed ) { this.$bus.emit( 'showNotice', 'Stopped tracking tweets from @'+ handle +'.', 'success' ); }
      else { this.$bus.emit( 'showNotice', 'Could not remove account @'+ handle +'.', 'warning' ); }

      this.resetFilters();
    },

    // mark tweets as viewed
    resetTweets() {
      if ( document.visibilityState === 'visible' ) return;
      this.$news.resetTweets(); // reset when hidden
    },
  },

  // on component beforeMount
  beforeMount() {
    this.$news.on( 'tweet', this.onNewsEntry );
    this.$news.importAccounts( twitterAccounts ); // default accounts
  },

  // on component mounted
  mounted() {
    this.$news.loadAccounts(); // load saved accounts
    this.$news.loadTweets(); // load saved tweets
    document.addEventListener( 'visibilitychange', this.resetTweets );
  },

  // on component destroyed
  destroyed() {
    document.removeEventListener( 'visibilitychange', this.resetTweets );
  },
}
</script>
