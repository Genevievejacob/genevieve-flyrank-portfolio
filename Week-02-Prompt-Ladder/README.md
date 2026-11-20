# Prompt Ladder — Week 2, Assignment 2

**Track prompt chosen:** Customer service complaint reply

---

## Baseline

**Prompt:** "Help me reply to a customer complaint"

**Output:**

> Dear [Customer Name],

>

> Thank you for reaching out and bringing this matter to our attention. We sincerely apologize for any inconvenience this may have caused. Your satisfaction is our top priority, and we are committed to resolving this issue promptly.

>

> We value your feedback and will look into this matter further. Please let us know if there is anything else we can assist you with.

>

> Best regards,

> [Your Name]

Generic, no idea what the complaint even was, sounds like a template.

---

## Version 1 — Layer added: Real context

**Prompt:** "Help me reply to a customer complaint. The customer says their order never arrived. I checked and found they changed their delivery address recently, which is likely why it didn't arrive at the expected location."

**Output:**

> Dear [Customer Name],

>

> Thank you for reaching out about your order. I looked into this and found that your delivery address was recently updated, which is likely why the order didn't arrive at your expected location.

>

> I'd like to help get this resolved — could you confirm your current address so we can arrange redelivery or reship the order? Please let me know and I'll take care of it right away.

>

> Best regards,

> [Your Name]

**Notes:**

- *What changed in the prompt:* Added the actual complaint detail (order never arrived) and the root cause found (address change).

- *What actually improved in the output:* Stopped being generic — names the real issue and gives an actual next step instead of just apologizing into a void.

- *What still failed:* Doesn't sound like me — no personality, still template-shaped. Doesn't reassure emotionally; jumps straight to logistics.

- *What I'd try next:* Add a tone/voice layer so it sounds warm and reassuring instead of procedural.

---

## Version 2 — Layer added: Tone/voice constraint

**Prompt:** "...Write it in a warm, reassuring, clear tone — the kind that reads the room, not a corporate template."

**Output:**

> Hi [Customer Name],

>

> I'm sorry about that — I can imagine how frustrating it is to be waiting on an order that hasn't shown up. I looked into it, and it turns out the address on file was recently updated, which is likely why it didn't reach you.

>

> Let's get this sorted quickly — can you confirm your current address for me? Once I have that, I'll get it reshipped right away.

>

> Thanks for your patience,

> [Your Name]

**Notes:**

- *What changed in the prompt:* Added an explicit tone instruction using my own voice card language.

- *What actually improved in the output:* Opens with acknowledgment of frustration before logistics — reads like a person, not a policy.

- *What still failed:* Still guessing at format/channel (email vs. chat), which affects length and structure. Doesn't address why the mistake isn't fully on the customer.

- *What I'd try next:* Specify the output format/channel since that changes length and structure.

---

## Version 3 — Layer added: Output format constraint

**Prompt:** "...Format it as a short live chat reply, 3-4 sentences max, no email greeting or sign-off."

**Output:**

> I'm sorry about that — I can imagine how frustrating it is not to have your order show up. I checked, and it looks like the delivery address was recently updated, which is likely why it didn't arrive. Can you confirm your current address so I can get this reshipped right away?

**Notes:**

- *What changed in the prompt:* Added a format constraint — live chat length, no email structure.

- *What actually improved in the output:* Tight and immediately usable — no wasted greeting/sign-off scaffolding. Paste-ready for a real chat.

- *What still failed:* Still risks sounding like it's blaming the customer for the address change, which could make things worse, not better.

- *What I'd try next:* Add a quality criterion so the explanation doesn't read as blame.

---

## Version 4 — Layer added: Quality criterion (no blame framing)

**Prompt:** "...Make sure the explanation doesn't sound like it's blaming the customer — frame it as something we'll fix together, not their mistake."

**Output:**

> I'm really sorry your order hasn't arrived yet — that's frustrating. I checked things on my end and found the address on file changed recently, so let's just double-check it together to get this fixed fast. Can you confirm the address you'd like it sent to?

**Notes:**

- *What changed in the prompt:* Added a quality criterion explicitly instructing it not to frame the issue as the customer's fault.

- *What actually improved in the output:* Blame is gone — "let's double-check it together" instead of pointing at the address change. Feels collaborative, not corrective.

- *What still failed:* Strong reply, but still one-size-fits-all — no room to state what happens next if the customer doesn't respond, or a timeline.

- *What I'd try next:* Try adding an example of a "gold standard" reply to see if it tightens things further.

---

## Version 5 — Layer added: Example of what good looks like

**Prompt:** "...Here's an example of a good reply for a different complaint: 'I'm so sorry about the mix-up — I know how annoying it is when something you ordered shows up wrong. I've already flagged it for a replacement, and it'll be prioritized so you're not waiting long. Is there anything else I can help sort out while we wait?'"

**Output:**

> I'm so sorry about the mix-up with your order — I know how annoying it is when something you ordered doesn't show up. I've already flagged it and will get this prioritized so you're not waiting long. It looks like the address on file changed recently, so let's just confirm it together to get this sorted fast. Is there anything else I can help sort out while we wait?

**Notes:**

- *What changed in the prompt:* Added a fully-written example reply from an unrelated complaint (wrong item, not missing order).

- *What actually made it worse:* Borrowed phrasing that doesn't fit this complaint — "I've already flagged it" and "while we wait" don't make sense here since nothing's been flagged and the customer isn't waiting, they're being asked for info. The example's specific phrases leaked in over the actual situation.

- *What still failed:* Sounds polished but is now less accurate than Version 4 — a customer reading closely would notice it doesn't match their situation.

- *What I'd try next:* Drop the example — Version 4 was already strong on its own, and the example traded accuracy for surface polish.

**This is the "made it worse" version.** Best version is Version 4.

---

## Final Reusable Prompt

> "Help me reply to a customer complaint about [brief description of the issue]. Here's what I found when I looked into it: [what you discovered — the cause, if known]. Write it in a warm, reassuring, clear tone — direct, no corporate template language. Format it as a short live chat reply, 3-4 sentences max, no email greeting or sign-off. Make sure any explanation of what went wrong doesn't sound like it's blaming the customer — frame it as something we'll fix together."

This works for a stranger on the same track because the blanks (issue, cause) are clearly marked, and every instruction generalizes beyond the specific order/address scenario tested here.
