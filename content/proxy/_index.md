# Proxy
## DDoS mitigation
All our providers have **DDoS mitigation services** which we are using, but **PureVanilla** has grown so popular certain attacks may be able to temporarily affect the connection to some of the proxies. These attacks are usually detected within minutes and the server is usually back online in a couple minutes. If it isn't, **relogging every 5 minutes** may improve your connection due to the **location resolution algorithm** described below.

{{% hint info %}}
### Etiquette
When the server is being hit with a **DDoS attack**, only a specific **proxy** may be affected by it. This means, sending 'lag' or similar messages on chat may be annoying for the rest of the players that are not experiencing any issues, or that are just trying to bear it patiently (it's usually a matter of minutes).

We would appreciate if such messages could be avoided in-game and on the **Discord server**, unless you believe a **downtime longer than 5 minutes** is underway, in which case opening a **ticket** on the **Discord server** (again, please avoid using #general) would be the most efficient way to notify server administrators to take a look into the issue.

Additionally, not sending any reports via **#tickets** may result in server administrators not knowing about the issue, and never fixing it. A **#ticket** in this scenario would be appreciated so we can swiftly solve any ongoing connection issues.
{{% /hint %}}

## Location list
We continuously add and remove **locations** based on server popularity all around the world.
|Country|Region|City|Provider|Count  |
|--|--|--|--|--|
|🇩🇪 **DE**| **Central** | **Frankfurt** | **OVH** | 2 |
|🇺🇸 **US**| **Central** | **Dallas** | **Linode** | 1 |
|🇺🇸 **US**| **West** | **Hillsboro** | **OVH** | 1 |
|🇺🇸 **US**| **West** | **Hillsboro** | **Hetzner** | 1 |
|🇺🇸 **US**| **East** | **Vint Hill** | **OVH** | 1 |
|🇺🇸 **US**| **East** | **Ashburn** | **Hetzner** | 1 |
|🇦🇺 **AU**| **Australia** | **Sydney** | **OVH** | 1 |
|🇸🇬 **SG**| **Southeast Asia** | **Singapore** | **OVH** | 1 |

You can consult their **status** and precise **location** from our [**status page**](https://purevanilla.co/status).

## Location resolution
When using any address ending in ``*.purevanilla.co``, you'll be connected to the closest **proxy location** (using Google Cloud datacenter sibling locations) to you. If there are multiple suitable proxies for your location, the traffic will be equally balanced between all of them, and the one you connect to is recomputed every **5 minutes**, with equal chances every time.

This means, if you **relog 5 minutes after first logging in**, you may or may not be connected to the same **proxy**. This also means, if any portion of the proxies close to you are performing below expectations, reconnecting may solve any apparent performance issues.

This also means using any ``*.purevanilla.co`` will result in the exact same **performance** and **balancing algorithm** (AKA ``b.purevanilla.co`` or ``b.purevanilla.co`` will have no performance difference whatsoever).

## Forced connection
**Forced connection** is not advised nor maintained via domains by design, as offering forced locations via domain could become a **security flaw** for malicious actors trying to target a specific **proxy** for a **DDoS attack**. 

## What is it
A **proxy** routes your connection to the end servers running **PureVanilla**, instead of connecting you directly to the server running **PureVanilla**.

## How does it benefit us
We must use **proxies** because the **Minecraft protocol** does not support server switching when being connected to a server, which would make our **multi-gamemode multi-instance** scheme not viable.

The **proxy** internally simulates a normal Minecraft server but routes the packets to the end server dynamically based on the **gamemode** you play.

Additionally, the use of **proxies** hides the backend server **IPs**, preventing **DDoS attack** to core infrastructure, and making the proxies, which are more abundant, the only user-facing (network-wise) element of the server.

## How does it benefit me
In addition to the **reliability improvements** commented above, we host multiple **proxies** all around the world which use **datacenter-grade connections** to route your connection between the **proxy** and the backend server, lowering the overall **latency** for your connection.
