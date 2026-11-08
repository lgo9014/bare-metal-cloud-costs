# Bare Metal Cloud Providers: Hourly or Committed? What a Server Really Costs and How to Choose One (Plan Table + Checklist)

Three things move a bare metal bill further than anything in the spec sheet: how you buy capacity (reserved monthly or hourly on demand), whether a hypervisor sits between your workload and the CPU, and what the headline price already covers in bandwidth, IPv4 addresses and DDoS filtering. Get those wrong and a $90 server turns into a $300 invoice.

Spin Servers is one of the smaller names in this market, and its shape is easy to describe: fixed monthly prices on the KVM VPS line starting at $39.00, bare metal dedicated servers and private clouds quoted per configuration, hardware the company says it owns, and dedicated servers offered in Dallas and Silicon Valley. What follows is what's actually published, the hourly-versus-committed arithmetic most comparison posts skip, and the checks that decide whether a quote is genuinely cheap.

> **Quick pick**
> - One database, game server, build runner or GPU box that stays on all month: get a quote for your exact CPU, RAM and NVMe spec rather than picking from a list. 👉 [Request a Spin Servers bare metal quote](https://bit.ly/Spinservers)
> - A handful of app servers behind a load balancer: the KVM VPS line starts at $39.00 USD/month for 6 vCPU, 8 GB DDR4, 120 GB RAID-10 SSD and 8 TB of monthly transfer.
> - Several machines that need to talk over a private network, with optional managed firewalls: the bare metal private cloud is priced around your topology, not a fixed plan.

## Spin Servers plans: what has a price tag and what doesn't

Spin Servers publishes prices on the VPS line. Bare metal dedicated servers and the bare metal private cloud are built to order and quoted per configuration, which is what you'd expect from a provider assembling servers from its own hardware inventory instead of reselling a fixed catalogue. If you find a "starting at" figure for the bare metal line in a forum thread or on another affiliate page, treat it as a lead rather than a price. The number that binds is the one on your quote.

The VPS side is where line-by-line comparison is possible.

| Plan | Core configuration | Price as published | Billing | Order |
| --- | --- | --- | --- | --- |
| KVM 6 vCPU / 8 GB | 6 vCPU, 8 GB DDR4, 120 GB RAID-10 SSD, 8 TB/mo transfer, 1 Gbps port, 1 IPv4 + 1 IPv6 | $39.00 USD/mo | Monthly | [Order the 6 vCPU plan](https://bit.ly/Spinservers) |
| KVM 8 vCPU / 8 GB | 8 vCPU, 8 GB DDR4, 160 GB RAID-10 SSD, 10 TB/mo transfer, 1 Gbps port, 1 IPv4 + 1 IPv6 | Shown on the plan card | Monthly | [Check the 8 vCPU configuration](https://bit.ly/Spinservers) |
| KVM 12 vCPU / 12 GB | 12 vCPU, 12 GB DDR4, 160 GB RAID-10 SSD, 10 TB/mo transfer, 1 Gbps port, 1 IPv4 + 1 IPv6 | Shown on the plan card | Monthly | [Check the 12 vCPU configuration](https://bit.ly/Spinservers) |
| KVM 16 vCPU / 16 GB | Intel Xeon, 16 GB DDR4, 320 GB RAID-10 SSD, 15 TB/mo transfer, 1 Gbps port, 1 IPv4 + 1 IPv6 | Shown on the plan card | Monthly | [Check the 16 vCPU configuration](https://bit.ly/Spinservers) |
| Advanced 32 vCPU / 32 GB | Intel Xeon, 32 GB RAM, 500 GB SSD, 20 TB/mo transfer, 1 Gbps port, 1 IPv4 + 1 IPv6 | Shown on the plan card | Monthly | [Check the 32 vCPU configuration](https://bit.ly/Spinservers) |
| Bare metal dedicated server | Built to order: CPU, memory and storage chosen for the workload, Dallas and Silicon Valley | Quoted per configuration | Confirmed in the quote | [Price a dedicated server](https://bit.ly/Spinservers) |
| Bare metal private cloud | Dedicated servers plus private networking, optional network management and managed hardware firewalls | Quoted per configuration | Confirmed in the quote | [Price a private cloud build](https://bit.ly/Spinservers) |

The VPS page also advertises a "from $62.00 USD monthly" tier next to its higher-core configurations; check the individual plan card before ordering so you know which configuration that price belongs to. All bare metal and private cloud pricing is quote-based, so confirm the current figure with sales for your spec.

Two details in that table matter as much as the prices. Every VPS plan includes both an IPv4 and an IPv6 address and a 1 Gbps port, with transfer allowances running from 8 TB to 20 TB a month depending on size. Port 25 is closed by default on all VPS. You can ask for it to be opened with a justification, and Spin Servers reserves the right to refuse. If you plan to send transactional mail straight from the box, plan for a relay or get a decision on port 25 before you order.

## Bare metal cloud, dedicated server and VPS: where the cost difference comes from

A bare metal cloud is a dedicated physical server sold with cloud-style provisioning: API or CLI access, fast reinstallation, and sometimes hourly billing. The hardware is single-tenant either way. What separates a bare metal cloud from a traditional dedicated server is mostly how quickly you can get one and how much of its lifecycle you can automate. Traditional dedicated hosting still often means a ticket, a setup fee and a manual OS install.

A VPS sits on the other side of that line: virtual machines on shared physical hosts. Cheaper per core, and perfectly adequate for plenty of application servers, but the other tenants on the host remain a variable you don't control.

What you gain from skipping the hypervisor is concrete: CPU and memory that aren't shared with a virtualization layer, lower I/O latency because there's one less abstraction between the disk and the application, direct access to the hardware, and a smaller attack surface with fewer layers between your application and the firmware. Oracle's bare metal shapes take the idea furthest, running with no hypervisor and no management agent installed, offloading infrastructure functions to its Acceleron cards and stating that compute, network and storage on those shapes aren't oversubscribed. Those are vendor claims, but the architecture explains why bare metal costs more per core than a VPS and still wins on heavy, steady workloads.

## Committed or on-demand: run the hourly rate through a full month first

Bare metal gets sold under two billing structures. Committed capacity means one or more dedicated machines reserved on a longer term at a predictable price. On-demand means the same dedicated hardware, no hypervisor, billed by the hour as you use it. i3D.net's product page describes the working pattern well: steady workloads run entirely on committed capacity, while gaming studios and real-time platforms keep a committed base and absorb peaks on-demand, so they neither over- nor under-commit. That page dates from 2020, so ignore its performance claims; the billing distinction itself is standard across the market.

The arithmetic most comparison tables leave out. Scaleway publishes both numbers for the same Elastic Metal line: from €27.99 per month, or €0.077 per hour. Run a machine around the clock and the hourly rate comes to 0.077 × 730 = €56.21 a month, roughly twice the monthly price. Hourly billing only wins below about 363 hours of runtime a month (27.99 ÷ 0.077), which is less than half of every month.

That ratio isn't a Scaleway quirk; it's the standard shape of hourly pricing. You pay a premium for the right to switch the machine off. Hourly earns that premium on migrations, benchmark runs, CI fleets that exist only during working hours and seasonal traffic. It loses money on anything that stays up.

## Choosing by workload

**Always-on database, game server or CI runner.** Committed monthly capacity. You know the machine runs 700+ hours a month, so the hourly premium buys you nothing. Ask for the spec you need rather than the closest catalogue item, and confirm NVMe count and RAID level in the quote.

**Traffic with real peaks.** A committed base plus hourly burst. Size the base to your median load and let the peak run on-demand; committing to the peak means paying for idle hardware eleven months a year.

**Already inside a cloud ecosystem.** Pick the bare metal product from the vendor whose network, identity system, object storage and private connectivity you already use. Cross-provider egress and identity glue usually costs more than the difference in list price.

**Short-lived work.** Anything under roughly 360 hours a month is cheaper billed hourly, provided the provider offers it. Spin Servers publishes monthly pricing on the pages you can verify, so ask about hourly or short-term terms if your workload is temporary.

## Where the other providers sit

| Provider | Best fit | Billing model | Verified specifics |
| --- | --- | --- | --- |
| Scaleway | European data residency, very wide hardware catalogue | Monthly and hourly | Dedibox from €4.99/month across roughly 100 configurations; Elastic Metal from €27.99/month or €0.077/hour; Mac mini M1 through M4 Pro from €0.11/hour; facilities in France and the Netherlands |
| Oracle Cloud Infrastructure | No hypervisor, broad choice of CPU and GPU silicon | Quote-based, with a standing free tier | Bare metal shapes on Intel, AMD and Ampere Arm; GPUs up to NVIDIA B200, GH200/GB200 and AMD MI300X; RDMA clustering at 100 Gb/s over RoCEv2; free tier covers 20+ services, 200 GB block storage, 10 TB/month egress and US$300 of credit for 30 days |
| Vultr | Self-service, cloud-style access to dedicated hardware | Hourly and plan-based, on-demand and reserved | Bare metal alongside GPU, Kubernetes and storage products; Linux, Windows or a custom ISO |
| i3D.net | Latency-sensitive workloads with heavy network demands | Committed and on-demand | Up to 20 TB of traffic included (varies by location), one public IPv4, standard DDoS mitigation, redundant uplink; 2×25 Gbps standard, 1 Gbps on older instance types; remote management billed as an add-on |
| phoenixNAP | API-driven provisioning | Hourly, monthly and reservation | Bare Metal Cloud with private networking and security options |
| OVHcloud | Bandwidth-heavy workloads | Monthly and plan-based | Global data centres, unmetered bandwidth options, anti-DDoS |
| Latitude.sh | Developer and AI deployments across regions | Usage and plan-based | 25 locations across five continents, API-first deployment |
| Cherry Servers | Recent AMD hardware, flexible terms | Hourly or fixed-term | EPYC, Ryzen and Threadripper platforms, DDR5 and Gen5 NVMe |

## What to confirm before you sign a quote

1. **Hardware.** CPU generation and clock speed, memory, NVMe count, RAID level, GPU model, supported operating systems. A cheap quote on an older Xeon is not the same product as a current EPYC at the same core count.
2. **Facility and egress.** Which region, what latency to your users, how much transfer is included, and what overage costs. A 20 TB bundle that "varies by location" on a provider's own page is worth pinning down in writing.
3. **What's inside the price.** Extra IPv4 addresses, DDoS mitigation, remote management, backups and monitoring are frequently add-ons. A lower monthly rate stops being lower once you add four of them.
4. **Automation.** API, CLI, Terraform, OS reloads, out-of-band console access. If your team rebuilds machines weekly, manual provisioning becomes the real cost.
5. **Contract terms.** Minimum term, setup fee, first-period price versus renewal price, notice period for cancellation. Promotional pricing that resets after three months is a different product from a flat monthly rate.
6. **Support scope.** Which hours, what response commitment, and whether hardware replacement is covered or billed.

## When bare metal is the wrong purchase

Two cases don't justify the price. Small sites and low-traffic applications rarely need a single-tenant box; a $39 VPS or a small cloud instance covers them at a fraction of the cost and the maintenance. Highly elastic workloads, the kind that need to double capacity for two hours and drop back, are better served by virtual infrastructure that scales in seconds. Bare metal scaling happens in minutes at best, and in a quote-based environment it may involve a conversation with sales.

If either describes you, the honest answer is to start smaller and revisit when a specific workload, a compliance requirement or a noisy-neighbour problem forces the move.

## Pick by rule, then confirm two numbers

One always-on box under 8 vCPU with modest I/O: the VPS tier or a small cloud instance. One always-on box where disk latency or hardware control actually matters: a bare metal quote. Several machines needing a private layer 2 network with managed firewalls: a private cloud quote. Anything under about 360 hours a month: hourly billing somewhere, not a monthly commitment.

Before you order, confirm the current price for your exact specification and whether bandwidth, IPv4 addresses, DDoS filtering and management are inside it. Those two answers decide more of your first-year cost than the headline rate. 👉 [Get the current Spin Servers quote for your configuration](https://bit.ly/Spinservers)
