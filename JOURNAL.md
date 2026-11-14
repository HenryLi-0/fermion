---
title: "fermion"
github: "https://github.com/HenryLi-0/fermion"
description: "Spark v2. Spark (the 3D printer) had a ton of issues, how does one make a successor with twice the overscope?"
created_at: "2026-11-14"
total_time: "14h 52m"
---

# August 28, 2026
<!-- fabricate:entry 2978 -->

## 8/10/2026 - 1st Update!

yes, im sure you have tons of questions lol

disregarding the overarching question that every first log has to solve (what is this?), i do know that river is incomplete as of now. i havent really had any motivation to finish it, but i do plan on it, sometime this week. but for now (and a while now), i feel like its progress is currently slowing us down a bit. regardless, im gonna complete it, but i have a ton of ideas i want to write down and document, so that i actually have a readable progress update, instead of coming in with a full design (because, after all, that's not as interesting or as educational as seeing designs converge into an idea!)

one more note, it's currently 2:03 AM on 8/11/2026 right now, but i'll push this for 8/10/2026!

so, the question you're probably wondering now, what is fermion? well, it's technically a successor to spark, which was more of a learning opportunity, looking at it retrospectively, and it's not easy or expected to get everything correct first try, so here we go, spark v2! with, a different name! ok, skip that, we got branding made already (yes ive been busy lol)

similarly to last time, after just around 2 weeks, i have returned to present you the raw concepts of fermion, tihs being arc 3 of year 3, following [`spark`](https://github.com/HenryLi-0/spark/) (build) and [`river`](https://github.com/HenryLi-0/river)! here we go

---

- compact. like, really compact
    - way back when, i came across alex's (qcoral) project [neutrino](https://github.com/the-openary/neutrino), which i later discovered was inspired by positron!
    - both are meant to be compact printers that fit in a standard filament spool box
    - spark needed a whole new suitcase to travel to open sauce
        - it was also a huge suitcase and would barely close unless the top bit was moved and held in a certain way
        - basically, not very convenient to travel with
- tool changing
    - of course, with such a small form factor, this is gonna be the bulk of the issues, aka, smart and compact design
    - just like spark, triple nozzle is the plan, maybe a fourth tool for z probing, which we should try to get

---

this thing, if those two are done, might make this the world's smallest (to my knowledge) folding (ill get to this) tool changing 3d printer, which would be insane (it might also be the first to fit in a filament box upon compacted)

of course, im getting ahead of myself (cant wait to realize the overscope), how are we pulling this off?

that's for the next commit to answer lol

ok so im back after a quick second, this time on github mobile, so where was i? oh right, the architecture! whatever we do, we have to have an incredibly compact extruder setup and xyz motion. unfortunately, i dont have all my ideas anymore, but heres the roguh process. (im actually out of words, see the picture!)

now, a quick search shows that this idea has been done before, which is a good sign (both because of design convergence and that it's been proven to be possible). yes, its a little sad that it's not super unique of an idea, but hey, corexy isnt exactly a new idea, the innovation comes in execution! (and the idea of course) (additionally, there arent many scissor lift 3d printers antways)

point is, imo this is the best way to compact it, espexcially because of size constraints. only issue i have is that the design needs to be very rigid somehow...

anyways, electronics go below the build plate, tools on the top in a row, gantry can fold there (hold on theres no way it can get there, actually nvm), dokcing areas are there too, print area is more of a rectangle, scissor lifts on the side

exact numbers and more ideas soon, just scribbling stuff down, but it's 3:01 AM, so yeah, good night!

![](https://fabricate.hackclub-assets.com/983d4a72711c5b53997a53348583926af006b29091f8e52a6833ac71250f082f/image-png/image.png)

**Total time spent: 19m**

# September 10, 2026
<!-- fabricate:entry 2977 -->

## 8/27/2026 - 2nd Update!

well, it's actually 1:31 AM on 8/28/2026 (yes, i just finished up the river bom stuff for today)... also, seems like, similar to `spark`, the strange gaps in time also exist (no ill stop disappearing for weeks. i think.)

anyways, i need to lock in on avarious things before school starts, this being one of them. my goal's to start sometime in the september, preferably before school starts, though no promises! anyways, today's gonna be yet another yap session, what do i have in store today?

ive been researching! at least, as far as youtube videos gets you... but yeah, lots of ideas recently!

last time we talked about the overall structure itself (scissor lift z axis, corexy, similar belting), but this time i want to talk about tool changing! here we go!

spark
- tool changing barely "worked"
    - the latch system had WAY too many parts (some fell off during transport lel)
    - the latch system required rubber bands that did not exist or could possibly exist (it needs to be kept in the middle of the track)
    - the only way it worked was if the latch had a default state in the middle (which, as just mentioned, it did not)
- the tools were MASSIVE
    - well, they're pretty normal sized, but still, it's not ideal
    - they also break stuff when they fell, and they were not fun to assemble
        - please no more impossible screws that need to be hand turned
- the single motor idea was pretty nice
    - however, functioning nicely is... yeah

essentially, tool changing did not really work as well as i envisioned (which was expected!). so, what's gonna change? well, one really nice idea, as noted above, was only having a single motor, as that saved on both price and tool size. however, the sacrifices it made was not really great (this was also partially due to a bad extrusion gearing)...

but what if the filament path was its own tool? im gonna be a bit honest here, i was inspired by the [INDX](https://github.com/BondtechAB/INDX/tree/main) project, but im gonna take my own spin on it! (as in, imma still design everything myself, the only thing im borrowing is the idea of sharing the filament gearing). to be clear, the idea im borrowing is the gearing releasing the filament, swapping to the next tool, and grabbing it again (with wired, not passive heaters!)

of course, that's a design challenge in of itself (were also probably still gonna use PLA). also during this time, ive been looking at various extruders, i came across [this](https://trianglelab.net/products/tz-e3-20-hotend?VariantsId=11441) from triangle lab again, but im not sure if i want to stick with it, the main goal is to have a hotend that's both compact and can get easily blasted by fans!

speaking of fans... we still need to decide on that, i havent done much research into it, but having one for each tool sound about right? anyways, the goal is still the same as spark, with 3 tools (maybe well add more if it makes sense and space allows), and maybe even a z probe? (ill be a switch lel)

anyways, for docking, we're probably gonna use magnets. yeah, for real this time? anyways, to detach, it'll probably be a simple latch hook- WOAH WOAH WOAH. what i meant by that is the tool going into, sliding on a screw, and detaching!

(see the rest of the logs in the image! yeah, im sorry i yap a lot lol)

anyways, it's 2:17 AM, so yeah, for now, good night!

![](https://fabricate.hackclub-assets.com/ee672a342fa121cd738672aabb045f71b51201a90b2e5d520130d56c6c4fca92/image-png/image.png)

**Total time spent: 45m**

# September 12, 2026
<!-- fabricate:entry 2976 -->

## 9/9/2026 - 3rd Update!

*It's 11:31 PM. It's been a full month since Fermion was announced to the infinite depths of the internet.*

*It's the night before the first day of school, senior year. The final year. The start of the end. If you had less than a year with the stuff you've grown up with for the past three years, what would you do?*

*If everything changes, what would you do?*

What would I do?

welcome back and yeah, it's the day before the start of my senior year. fermion would be quite a way to kick it off :D, there hasn't been much progress on this at all, and im very sorry for this. after all, a bunch of unkept promises, unfulfilled dreams, you get the idea, isn't really plesant.

so, stardance ends in 21 days. i have multiple essays and applications to finish up. 21 days, somewhere around 500 hours, probably less. how am i gonna split up my time? the goal, at least for the rest of september is to first finish river by the end of the week (its only cleanup and updates at this point), and to submit it! then, for the rest of the month, i'll work on trying to, well, cad the whole thing in two and a half weeks

where have i heard this before? oh yeah, i dont have much confidence i could do it by the end of stardance, and that's fine. well, it actually isnt, but hey, hopefully moving projects works by the end of it all? (ill still aim to finish)

of course, ill do last minute stuff after the deadline, probably the day after (like the wiring diagram), but lets not think that far yet!

*bzz*

![hmm](</updatelogs/images/202609/09092026 - 1.png>)

yep! first photo, that's currently my ideas for now. there's no way to actually scuplt or imagine it in 3d (i mean, i can sketch, its just gonna be messy with so many iterations), so it'll have to be a krayoncad (yes we're using that again!). it'll probably be some mashup of random stuff, but it's just to get a conceptually idea, of course, then we'll hopefully start mastersketching by next week.

speaking of which, how do you balance this with school? lemme reference the spark logs...

bad news guys, uhh... last time i tried doing this in a month, it became six months (not counting research), with the time before being a one week attempt (which got nowhere). so, we got stuff to do

- 9/10/2026 - 9/12/2026
    - Finish and submit `river`
    - KrayonCAD and refine ideas
    - Idea Refining (1 day)
- 9/13/2026 - 9/19/2026
    - Mastersketch (3-4 days)
    - Physics Work (1 day)
    - Subsystems (Basic) (2-3 days)
- 9/20/2026 - 9/26/2026
    - Subsystems (Detailed) (5-6 days)
    - Fixes (1 day)
    - BOM Assembly (1 day)
- 9/27/2026 - 9/30/2026
    - Electrical (1 day)
    - BOM Assembly (1 day)
    - Buffer (1 day)

*But that's impossible! It's basically constant work and unrealistic scheduling, with almost zero free time.*

yeah, that's the issue. to pull this off, i (quite literally) need to work everyday on this, along with balancing school, essays and applications, homework, and robotics (woo), so this is quite truly a challenge. but hey, no one got anywhere stay in their comfort zone, and, frankly, ive been in mine for far too long (the second half of this summer)

so, see you on friday? or saturday, idk

anyways, it's 11:57 PM, here's to ambition and the will to challenge, and yeah, good night!

![](https://fabricate.hackclub-assets.com/830883a07235987d0e4c59a20e3f27f3c281a932a395e4a6b01fbf5b3f75d631/image-png/09092026%20-%201.png)

**Total time spent: 32m**

# September 14, 2026
<!-- fabricate:entry 2975 -->

## 9/12/2026 - 4th Update!

hey hey hey

it's 3:52 PM on saturday, and happy to say that we're barely following schedule! after 9/9/2026's update talking about shipping river, got back to work and wrapped it up and shipped it across 9/10/2026 and 9/11/2026! it's submitted for review, so i theoretically dont need to do much about it now (maybe some firmware stuff but not much), so yeah, time to focus on this now! the goal for the end of today is to have a krayoncad and refine to concept, so that we actually have something in 3d to look at the linkages and stuff!

well, brb, one second, back at 4:06 PM, let's go!

yeah so we basically have a 200mm x 200mm space to work with, with like 3mm of wiggle room, with 7 (ish) centimeters vertically (im measuring a polymaker spool box btw)

idk why onshapes a bit slow today

ok, if the motors are on the front, it lets a little place in the front which would be neat but that shifts all the weight to the front which isnt really good, but if the tools are in the back, thatll help with the load but its still goofy, but what if we just move the scissor lift to the back? well that just reverses the entire printer, its the same thing as moving our tool bay to the front, which would shift the space to the back but not be very nice with balance

idk, text blob of thinking

well, this is what i have so far!

![hmm](</updatelogs/images/202609/09122026 - 1.png>)

it's not exactly the best, theres a lot of goofy stuff (and stuff i havent considered, specifically where the z motors are gonna go), but i think its a good start?

ok, heres a list of all the issues i currently have with this

- z axis
    - what??? (like seriously what is going on here)
    - need to have an actual concept for the motion
    - currently is just a "linear rail" and a lead screw (represented by the belt) in that orientation
- tool area
    - the tool size is kinda unrealistic but still maybe possible?
    - its probably better to have a fan on the tool bay area that stays there than have one that moves
        - as in, fans on the tool for the cold end, then a fan per tool in the docking area, not one that moves across
- tool base
    - theres no space for the stepper motor (at all)
    - theres a very low chance all the gearing will fit but we'll see
- dimensions are unrealistic
    - unless the rails are the actual supports (probably will need 1cm x 1cm extrusions, need to look into the structure and support stuff), the widths are not correct
- z scissor lift
    - the z scissor lift is kinda goofy in numbers (expected, since we cant really do that yet)

ok, it's 5:42 PM, brb... (quick commit)

(bro yapped too much, the middle part of this updatelog is in the first screenshot)

yeah kinda tired right now, idk, ok, 11:25 PM now, gonna go watch a movie, see ya!

ok, 1:20 AM now, i think this is a good start, gonna sleep on it for tonight and hopefully refine the idea overnight? idk, letting the idea process for a bit usually helps out! that said, good night!

![](https://fabricate.hackclub-assets.com/cf456d32342ade7098cc830896e9de4eaed86551b253f1068494702f92ddf139/image-png/09122026%20-%201.png)

![](https://fabricate.hackclub-assets.com/9404ae64306f40f43ac533f63c6b414a2d5f76e7c27a6e4a4c36888cf2511657/image-png/screenshot.png)

![](https://fabricate.hackclub-assets.com/cf456d32342ade7098cc830896e9de4eaed86551b253f1068494702f92ddf139/image-png/09122026%20-%201.png)

![](https://fabricate.hackclub-assets.com/9404ae64306f40f43ac533f63c6b414a2d5f76e7c27a6e4a4c36888cf2511657/image-png/screenshot.png)

**Total time spent: 2h 40m**

# September 14, 2026 (entry 2)
<!-- fabricate:entry 2974 -->

## 9/13/2026 - 5th Update!

it's 9:44 PM, im back! hope you didnt think i was gonna miss today :p

ok, so the reason why i cant really start working, and im really stumped, is that fermion's more of a packaging problem. for spark, the whole thing was easily tunable (as in, heights were changed a BUNCH during the end, which being parametric really helped out), but fermion has to "work", of course not first try, but the order we do things really does make stuff work out or be super painful later on

i think im not gonna use linear rails again (what!) because, well, i really dont enjoy having to import random parts from outside, and working around them is a real nuisance (along with the fact they are really pricey sometimes, given that we would need like 3 for the corexy and 4 for the scissor lift)

hmm it might be best for me to start with front facing points instead of side heights, basically a front facing profile first, well, let's go then!

(instead of locking in, the narrator went straight to catching up on messages and quite some time has passed (10:01 PM and now its 10:14 PM))

so uh, the whole things gotta be mirrored right

quick check that t nuts for 1010

sorry had to quickly get rid of an insect, anyways, why are 1010 extrusions intrepreted in inches???

im gonna implode (onshape doesnt have 1010 profiles)

good news is that 10x10mm extrusions do exist on amazon, except theres no standard for them 

shoutout to [this](https://www.amazon.com/MakerBeam-300x10x10mm-clear-anodised-pack/dp/B01M19VTOB/) thing on amazon, first place with actual decent drawings for this

ok, good news, the profile is now in onshape, most details are in, just except for the fillets (the listing thing doesnt provide that information, and onshape doesnt want it to exist). however, this is probably for the best for performance (cope)

ok, for the sake of clarity, let's name the parts:
- central: the part that remains stationary to the ground, so the electronics and the build plate
    - build plate: the build plate, which sits above the electronics
- z scissor lift: the part that makes the z move, but NOT the subject itself (basically, the scissor mechanism)
- upper platform: the subject that gets moved, so the corexy and tool bay
    - tool/docking bay: the docking bay for the tools

shouldnt be that hard? yeah, fairly straightforward. anyways, thats the standard i guess im gonna use for the cad

woo 3mm gt2 belts actually exist! found some [here](https://www.aliexpress.us/item/3256803817478370.html) on aliexpress

anyways, for this corexy setup (no, we arent cadding it yet, im working on side heights right now), we're NOT gonna be fitting the belts inside/between the rods (did i mention that already? i think i did, we're using rods), but instead we'll make them side by side, one second

a little doodling later, here's what i mean!

ok, so here's the order we should mastersketch in, since ive been twirling around the cad for like a good couple minutes now

- base and side heights (obviously)
- z lift (what!) (since this is super influential in the amount of space we get)
- corexy (upper layer stuff) (needed before tool stuff)
    - motor positions! (this influences docking area spaces)
- tool base and docking area
- compact
- main electronics area

so uh, how does one even have a scissor lift with a screw in the middle? i forgot to press record.

well, yeah, its been a bit, i took a bit of a break, it's 12:38 AM, i think im gonna stop here for today!

of course, there's still lots to do, but yeah, seems like a good place to stop for today! it's 12:39 AM, and yeah, good night!

![](https://fabricate.hackclub-assets.com/05bde09189bea32e4da8b8fc03693b8a91d5644e026714861fd4a6de3c675e55/image-png/09132026%20-%201.png)

![](https://fabricate.hackclub-assets.com/99baec69643676bd204c5024c5ded342d9dea9096286f525d1d6e64700b384d4/image-png/09132026%20-%202.png)

![](https://fabricate.hackclub-assets.com/2a54b941e4fd1944a89897221cb02b154a3fb3ccf1028836c74c75eadd909dd0/image-png/09132026%20-%203.png)

**Total time spent: 1h 44m**

# September 16, 2026
<!-- fabricate:entry 2973 -->

## 9/14/2026 - 6th Update!

ok, ill admit, it's pretty late, it's currently 12:22 AM on 9/15/2026 (but that doesnt mean progress cant happen!)

quick glance at the schedule

- 9/13/2026 - 9/19/2026
    - Mastersketch (3-4 days)
    - Physics Work (1 day)
    - Subsystems (Basic) (2-3 days)

i doubt that itll be possible to finish the mastersketch in two more days (not counting today), considering the meetings and stuff, so mastersketch work might take up the entire week, but also, making all the subsystems in a week was also super unrealistic

anyways, may the cad resume!

so, ive been thinking about the structural integrity, what does the extrusion actually do (other than forming some sort of support structure)? it would be more compact to just have two rods with the belts running on the side, which should offer the same level of support (the only worry i have with that is basically the back would have to be pretty strong)

basically, a C shaped structure of that size (with the gap being the front) has the potential to be wobbly (as exemplified by the early assembly of the spark frame). ngl, i can't really remember if it was super bad, i think after tightening the screws it was actually pretty strong

anyways, point is that it might be worth it to have an extra extrusion on the front (though, i dont think it'll be necessary given the amount of gussets and stuff at the back)

now, how will the rods be installed? on spark, it was basically friction fit, except it wasnt really a fun experience (fun fact, to install the z rods i had to put all my weight on the part, yes, i also had to add the bearings by jumping on the parts). this is not optimal. obviously. one solution can just be using heat inserts and just driving the screw to clamp it, or just use a giant clamp. idk which one i like more, im personally not a big fan of having massive blocks at the ends with screws sticking out, so i think it'll be more of a clamp style thing

theres no way i listened to two full albums tonight, one second... ok, so enough chit chat, let's get to the mastersketch!

so uh, linear bearings are actually massive, gonna expand height to 7.5cm

why am i actually locked in (why is this also appearing deceivingly straightforward), anyways, need to find some motors, then gonna end it there!

- [nema11 31mm length](https://www.aliexpress.us/item/2251832398319009.html)
- [nema11 45mm length](https://www.aliexpress.us/item/3256808324131817.html)
- anyways, gotta decide on one of those, then the cursed geometry to combine the stepper motor, linear rods, and aluminum extrusions together

ok, so we just have one of the pivots being stationary, i think? probably the back corner? and then the sliding one does the force and yeah

well, that's about it for today! lots of planning, but also a good amount of cad work (at least for around 1.25 hours of work!)! well yeah, hopefully i can start working on this earlier tomorrow (had to get home today by train, probably not the best move), but yeah! it's 1:37 AM, so yeah, good night!

![](https://fabricate.hackclub-assets.com/27a5a3a66c9aaa725ce2c1cd546def5151826f2f9554e1b43bf1f8d16d054575/image-png/09142026%20-%201.png)

**Total time spent: 1h 14m**

# September 17, 2026
<!-- fabricate:entry 2972 -->

## 9/15/2026 - 7th Update!

uh, it's even later than yesterday, it's actually 1:37 AM right now. anyways, you think id miss an updatelog :p

(no, this isnt a continuation of yesterday's session, its actually been a whole 24 hours)

not much talking, i want to get at least half an hour of cad done today!

ok, so for the rods on the z lift, we need to have limits, and we gotta define the ending blocks at this point...

also, we're gonna be using whatever screws the motors use (unless theyre somehow too big for our purposes), just because its, well, optimial i guess

my sourcing adventures have told me about the F4-9M thrust bearing. idk.

so uh, imma ignore that and try to solve it, one second

ok, good news, we now have a solid 5cm of build height (in the worst case scenario, how low the tools are is the biggest influence for this, this statistic assumes the worst case that the tool reaches the very bottom). yeah. so. we do need to optimize the scissor lift bit to squeeze more height in

ok, so it's 2:27 AM, did a bit of z and corexy work today. yeah, we're running pretty close to deadline, ill see what i can do tomorrow, hopefully with an earlier start? also, another note, the build plate representation was done yesterday (but i just put it below the rollback bar for things to be more accessible while working on it)

so yeah! it's 2:30 AM, so yeah, good night!

![](https://fabricate.hackclub-assets.com/d11e47d848ec5d99a678aaf09049e3384bc2a12dbc81a7ff69a27d5beefe7e26/image-png/09152026%20-%201.png)

**Total time spent: 51m**

# September 18, 2026
<!-- fabricate:entry 2971 -->

## 9/16/2026 - 8th Update!

hey! it's 12:22 AM, we are back earlier than yesterday but not as early as i would've hoped, but that's alright!

ok, yesterday's updatelog has been moved over, time to get to the cad! a quick check on what we need to work on:

- **MOST** - base and side heights (obviously)
- **MOST** - z lift (what!) (since this is super influential in the amount of space we get)
- **SOME** - corexy (upper layer stuff) (needed before tool stuff)
    - motor positions! (this influences docking area spaces)
- **NONE** - tool base and docking area
- **NONE** - compact
- **SOME** - main electronics area

well, let's get to it!

ok, i need to think of what the belt path looks like, we have the switch back stuff towards the front, of course, but for the back? i guess id probably just use a bearing to push it to the center, since i do need to consider im trying to fit this in a really tight space

can we just put the bearings inside the motors shafts (shh) (not a bad idea except its probably a bad idea)

so uh. we have a ton of geometry fixes to do. right now, theres not enough space in the middle, and the only real way to fix that is to stack the corexy stuff on top of the linear rods, not to the side (there literally just isnt enough space at that point.) it might sacrifice a bit of height but it'll be able to have around 2.6cm extra space on the x direction

seems like it'll sacrifice roughly 0.7cm? but again, the stuff would be higher up so that might also cancel things out

so uh. i think i gotta just redesign the whole thing at this point

i think i might use thinner rods for this, idk, just a thought

so uh, on second thought, how am i gonna make the belt go through a rod... (you go around it!)

very good news! turns out, the calculations were a bit wonky, and now we should have like 9cm of height? maybe?

[this](https://www.aliexpress.us/item/3256811894610177.html) looks pretty decent for the pulleys?

so yeah, that's the current status of things! sorted out the lift stuff (i think?), and did some of the pulley stuff (so that we can add belts pretty quickly)! after that is probably tool base work?

just remembered that the belts on a different layer (as in, its above), so fixed that and made it a bit more compact!

reminder to self to add a tensioner at some point

ok, stuff got updated, not too much changed, mostly just small fixes and changes here and there

well, it's 2:08 AM, a decent amount of stuff done today, i don't think that we're exactly done yet, so we are now technically falling behind schedule, but we'll see how much can get done by the end of saturday? anyways, yeah, that said, good night!

![](https://fabricate.hackclub-assets.com/36e835c813a0f34a7772f2d30f04b06385fb08a2b11b3211a47c806acb19a693/image-png/09162026%20-%201.png)

![](https://fabricate.hackclub-assets.com/d9119a3f0325acf315e1ceda0dbf9b808a94d187057b58e31996928051cf0349/image-png/09162026%20-%202.png)

**Total time spent: 1h 41m**

# September 19, 2026
<!-- fabricate:entry 2970 -->

## 9/17/2026 - 9th Update!

ok, we're back! it's 12:47 AM, enough talking, let's get back to cad work!

looking at the todo list, i think we want to finish the corexy definitions (mostly just the motor positions), i think im gonna try to add the belt paths in my free period tomorrow in school, tool base work needs to get started today, gotta consider a configuration, still considering if doing a tool changer by only switching the filament and the tool is the move (as in, if its the most feasible)

anyways, cad time! (also, friendly reminder that we need to put a motor on the gantry somewhere) (how does one even start here?)

so ive been thinking, uh, nvm, not that great of an idea. basically, what if we move the docking/tool area to the front, so that we can have the motor pointing towards the back (where the corexy motors are) for better storage. it'll probably work, but that's kinda a nightmare for supports? unless, of course, its super light

hmm im actually seriously considering this, since its such a nice geometry (it also moves the printing area to the center, which should theoretically let us print there instead of aiming to print in the very outside/front area)

(also, in theory, the back is heavy enough with two whole motors to balance things out, if needed, weights can also be added, but i dont think thats necessary)

(insert fun geometry change montage) (why does my leg hurt)

ok, so stuff has been updated and fixed, the idea is the motor points, you know what, lemme just cad it

also, note, we kinda dont have a second linear rod for the purpose of, you know, cancelling our rotation, might have to add that soon

ok, since we're here, im thinking of using 6mm rods because 8mm might be unnecessary because we have the rods in pairs (specifically, the cantilever side of the lifted part), so we get that benefit

fun fact, it might be possible to stash all the motors in the back. yeah its not necessary but it would be cool :p

actually, i dont think im gonna do that, its also probably better to just keep the z motors at the front since we can actually have a belt path that way... new issue! if we place it in the front theres basically no space to put the tools for the tool changing

ok, idk if the belt can even fit like that, but lets say it can (basically, it has to go under the corexy motors)... unless it doesnt...

ngl it might be easier to have 3 motors for this, since they funnily enough perfectly slot in (maybe? not sure but its an idea)

ok, so not too much done today, mostly just design changes and stuff, yeah, a good amount of fixes here and there

hopefully tomorrow i can start earlier (since its friday and no after school stuff is planned for tomorrow?), that said, it's 2:21 AM and yeah, good night!

![](https://fabricate.hackclub-assets.com/836160740008649e75c0622f16ec254a421ded6a89211ea494b92da068f1fb32/image-png/09172026%20-%201.png)

**Total time spent: 1h 37m**

# September 21, 2026
<!-- fabricate:entry 2969 -->

## 9/18/2026 - 10th Update!

it's like 1:43 AM, wasnt gonna write a log for today, but might as well? anyways, added a stack, hopefully i remember to make those actually tensioners later

6.540 cm vs 5.162 cm, we should be able to tension up to 1 cm with this setup?

hmm i really dont know how to do this setup, with two rods here? anyways, the corexy belts are added, just trying to get the tool base profile working? considering maybe using a linear rail here, or maybe even v wheels for the extrusion? (idk)

mfw looking for MGN9C models and the specs dont include data on the screw hole size for some reason

yeah uh the screw hole is bigger than the middle section of the extrusion, might have to use MGN7C at this point

well, after a bunch of research, i think using the rail is the method, though, im not sure exactly how we should use it. mounting it above an extrusion is probably the best setup here, except 10mm x 10mm rails are like super niche or something since basically no one sells them (pla t nuts cant be too bad... right?)

welp, not sure, not much cad updates today, mostly research?

also, the reason i didnt start earlier today was because i sorta fell asleep today for four hours in the afternoon after coming back from school, oops, anyways, it's 2:42 AM now and yeah, good night!

![](https://fabricate.hackclub-assets.com/5a4bd0ebec89e16415656fba18a8f177098c2eaa15ce2568c421437ace232359/image-png/09182026%20-%201.png)

**Total time spent: 1h 1m**

# September 22, 2026
<!-- fabricate:entry 2968 -->

## 9/20/2026 - 11th Update!

missed one day, but miss two? i dont think so. anyways, dramatic opening aside, it is 11:25 PM, just celebrated cake day (a couple days late but still great :D), so yeah, in celebration of becoming yet another year older (my foot hurts), time to get cadding! (brb)

ok, it's 11:50 PM, might need to lock in, in other news, doggie just got 97% (again) and 91% on grief tonight! might want to tune in (if youre reading this from the future, today's stream 390)

anyways, first things first, we need to find a stepper motor ideally with lead screws built in (those exist?) (yeah, apparently so)

ok, it's 11:58 PM, gonna go watch a movie, brb!

ok ive returned at 1:30 AM to focus on two things at once (i gotta get the sticker streak continuing), so yeah

ok now what are the heights of mgn7c rails...

why does no one have cad models for mgn7c rails that arent filled with other stuff...

ok 1:46 AM and now im actually gonna be fully focused

so, this might not be the most ideal setup. currently the motors really far in the back, however, theres no real mounting solution going on here, so here's the dilemma. the motors too big. like. too big. additionally, this means that it kinda pokes through the back, or in a weird way. anyway this happens isnt very good, since the gearing has to go through the extrusion. obviously, we can do a hex adapter and do a spark here, but that's not a good idea for obvious reasons (re: `spark`)

do we actually have to look into pancake motors? yeah, i think we do...

also, one more thing, it might be a good idea to split the belts to be on both sides instead of just one, just to balance things out a bit

got a little distracted with [compact hotends](https://www.trianglelab.net/products/tz-e3-20-hotend?VariantsId=11441), but yeah, went down a rabbit hole, we need ptfe tubes (spark did not have these), wow, theres a lot to do

turns out, sourcing these things is super annoying! looked for nema 11s with integrated lead screws, all of them are mad expensive, probably just gonna use a shaft coupler, yep certainly am.

anyways, lets do some math, the 45mm motors have (allegedly) 10Ncm of torque, should be enough with a T8 screw and having two of them (additionally, to help with lower layers, an idea that came across the other day was adding springs at the bottom)

uh idt this is gonna reach the full range...

anyways, it's 2:43 AM, mostly a bunch of research and small adjustments, nothing too big today, hopefully more stuff tomorrow?

that said, it's 2:44 AM, good night!

![](https://fabricate.hackclub-assets.com/3e95c9f49c2ad19e6ecef8a4d2f2a0b0a74efb5f82ac0a56f19c0bdef8587ba1/image-png/09202026%20-%201.png)

**Total time spent: 2h 12m**

# September 23, 2026
<!-- fabricate:entry 2967 -->

## 9/21/2026 - 12th Update!

*You couldn't build a printer in a week. You **can't** build a printer in a week.*

Yeah, I know.

*You've got eight or so days left. And you spent the last three grinding Geometry Dash.*

Yeah, 158% on nine paws, woo!

*And you're not at all concerned about the time?*

The what?

welcome back! it's 12:08 AM on the morning of 9/22/2026, and boy did i realize the entire weekend and the extra day off disappeared in a blink of an eye. yes, i finally beat the level, now moving on to something way more difficult, but first, it's time to address the bigger issue in the room. yes, technically fermion, but also time. pause the music, it's getting a bit serious here.

we have a solid 8 or so days left. we didnt spend the weekend well, i didn't spend the weekend well. but hey, we can't get that time back. what a mindset, instead, i gotta start actually spending my time efficiently. yes, i beat the level, but now, i need to take a break. not because of exhaustion, but because we literally don't have enough time to play gd at the same time. its just not able to fit there.

*It's not meant to be easy, you know.*

who is that guy in italics? idk, they're kinda weird. anyways, question is, what now?

8 days. lock in.

if we cant get this done by the end of stardance, id probably look into exporting this to a similar ysws, hopefully to finish it there in time for the winter season, because that's a pretty fun time to build stuff before build season starts, and when college applications are mostly over! that said, back to the cad...

ok, we need to sort out the motor support first, one second. ok, that should be good, 

ok, ive got a plan. but it requires the tool head to be both unbalanced, weirdly shaped, and quite low. of course, that's if we're still going with the small tool idea, we can always just slap three extra motors and call it a day, but thats too easy and probably more sane. theres no avoiding it, gotta get designing that now

mfw 8.8cm for the available tool space (horiziontally)

at that point might as well just have two tool heads that swap out with the motor and all at the front

im thinking of a ton of possible configurations, lets write them out

- idea 1
    - z motors are in the front, belted to the lead screws
    - corexy motors move to the side
    - still doesnt solve the issue that the tool head areas
    - front does look cooler
    - no neat place to put the tool head
- idea 2
    - similar to the first idea in the the z motors and lead screws are belted together, but the z motor is above, facing backwards, belted to the lead screw, so that it can be at an angle (getting this to the other side would be wonky, but perhaps doable)
    - this should move the lead screws closer to the sides, giving more space! (also look into different things that move on the t screw that are smaller, perhaps smaller than T8 lead screws?)

huh. i seem to have forgotten to add yesterdays log to the website. oops. well, that just got added, some weird time stuff but yeah.

well yeah, it's 1:17 AM, and i think i like the second idea. checking the cad, it's probably possible to fit this (its gonna be close?), so thats cool! anyways, yeah, good night!

![](https://fabricate.hackclub-assets.com/df2b249f0fd5b31d17b40385cf2ca11b3a5c7a9f175b26514cf899e9b43e6abb/image-png/image.png)

**Total time spent: 16m**
