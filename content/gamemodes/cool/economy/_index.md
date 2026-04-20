---
title: Economy
---

# Gem Economy

> A semi-item based economy where **shards** are the currency.  
> This document explains every mechanic clearly — including the maths behind the scenes.

---

## Table of Contents

1. [What are Gems?](#1-what-are-gems)
2. [How to Earn Gems](#2-how-to-earn-gems)
3. [The Income Softcap](#3-the-income-softcap)
4. [Fractional Accumulation](#4-fractional-accumulation)
5. [Death Penalty](#5-death-penalty)
6. [Anti-Exploit Systems](#6-anti-exploit-systems)
7. [QuickShop & Money Recirculation](#7-quickshop--money-recirculation)
8. [Income History & Decay](#8-income-history--decay)
9. [Quick Reference](#9-quick-reference)

---

## 1. What are Gems?

Gems are physical **emerald items** (◬/◭/▲) that drop in the world when you do certain activities. When you walk over one or pick it up, its value is added to your **balance** via Vault — there is no separate gem currency, it maps directly to money.

| Symbol | When it appears | Meaning |
|--------|----------------|---------|
| `◬ 1` | Single gem | Value = 1 |
| `◭ N` | Normal stack | Value = N (2 – 7) |
| `▲ N` | Condensed block | Value = N (8+) |

Gems **glow** for a few seconds after spawning so you can spot them.  
If your **inventory is full**, gems within ~2 blocks are picked up automatically (no item needed).  
**Hoppers cannot collect gems** — they are destroyed on contact.

---

## 2. How to Earn Gems

Every source has a configured **min/max range**. A random value is rolled each time:

### 2.1 Breaking Blocks (Mining / Logging)

Break naturally-generated ore or tree blocks to get a gem drop. Only blocks that existed before you joined the server count — blocks you placed yourself **never** yield drops (see §6.1).

| Example blocks | Range |
|---------------|-------|
| Diamond ore | 1 – 5 |
| Emerald ore | 1 – 4 |
| Iron / Gold ore | 0 – 1 |
| Logs (oak, spruce…) | −3 – 1* |
| Melon / Pumpkin | 0 – 1 |

> *A negative roll means no gem drops. Logs are intentionally low-yield to limit tree farms.

### 2.2 Killing Mobs

Kill a mob yourself (you must be the killer — assist kills don't count).

| Example mobs | Range |
|-------------|-------|
| Ender Dragon | 12 – 21 |
| Blaze / Ghast | 3 – 10 |
| Cave Spider | 2 – 6 |
| Zombie | 2 – 4 |
| Enderman | −1 – 0 |

> Enderman drops are nerfed to near-zero specifically to discourage XP/gem-farm rooms.

### 2.3 Farming Crops

Harvest a **fully grown** crop to get a drop. After harvesting, re-planting the seed in the same spot gives a small **replant bonus** automatically.

| Crop | Harvest range | Replant bonus |
|------|--------------|---------------|
| Wheat, Carrots, Potatoes, Beetroot | 0 – 1 | 0 – 1 |

### 2.4 Animal Breeding

Successfully breed two animals — you (the breeder) receive a drop.

| Source | Range |
|--------|-------|
| Any compatible breeding | 1 – 3 |

---

## 3. The Income Softcap

This is the **most important mechanic**. The richer you are (in terms of lifetime earnings), the fewer gems each activity rewards. The server tracks your **total lifetime income** (all gems ever picked up, minus adjustments — see §7 and §8).

### The Formula

```
effective_gems = raw_roll / (1 + (lifetime_income − 6000) / 10000)
```

This is capped at `raw_roll` — you can never get *more* gems than the base roll.

### What this means in practice

| Your lifetime income | Divisor | % of base drop |
|---------------------|---------|----------------|
| ≤ 6,000 | ≤ 1.0 | **100%** (full drops) |
| 16,000 | 2.0 | 50% |
| 26,000 | 3.0 | 33% |
| 56,000 | 6.0 | 17% |
| 106,000 | 11.0 | ~9% |

**The sweet spot is below 6,000 income** — you earn at full rate. Past that, each gem earned slowly reduces future yield. This is intentional: new players catch up, veteran players rely less on grinding and more on spending.

### How to improve your rate

- **Spend money** — buying from shops reduces your income (see §7)
- **Wait** — old income expires after 12 months (see §8)
- **Die** — the death penalty removes balance, but your income record stays

---

## 4. Fractional Accumulation

When your softcap makes a drop worth less than 1 gem (e.g. 0.4), the fraction is **saved across drops** until it totals a whole gem, which is then awarded.

Specifically, fractions are halved before being added to your accumulator (a balancing mechanic that slightly slows down trickle income at high softcap). This means:

- A 0.4 effective rate → `0.4 / 2 = 0.2` added to your accumulator
- After 5 such drops: `5 × 0.2 = 1.0` → you receive 1 gem

You will still earn gems even at heavy softcap — it just takes longer per gem.

---

## 5. Death Penalty

When you die, a percentage of your **current balance** is dropped at your location as a special death-gem. Other players can pick it up.

| Setting | Default |
|---------|---------|
| Default loss % | 15% |
| Minimum | 0% (via permission `gemmy.death.0`) |
| Maximum | 100% (via permission `gemmy.death.100`) |

Your server admin can set a custom percentage per rank by granting the permission `gemmy.death.<0-100>`. The highest-numbered permission you hold wins.

> ⚠️ Death gems count toward the picker's income, but **not** toward yours. Your income record is unchanged by dying — only your balance drops.

---

## 6. Anti-Exploit Systems

These systems run silently in the background. Knowing they exist helps you understand why you might occasionally get 0 drops.

### 6.1 Player-Placed Block Tracking

The server tracks blocks placed by players. Breaking a block you (or anyone) placed yields **no drops**. This prevents the classic "place ore → break ore → infinite gems" exploit.

- Works for ores, logs, and any other rewarded block
- Pistons moving a tracked block update the record correctly
- Crop placement does **not** block the replant bonus — only direct block breaks

### 6.2 Spawner Mob Filtering

Mobs spawned by **mob spawners** drop **no gems**. This is tracked via a persistent tag on the entity, which also propagates through transformations (e.g. a spawner zombie that drowns is still tagged).

### 6.3 AFK = Zero Drops

If you are detected as AFK (via AFKPlus), your effective drop rate becomes **0%**. The moment you return from AFK, drops resume normally.

### 6.4 AFK Chunk Nerf (1 hour)

When any player goes AFK, the **chunk they were in** is flagged for **1 hour**. During that time, all players mining or fighting in that chunk receive only **10% of normal drops**.

This prevents the strategy of rotating AFK accounts through a high-value farm area without actually grinding.

> The nerf applies to the chunk, not the player — if you start mining in a recently-AFK'd chunk, you will see reduced yields.

### 6.5 Per-Chunk Hourly Limit

Each chunk has a **gem budget per hour** (default: 500 total gem value). Once a chunk's budget is exhausted, drops from that chunk are suppressed until the hour resets.

This caps the maximum throughput of automated farms or large group grinding sessions.

### 6.6 Hopper Blocking

Gems that touch a hopper's collection area are **destroyed**. There is no way to automate gem collection via hoppers.

---

## 7. QuickShop & Money Recirculation

Spending money in the player economy **reduces your lifetime income**, making you eligible for better drop rates again. This is the primary intended way to "reset" your softcap mid-game.

### How it works

When you **buy goods** from another player's QuickShop:

```
income_reduction = money_spent × 0.5   (50% by default)
```

This amount is subtracted from your tracked income. Your balance is spent normally — the reduction only affects how much income the server remembers you having earned.

**Example:** You spend 200 coins at a shop → 100 is subtracted from your income record → your softcap divisor decreases → you get better drops on your next grind session.

### Anti-Alt Limit

To prevent players from cycling money through alt-account shops to game the system, there is a **daily cap per seller**: by default, buying from the same shop owner can only reduce your income by **1,000 per day**. Additional purchases from that seller still cost money normally but have no income effect until the next reset.

> This cap is per buyer→seller pair. You can buy from multiple different players and each pair has its own daily limit.

### What does NOT count

- Buying from your **own** shop — no effect
- Admin shops / non-player-owned shops — no effect
- Selling *to* a shop (someone buying from you) — no effect on buyer's income; it is your sale, not their spend

---

## 8. Income History & Decay

Your income is not a permanent counter. Records are stored with a **timestamp** and automatically expire after **12 months** (configurable by the server admin).

This means:

- Gems you earned more than 12 months ago no longer count toward your softcap
- Active players who grind consistently will stabilize at a softcap level, not hit a hard ceiling forever
- Long-time players who return after a break will find their effective rate has **naturally recovered**

---

## 9. Quick Reference

### Drop Rate at a Glance

```
Rate = 100%  →  income ≤ 6,000
Rate =  50%  →  income = 16,000
Rate =  33%  →  income = 26,000
Rate =  10%  →  income ≈ 96,000
```

### Ways to Improve Your Drop Rate

| Action | Effect on income |
|--------|-----------------|
| Buy from another player's shop | −50% of purchase (up to daily cap) |
| Die | Balance drops, income unchanged |
| Wait 12 months | Old income expires naturally |
| Stay active in the economy | Money circulates, overall rate healthier |

### Things That Give Zero Drops

| Situation | Reason |
|-----------|--------|
| Breaking a block you placed | Anti-exploit: placed block tracking |
| Killing a mob spawner spawned mob | Anti-exploit: spawner tag |
| Grinding while AFK | AFK rate = 0% |
| Mining in a recently-AFK'd chunk | Chunk nerf active for 1 h |
| Chunk over hourly gem budget | Chunk limit reached |
| Crop not fully grown | Must be at max age |

### Gem Symbols

| You see | Value |
|---------|-------|
| `◬ 1` | 1 coin |
| `◭ 5` | 5 coins |
| `▲ 12` | 12 coins |

