# p2pool
Decentralized pool for Monero mining

# Pool mining vs Solo mining vs P2Pool mining

Here's the comparison table of the different ways of mining. While pool mining is the easiest to setup, it centralizes Monero network and pool admin gets full power over your hashrate and your unpaid funds. Solo mining is 100% independent and the best for the network. P2Pool mining has all the advantages of solo mining, but also makes regular payouts possible.

Pool type |	Payouts |	Fee |	Min. payout |	Centralized? |	Stability |	Control |	Setup
 ---- | ----- | ----- | ----- | ----- | ----- | ----- | ------  
Centralized pool |	Regular |	0-3% |	0.001-0.01 XMR |	Yes |	Less stable due to pool server outages |	Pool admin controls your mined funds, what you mine and can execute network attacks |	Only miner software is required
Solo |	Rare |	0% |	0.6 XMR or more |	No |	As stable as your Monero node |	100% under your control |	Monero node + optional miner
P2Pool |	Regular |	0% |	~0.0003 XMR |	No |	As stable as your Monero node |	100% under your control |	Monero node + P2Pool node + miner

# Features

 * Decentralized: no central server that can be shutdown/blocked. P2Pool uses a separate blockchain to merge mine with Monero. Pool admin can't go rogue or be pressured to do an attack on the network because there is no pool admin!
 * Permissionless: there is no one to decide who can mine on the pool and who can't.
 * Trustless: there is no pool wallet, funds are never in custody. All pool blocks pay out to miners immediately.
 * PPLNS payout scheme
 * 0% fee
 * 0 XMR payout fee
 * ~0.0003 XMR minimal payout
 * Fast block times, down to 1 second
 * Uncle blocks are supported to avoid orphans - all your shares will be accounted for!
 * Configurable PPLNS window size and block time
 * Advanced mempool picking algorithm, it creates blocks with better reward than what monerod solo mining does
 * Password protected private pools

# How PPLNS works in P2Pool

First you need to find a pool share. This share will stay in PPLNS window for 2160 pool blocks (6 hours). The moment P2Pool finds a Monero block and you have at least 1 pool share in PPLNS window, you'll get a payout! Monero block reward is split between all miner wallets in PPLNS window. Each miner gets a part of block reward proportional to the total difficulty of his/her shares in PPLNS window.

NOTE If P2Pool doesn't have enough hashrate to find Monero blocks faster than every 6 hours on average (~15 MH/s), not all your pool shares will result in a payout. Even if pool hashrate is higher, bad luck can sometimes result in a share going through PPLNS window without a payout. But in the long run it will be compensated by other shares receiving multiple payouts - your payouts will average out to what you'd get with regular pool mining.

# Default P2Pool parameters

 * Block time: 10 seconds
 * PPLNS window: 2160 blocks (6 hours)
 * Minimum payout = Monero block reward/2160, ~0.0003 XMR

# How to mine on P2Pool
## General Considerations

 * In order to mine on P2Pool, a synced Monero node using monerod v0.17.3.0 or newer is required. If you do not currently have one configured, you can find instructions to do so here.
 * It is highly recommended that you create a separate restricted user account for mining. While P2Pool has been battle-tested for a long time now, any software may have unknown bugs/vulnerabilities.
 * You have to use a primary wallet address for mining. Subaddresses and integrated addresses are not supported, just like with monerod solo mining.
 * Starting from P2Pool v1.7, you can add the --mini parameter to your P2Pool command to connect to the p2pool-mini sidechain. Note that it will also change the default p2p port from 37889 to 37888.
 * Check that ports 18080 (Monero p2p port) and 37889/37888 (P2Pool/P2Pool mini p2p port) are open in your firewall to ensure better connectivity. If you're mining from a computer behind NAT (like a router) you could consider forwarding the ports to your local machine.
 * You can connect multiple miners to the same P2Pool node. The more the better!
 * The below steps assume that you run everything on the same machine. If it's not the case, change 127.0.0.1 to appropriate IP addresses for your setup.
 * It is highly recommended to create a new mainnet wallet for P2Pool mining because wallet addresses are public on P2Pool.

