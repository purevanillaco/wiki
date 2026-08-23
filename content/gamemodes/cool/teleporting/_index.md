# 🌀 Teleportation Guide – Cool Gamemode

Teleportation is a central feature of the **Cool Gamemode**. Below you’ll find all commands, mechanics, and helpful details.

---

## 🧭 Common Teleport Commands

| Command                 | Description                                                                                                                                   |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| ⛺ `/bed`                | Teleport to your respawn point.                                                                                                               |
| 🔙 `/back`              | Teleport to your previous location.<br>Works for **death points** if you:<ul><li>**vote**</li><li>have the **Immortal rank**</li><li>or are on your **first session**.</li> |
| 👣 `/tpa <player>`      | Request to teleport **to another player**.                                                                                                    |
| 🧲 `/tpahere <player>`  | Request for **another player to teleport to you**.                                                                                            |
| ✅ `/tpaccept`           | Accept a pending teleport request.                                                                                                            |
| ❌ `/tpdecline`          | Deny a pending teleport request.                                                                                                              |
| 🚫 `/tpignore <player>` | Ignore all teleport requests from a player.                                                                                                   |
| 🎲 `/rtp`               | Randomly teleport in the overworld of your **current server**.                                                                                |
| 🏠 `/home <name>`       | Teleport to a saved home.                                                                                                                     |
| 🌀 `/warp <name>`       | Teleport to a player-created warp. See the [Warps guide](../warps) for details.                                                              |


{{% hint info %}}
Teleportation works across **different Cool instances**.
{{% /hint %}}
{{% hint warning %}}
If you are not a **booster** and you are not on your **main server**, you’ll enter **Visitor Mode**.

* 🚫 Cannot break or place blocks
* ✅ Can trade, use farms, and interact
* ⚠️ Breaking/placing blocks prompts a **server switch disclaimer** (locks your main server if not boosted).
{{%/hint%}}

---

## 🏡 Home Management

| Command               | Action                                            |
| --------------------- | ------------------------------------------------- |
| ➕ `/sethome <name>`   | Save a new home at your current location.         |
| ➖ `/delhome <name>`   | Remove an existing home.                          |
| ✏️ `/edithome <name>` | Rename, relocate, or add a description to a home. |

{{% steps %}}

1. **Set up your first base**
   Use `/sethome base` at your base to quickly return.

2. **Manage multiple homes**
   Keep homes for mines, farms, or builds with different names.

3. **Upgrade your rank**
   Start with 4 homes per server. Unlock more homes by purchasing a higher rank → [🌟 See Ranks](http://purevanilla.co/shop/cool).
{{% /steps %}}

{{% hint success %}}
Your ``/bed`` is not taken into account for your home slot count.
{{% /hint %}}
---

## ⚰️ Respawn Mechanics

{{% hint warning %}}
If you die 💀, you respawn at your **bed 🛏️** or **respawn anchor 🔗** on your **main server**.
If no respawn is set, you appear at your **first saved home 🏡** in your main server (alphabetical order).
{{% /hint %}}

{{% steps %}}
1. **Primary respawn at bed or anchor**
   The game first tries to respawn you at your bed or respawn anchor if available.
2. **Fallback to your first home**
   If no respawn is set, the system falls back to your first home location.
3. **Safe random teleport**
   If death loop detected (>6 deaths/minute), performs a safe random teleport to prevent spawn camping.
{{% /steps %}}

---

## 🌍 Additional Teleport Options

Even without free home slots, you can use **lands** as teleport targets.

```
/lands spawn <claim>
```

{{% hint success %}}
Trusted or claimed lands give you extra teleport flexibility without requiring more home slots.
{{% /hint %}}

Players can also open up their land as a **public teleport point** by creating a warp — see the [Warps guide](../warps) for how to set one up and how access works.
