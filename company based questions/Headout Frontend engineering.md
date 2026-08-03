##  Frontend Machine Coding

**Focus areas:**

- Vanilla JavaScript
- Plain CSS
- HTML
The problems revolved around:

- **Infinite scroll / pagination**
- **Virtualized lists with 10,000+ items**

Now, the interesting part wasn’t _just_ writing the code. The interviewer wanted me to explore **multiple approaches**:

- **Intersection Observer API** — the modern, elegant, “look at me being a 2024 developer” approach.
- **Scroll position + screen height calculations** — the classic, slightly chaotic, “I was here before Intersection Observer was cool” approach.

We talked about trade-offs. When does each shine? What’s the performance hit? What happens when you have 10k DOM nodes vs. 10k virtualized nodes?

How do you keep scroll position stable when items load?

How do you handle edge cases like fast scrolling or sudden window resizes?

This round wasn’t just “can you code it?” It was **“do you understand _why_ you’re coding it this way?”**

## Round 3 — System Design + Frontend Architecture

Ah yes. The final boss.

This round was a glorious **1.5 hours long**, and by minute 47, I’m pretty sure my brain started making the dial-up internet noise.

The question? On paper, it sounded innocent:

> “Design a Toast component as an NPM package.”

I almost laughed.

_A toast? I’ve built toasts. Toasts are easy. Toasts are like —_ `_position: fixed; bottom: 20px; show; setTimeout; hide._` _Done._

Reader, I was wrong.

Once you peel back the layers of “design it as a _package_,” the floor opens up beneath your feet. Suddenly, you’re not just building a component — you’re building a product that _other engineers_ will install, configure, customize, debug, and possibly curse at on a Friday night.

The expectations were genuinely high:

- ✅ **Strictly typed code** (TypeScript, and not the “any everywhere” kind)
- ✅ **High-level design** — architecture, public API, extensibility
- ✅ **How will external apps consume it?** — peer dependencies, tree-shaking, bundle size
- ✅ **Performance considerations** — re-renders, animation jank, queue management
- ✅ **Folder structure** — yes, _folder structure was discussed in detail_
- ✅ **Unit testing strategy** — what do you test, how, with what tools?

We went deep into things like:

- How do you expose the component API without forcing a provider?
- How do you handle multiple toasts? A queue? A stack? FIFO? LIFO?
- How do you make it themeable without bloating the bundle?
- What if someone wants to render a custom component inside the toast?
- How do you handle SSR? (Because of course, SSR.)
- What about accessibility? ARIA roles, keyboard dismissal, screen reader announcements?

I tried my best. I really did. I got through most of it.

But somewhere along the way, I could feel the gap between _“I can build this”_ and _“I can design this at a senior bar.”_

