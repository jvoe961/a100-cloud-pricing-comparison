# A100 Cloud Pricing: Hourly Rates Compared Across 18 Providers, the Cheapest Ways to Rent an 80GB Card, and Where Vultr's $2.40/hr Fits In

Renting an NVIDIA A100 in the cloud costs anywhere from **$1.09 to $5.07 per GPU-hour** on demand right now, and the spread has almost nothing to do with the chip itself. It comes down to who owns the hardware and how they sell it: marketplace hosts and budget clouds sit between roughly $1.09 and $1.79 for an 80GB card, mid-tier clouds like Vultr charge **$2.40**, and the hyperscalers bill $3.43 to $5.03 for the same silicon. This guide walks through current A100 cloud pricing across 18 providers, what an A100 actually costs per job, where spot rates drop below $1.70, and when Vultr's rate is the sensible middle ground versus the cheapest marketplace listings.

> **Quick take:** For a single A100 80GB on demand, marketplace hosts are cheapest — Thunder Compute tracks $1.09/hr and Vast.ai's median is $1.63. Vultr's fixed **$2.40/hr** undercuts AWS by about 30% and Google Cloud by about 52%, without the per-host variability of a marketplace. Spot rates start at $0.89. 👉 [Check the current rate on Vultr's GPU price list](https://www.vultr.com/pricing/?ref=7268283#cloud-gpu)

## What A100 cloud pricing looks like right now

On demand, in US regions, an A100 80GB rents for between $1.19 and $5.07 per GPU-hour, and the median across 40 tracked providers is **$1.77** according to the getdeploying tracker cited in Beam's September roundup. Here is the full field, compiled from the most recently published comparisons (September–October 2026):

| Provider | GPU / SKU | On-demand $/GPU-hr | Notes |
| --- | --- | --- | --- |
| Thunder Compute | A100 80GB | $1.09 | Lowest tracked on-demand rate |
| Vast.ai | A100 80GB | $1.63 | Median of 3 verified US/CA hosts; range $1.21–$1.76 |
| RunPod | A100 80GB | $1.19–$1.79 | Community Cloud PCIe at the low end; Secure Cloud higher |
| Crusoe Cloud | A100 80GB | $2.00 |  |
| Vultr | A100 80GB | $2.40 |  |
| Modal | A100 80GB | $2.50 |  |
| CoreWeave | 8× A100 80GB | $2.70 | Per-GPU share of an 8-GPU node |
| Lambda | A100 SXM 80GB | $2.79 | 8-GPU instances only |
| Paperspace | A100 80GB | $3.18 |  |
| AWS EC2 | p4de.24xlarge | $3.43 | Per-GPU share of an 8-GPU node |
| Azure | Standard_NC24ads_A100_v4 | $3.67 | Cheapest US region; $3.67–$4.78 across 8 US options |
| Oracle Cloud | BM.GPU.A100-v2.8 | $4.00 |  |
| Google Cloud | a2-ultragpu-1g | $5.03 | us-central1; up to $6.04 in other US regions |

A few of these rates deserve SKU-level detail, because card type and billing granularity change the number:

| Provider | Card | On-demand $/hr | Spot $/hr | Notes |
| --- | --- | --- | --- | --- |
| RunPod (Community Cloud) | A100 80GB PCIe | $1.19 | — | Third-party hosts; SXM $1.39; Secure Cloud $1.59 |
| Hyperstack | A100 80GB PCIe | $1.35 | $1.08 | Per-minute billing |
| Beam | A100 80GB SXM4 | $1.36 | — | Machine price includes vCPU, RAM, and NVMe |
| Spheron | A100 80GB PCIe | $1.43 | $1.13 | 20-minute minimum |
| Runcrate | A100 80GB SXM4 | $1.49 | — | Per-second billing |
| Verda | A100 SXM4 80GB | $1.79 | $0.89 |  |

One thing none of the price tables tells you: these numbers move. Thunder Compute charged $0.78/hr for the same 80GB card in December 2025 and $1.09 by October 2026; Lambda's 40GB card went from $1.29 to $1.99 over the same stretch. Any price you read in an article, including this one, is a snapshot — confirm the rate on the provider's page before you commit to a long job.

## Vultr's A100 pricing, and where $2.40 an hour sits

Vultr rents the A100 80GB at **$2.40 per GPU-hour on demand**, hourly billing, US region, with no reserved-instance commitment applied to that figure. In practice that puts it in the middle tier of the market — the one most people actually should be shopping in:

| Instance | GPU | On-demand price | Billing | Link |
| --- | --- | --- | --- | --- |
| A100 (single GPU) | NVIDIA A100 80GB | $2.40/GPU-hr | Hourly, on demand | [See the current rate on Vultr's GPU price list](https://www.vultr.com/pricing/?ref=7268283#cloud-gpu) |
| Other GPU families | H100 and others | Listed on the price list | Hourly | [Open Vultr's full GPU price list](https://www.vultr.com/pricing/?ref=7268283#cloud-gpu) |

Against the rest of the field, $2.40 works out to roughly 30% less than AWS's p4de rate ($3.43), about 52% less than Google Cloud's a2-ultragpu-1g ($5.03), and it beats Oracle ($4.00) by a wide margin too. In the other direction, it runs about 2.2× Thunder Compute's $1.09 and about 47% above Vast.ai's $1.63 median.

So what is the premium actually buying? With a marketplace host you're renting from individual third parties whose reliability, storage setup, and billing quirks vary host by host — Vast.ai's pricing, for example, is quoted as compute plus 100GB of storage with bandwidth billed separately. Vultr is a single vendor with its own inventory and data centers across the US, Europe, Asia, and Australia, which matters when a job needs to run unattended or sit close to your existing infrastructure. If the price difference across a short job is a few dollars, that consistency is usually worth it; on a month-long continuous workload, the ~$950 gap versus the cheapest tracked rate is real money and worth thinking about honestly. 👉 [Compare Vultr's hourly rate against your workload size on its pricing page](https://www.vultr.com/pricing/?ref=7268283#cloud-gpu)

## What an A100 80GB really costs per job

Sticker prices hide the actual answer, so run the workloads. The two-hour and 100-hour figures below come straight from the published comparisons; the monthly row is computed from each provider's hourly rate. All of it excludes storage, networking, and egress fees.

| Workload | Vultr ($2.40/hr) | Thunder Compute ($1.09/hr) | AWS ($3.43/hr) | Google Cloud ($5.03/hr) |
| --- | --- | --- | --- | --- |
| 2 hours | $4.79 | $2.18 | $6.86 | $10.06 |
| 100 hours | $240 | $109 | $343.09 | $502.77 |
| 730 hours (~1 month) | $1,752 | $795.70 | $2,503.90 | $3,671.90 |

Two things jump out. First, small jobs barely notice the difference — a two-hour fine-tuning run costs $4.79 on Vultr versus $10.06 on Google Cloud, which is pocket change either way. Second, the gap compounds fast: keep an A100 running around the clock for a month and the spread between the cheapest tracked provider and GCP is nearly $2,900. That's the number that should drive your choice, not the per-hour rate in isolation. 👉 [Check how your expected runtime translates into cost on Vultr's GPU price list](https://www.vultr.com/pricing/?ref=7268283#cloud-gpu)

## Spot rates: the cheapest A100s anywhere

The lowest A100 prices on the market are spot rates, and they start at **$0.89/hr** for Verda's A100 SXM4 80GB. Hyperstack lists the 80GB PCIe at $1.08 spot and Spheron at $1.13, with RunPod historically discounting spot 40–50% below on-demand (roughly $0.70–$0.90 in practice, per Deploybase's March data).

The hyperscalers' spot prices are less publicized but competitive once you normalize for node size. DevZero's instance tracker puts Google Cloud's a2-highgpu-1g at $1.56 spot (40GB card, down from $3.67) and a2-ultragpu-1g at $1.66 spot (80GB, down from $5.03). AWS's p4de.24xlarge — eight A100 80GBs — lists at $12.13/hr on spot, which works out to roughly **$1.51 per GPU-hour**, less than most providers' on-demand single-card rate. Across its tracked configurations, DevZero logs maximum spot savings of 82% versus on-demand.

The catch is obvious but worth stating: spot capacity can be reclaimed mid-job. This is the right lane for batch inference, checkpointed training, and anything resumable. It's the wrong lane for a fine-tuning run you can't afford to restart.

## 80GB vs 40GB: which one should you rent?

Rent the 80GB card in almost every case — it frequently costs the same or less than the 40GB while doubling the memory. Thunder Compute's 80GB at $1.09 undercuts Paperspace's 40GB ($3.09) and Google Cloud's 40GB ($3.67) outright, and DevZero lists GCP's a2-ultragpu-1g at $5.03 against $3.67 for the 40GB a2-highgpu-1g, which is a smaller gap than you'd expect for twice the VRAM.

The 40GB only wins when it's priced well below the 80GB option, and there's exactly one reliable place where that happens: the Vast.ai marketplace, where the 40GB median across nine verified US/CA hosts is $0.62/hr (range $0.44–$0.99). For short jobs on small models, that's legitimately the cheapest A100 access anywhere.

The technical case for 80GB holds up too. The 80GB SXM card carries 2,039 GB/s of memory bandwidth against the 40GB's 1,555 GB/s, and at two bytes per parameter, 80GB holds roughly 40B parameters of BF16 weights before activations and KV cache — enough headroom for LoRA and QLoRA fine-tuning of mid-size models, larger batch sizes, and practical MIG partitioning if you want to slice one card across tenants.

## Is the A100 still worth renting next to an H100?

For budget-priced workloads, yes — with one clear disqualifier. The A100, which launched in August 2020, has no FP8 support and no Transformer Engine, so if your stack depends on FP8, the decision makes itself. Otherwise the math from Beam's comparison is the useful one: their H100 PCIe rents for $1.83 against $1.36 for the A100 80GB SXM4, about 35% more. The H100 only wins per job if it runs more than 1.35× faster. Compute-bound training often does. Low-batch BF16 inference often doesn't, because the H100 PCIe's memory bandwidth is close to the A100 SXM4's.

One more exit ramp: if your model fits in 48GB, an L40S rents for less per hour than either card and may be the better budget pick entirely.

## Three things to check before you book

Hourly list prices are only the starting point. Three details change what you'll actually pay:

1. **Region.** The published rates are US-region; rates elsewhere typically differ by 5–20%. Azure's A100 ranges from $3.67 to $4.78 across its eight US options, and Google Cloud's a2-ultragpu-1g runs $5.03 to $6.04 across ten. Check your specific region's calculator before assuming you'll get the headline number.
2. **Node math.** Several headline figures are per-GPU shares of 8-GPU nodes — AWS, Oracle, CoreWeave, and Lambda all work this way for at least part of their A100 lineup. Lambda's $2.79/GPU SXM 80GB, for instance, means roughly $22.32 per hour for the whole node. Fine for distributed training; wasteful if you need one card.
3. **Tracker disagreements.** These comparison sites don't always agree. DevZero's tracker lists Azure's single-GPU Standard_NC24ads_A100_v4 (A100 80GB) at $0.735/hr in West US 2, while Thunder Compute's October table shows $3.67 for the same SKU in its cheapest US region — a five-fold gap on paper. One of those listings is off or measuring something different, and the only tiebreaker is Azure's own calculator. The broader lesson: treat any single table, including this one, as a starting quote.

## FAQ

**How much does an A100 cost per hour?**
On demand, an A100 80GB runs $1.19–$5.07 per GPU-hour across major providers, with a market median of $1.77. The cheapest tracked on-demand rate is $1.09; hyperscalers charge $3.43–$5.03.

**How much is an A100 per month running continuously?**
From about $796/month at the cheapest tracked rate to roughly $3,672 on Google Cloud, based on 730 hours. Vultr works out to $1,752/month at $2.40/hr. Storage and bandwidth are extra on top of all of these.

**What's the cheapest way to rent an A100?**
Spot, starting at $0.89/hr (Verda's SXM4 80GB). On demand, the cheapest tracked 80GB is $1.09, and Vast.ai's 40GB median of $0.62 is the lowest A100 price of any variant — if your model fits in 40GB and you accept marketplace variability.

**Does Vultr rent A100 GPUs?**
Yes. Vultr lists the A100 80GB at $2.40 per GPU-hour on demand with hourly billing, alongside other GPU families including the H100 on its price list.

## Picking the right A100 rental

Match the rental to the job, in order of what you actually need:

- **Lowest possible hourly rate, variability acceptable:** marketplace and budget tiers at $1.09–$1.63 (Thunder Compute, Vast.ai, RunPod's Community Cloud).
- **Interruption-tolerant batch work:** spot rates from $0.89 to about $1.66.
- **A single fixed vendor, standard cloud workflow, and still well under hyperscaler pricing:** Vultr's $2.40/hr A100 80GB — 30%+ cheaper than AWS with none of the per-host roulette.
- **Multi-GPU NVLink training:** an 8-GPU SXM node from Lambda or CoreWeave, and accept that you're paying for all eight cards.

Before clicking buy on any of them, confirm two things: the price in *your* region, and whether the rate you're quoted is one card or a share of an eight-card node. Those two checks catch most billing surprises. If the middle-tier route sounds right for your workload, 👉 [deploy an A100 80GB on Vultr](https://bit.ly/VulTR) and start with a short job to validate the setup before scaling up.
