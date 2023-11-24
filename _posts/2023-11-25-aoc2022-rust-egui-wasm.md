---
layout: post
title:  "Advent of Code 2022, Rust, egui and Wasm"
date:   2023-11-25 02:42:00 +1100
categories: blog
tags: rust egui wasm aoc2022
---
I've been going through the Advent of Code 2022 (aoc2022) challenges in an attempt to improve my skills coding in the *Rust* programming language. 

It's been fun so far! 

I'm up to day 12 of the advent challenges at the time of writing, and liked the challenge so much I made a *egui Wasm web app* for it: [play with it here!][gh-page-jwebmeister-aoc2022] 
(it runs in your browser)

![My web app](/assets/images/aoc2022_day12_pathfinder.png)

I did peek at a few solutions from others. Sometimes when I ran into roadblocks, but always after I completed a challenge, curious to see how others approached it. 

I'm glad I did! 

I learned a lot by repeating the challenges, inspired by (read: copying) other approaches, and learning of and how to use several new (to me) Rust crates.

Some folks were also going beyond just solving the challenges, going on to build interactive apps that visualise the challenge and their solution. On that point, [fasterthanli.me][fasterthanlime-aoc2022] is a site (and person) I highly recommend checking out, if you're interested in a series of articles detailing Rust solutions to the aoc2022 challenges. 

Inspired by others going beyond just solving the challenges, I decided to make an interactive web app visualising one of the challenges and my solution. Specifically **day 12** of the aoc2022 challenges, a `pathfinding` problem. 

I attached a screenshot of the interactive web app near the start of this post, but you can play with the *interactive web app* yourself in your browser here: [jwebmeister.github.io/aoc2022][gh-page-jwebmeister-aoc2022]

The challenge for day 12:
- `Goal`: find the `minimum number of steps` required to go from the `Start` location at ground level, to the `End` location 25 units above ground. 
- Travel from each cell is limited to the four closest orthogonally adjacent neighbouring cells, i.e. `North`, `South`, `East`, `West` `neighbours`.
- Travel is only permitted if the `elevation` of the destination cell is `at most 1 unit greater` than the current cells `elevation`.
- (Travel is also allowed if the destination cells elevation is less than or equal to the current cells elevation.)

In terms of solving the challenge, I solved it using `Breadth First Search (BFS)`.  

The app visualises each step of the BFS as it progresses through the challenges grid of cells, tracking:
- `current` cells being evaluated for their next move, 
- `visited` cells, and the previous cell they were travelled from,
- when the `goal` End location cell has been reached, the `path` (array of cells) that reached it, and 
- the `length of the path` to determine the minimum number of steps required to reach the goal.

It looks cool watching it run through the big grid!

In terms of tooling and crates, for the web app, I used [egui + eframe][gh-repo-egui] and [eframe template][gh-repo-eframe-template] for the GUI framework which I had used before, just not deployed to Wasm before. 

I found [egui + eframe][gh-repo-egui] easy to learn and use, and suprisingly performant considering it's an immediate mode GUI.

The [eframe template][gh-repo-eframe-template] has instructions on their github repo for deploying to Wasm using [Trunk][trunk-rs]. 

Deploying to Wasm was relatively painless. A few easily diagnosed issues were solved by "being inspired by" (copying or using) smarter / more experienced / better looking peoples code and crates. 

As examples:

- **Couldn't open files from Wasm**. Solved by being "inspired by" [woelper's egui_-_pick_-_file github repo][gh-repo-egui-pick-file].
- **Couldn't get systems current timestamp now() in Wasm**. Solved by using the [Chrono crate][gh-repo-chrono].
- **Trunk `serve`, web app didn't work**. Used `Chrome developer tools` to see the very descriptive error message, leading me to the Chrono crate mentioned above.
- **Trunk `serve`, web app didn't work or was outdated version**. Solved by going into the `Site Settings` in Chrome and deleted cached data.

I've waffled on long enough. There's hopefully enough useful information in there to make it worth reading, otherwise, there are links to the web app and code below.

You can run the egui app in your browser at [jwebmeister.github.io/aoc2022][gh-page-jwebmeister-aoc2022]

You can find the code at [github.com/jwebmeister/aoc2022][gh-repo-jwebmeister-aoc2022]


[gh-page-jwebmeister-aoc2022]: https://jwebmeister.github.io/aoc2022
[gh-repo-jwebmeister-aoc2022]: https://github.com/jwebmeister/aoc2022

[gh-repo-egui]: https://github.com/emilk/egui
[gh-repo-eframe-template]: https://github.com/emilk/eframe_template/

[trunk-rs]: https://trunkrs.dev/
[gh-repo-egui-pick-file]: https://github.com/woelper/egui_pick_file
[gh-repo-chrono]: https://github.com/chronotope/chrono

[fasterthanlime-aoc2022]: https://fasterthanli.me/series/advent-of-code-2022/
