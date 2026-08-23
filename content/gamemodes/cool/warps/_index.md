---
title: Warps
---

# 🌀 Player Warps – Cool Gamemode

A warp is tied to one land. You must own that land to create or update a warp on it, and only one warp is allowed per land.

---

## 🧭 Commands

### ➕ Create a warp — `/setwarp <name> [price]`

Creates a warp at your current location. Price is optional — if you omit it, the warp is free; you can also type `0` explicitly for free.

{{% hint info %}}
**Requirements**
- You must be standing on land you own.
- The land must not already have a warp — only one warp per land.
- The land must already have a role named **"benefactor"** (case-insensitive). Create that role first if it doesn't exist yet, then try again.
- The name may only contain letters, numbers, hyphens, and underscores, and must fit within the server's configured max length.
- You must not have exceeded your warp limit (see [Warp limits](#-warp-limits) below).
{{% /hint %}}

**Effects on roles**
- The land's default/untrusted role has its **pick up items** and **attack monsters** permissions turned **OFF**. This stops random visitors from farming mobs or looting item drops at your public warp.
- Anyone who was already trusted with Benefactor-or-higher role on the land *before* the warp existed is automatically marked as having unlocked it for free — they won't be asked to buy access they already effectively had.

### ✏️ Update a warp — `/updatewarp <name> <new-name> [price]`

Renames a warp and/or changes its price. Price is optional — if you omit it, the warp keeps its current price; pass a value (including `0`) to change it.

{{% hint info %}}
**Requirements**
- You must be the warp's owner.
- The new name must follow the same rules as warp creation (allowed characters, max length) and must not already be taken by another warp.
{{% /hint %}}

**Effects on roles**
- None. Updating a warp doesn't touch its land's roles or location — only its name and/or price change.

### ➖ Delete a warp — `/delwarp <name>`

Deletes one of your warps.

{{% hint info %}}
**Requirements**
- You must own the warp.
{{% /hint %}}

**Effects on roles**
- The land's default/untrusted role has **pick up items** and **attack monsters** turned back **ON** (undoing what creation disabled).
- All players who had Benefactor access to this warp have that access revoked. Refunds are **disabled** on this server, so no money moves when this happens.

### 💰 Unlock a warp — `/buy warp <name>`

Pays the warp's price to unlock Benefactor access on its land. You are trusted on the land (if not already) and given the "benefactor" role.

Even **free** warps have to be unlocked this way — walking to or teleporting to a warp never grants access by itself, whether it's free or paid.

{{% hint info %}}
**Requirements**
- You must not already own the warp.
- You must not already hold Benefactor-or-higher role on the land.
- You must not have already purchased access to this warp.
- You need enough balance to cover the price (free warps unlock instantly, no balance needed).
{{% /hint %}}

**Effects on roles**
- You are granted the land's **"benefactor"** role (and trusted on the land first, if you weren't already).

**What Benefactor access usually grants**

By default, the Benefactor role lets you:
- Plant and harvest crops, and shear sheep
- Use buttons, levers, pressure plates, and other mechanisms
- Open trapdoors and containers (chests, furnaces, etc.)
- Trade with villagers
- Attack animals and monsters
- Fly and use an elytra
- Enter the land and use vehicles (boats, minecarts, horses)
- Pick up items

{{% hint warning %}}
This is just the server's default starting point for the Benefactor role — **the warp/land owner can change what Benefactor is allowed to do at any time**, so your actual access may be more or less than the list above depending on how they've configured it.
{{% /hint %}}

**Losing access**

If a land owner later untrusts you from the land, your Benefactor access to any warp there is automatically revoked. Refunds are **disabled** on this server, so no money is returned when this happens.

### 🚀 Teleport to a warp — `/warp <name>`

Teleports you to a warp. Works cross-server if HuskHomes is installed; otherwise only warps on your current server are reachable.

If the warp has a price and you haven't unlocked it yet, you'll get a clickable prompt to buy access after teleporting.

### 📜 List warps — `/warps [page]`

Shows a paginated, clickable list of every warp on the server. Click a warp's name to teleport to it.

Some entries show extra icons before the name (hover over them in-game for a tooltip):

| Icon | Meaning |
|---|---|
| 🔓 | You've already unlocked this warp (you own it, hold Benefactor-or-higher role on its land, or already bought access). |
| 🌎 | This warp is on a different server than the one you're currently on. |

---

## 🔢 Warp limits

Each player can only own a limited number of warps at once — **10** by default. Ask server staff if you need a higher limit.

---

## 📋 Summary of role effects

| Trigger | Effect |
|---|---|
| Warp created | Default (untrusted) role loses pickup-items and attack-monsters permissions on that land. Players already trusted with Benefactor-or-higher role are marked as unlocked for free. |
| Warp deleted | Default (untrusted) role regains pickup-items and attack-monsters permissions on that land. |
| Access purchased | Buyer gains the land's "benefactor" role. |
| Buyer untrusted from land | Buyer's Benefactor access to that land's warp is revoked. No refund — refunds are disabled on this server. |

{{% hint warning %}}
Refunds are **disabled** on this server. Deleting a warp or losing trust on a land revokes Benefactor access for everyone who bought it, but no money is ever returned.
{{% /hint %}}
