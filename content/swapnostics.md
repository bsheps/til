---
title: "Swapnostics"
date: 2022-12-14T20:31:24-06:00
draft: false
---

Recently our older high mileage (270k mi+) sedan started to stutter when pressing the gas pedal. The engine rpm's were fluctuating between 350 and 900 every few seconds. Shortly thereafter, the (in)famous check engine light showed on the dashboard. Using my OBDII (onboard diagnostics version 2) code reader tool, I found the error code was:

> P0302 – cylinder 2 misfire detected

No bueno.

After a little time researching online and referencing the repair manual, I learned P0302 could be caused by a multitude of issues. The common source of P0302 is either something in the ignition system or the fuel system; most commonly a bad spark plug. Since I had replaced spark plugs not long ago (<20k miles with premium name brand spark plugs), I was thinking it’s probably not the spark plugs. The next item upstream from the spark plugs are the ignition coils. On our car, the ignition coils are easy to access since they are located on the top of the engine and held in by a single 10mm bolt. 

*Background: Each cylinder has 1 spark plug and 1 ignition coil. The ignition coil attaches to the spark plug. The purpose of the [ignition coil is to convert the 12 volts][1] coming form the battery to several thousand volts using [induction][2]. This high voltage gets passed from the ignition coil to the spark plug, allowing the spark plug to consistently create the electrical sparks needed to ignite the gasoline being injected into the car engine's cylinder.*

Since the error code was specific to cylinder 2, I decided I would try the **swapnostic** method by swapping the cylinder 1 ignition coil with cylinder 2 ignition coil. 

So I swapped the ignition coils and cleared the error code / check engine light. Then I started the engine. The car engine still was stuttering (as expected) and eventually (15~ minutes later) the check engine light returned. This time the error showed:

> P0301 – cylinder 1 misfire detected.

Bueno, it moved.

The error code moved with the swapped ignition coil, which confirmed this was the faulty part. I ordered a new ignition coil online, swapped the part out when it arrived, and the engine was purring smoothly again with the engine idling stably at 650 rpm's.

Lesson learned: if you have a suspected bad component and an identical known working component, give **swapnostics** a try. It might identify the source of your issue. But even if nothing changes with the swap, you can feel fairly confident about ruling out that component as an issue.

[1]: https://help.summitracing.com/app/answers/detail/a_id/5094/~/how-does-an-ignition-coil-work "How does an ignition coil work?"
[2]: https://en.wikipedia.org/wiki/Induction_coil "Induction coil on wikipedia"