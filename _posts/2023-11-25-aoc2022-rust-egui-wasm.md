---
layout: post
title:  "Advent of Code 2022, Rust, egui and Wasm"
date:   2023-11-25 19:57:00 +1100
categories: blog
tags: rust egui wasm webapp aoc2022
excerpt_separator: <!--more-->
---
I've been going through the [Advent of Code 2022][aoc2022] (aoc2022) challenges in an attempt to improve my coding skills in the [Rust][rust-lang] programming language. 

It's been fun so far! 

I'm up to [day 12][aoc2022-day12] of the challenges at the time of writing, and liked the challenge so much I made a *egui Wasm web app* for it: [play with it here!][gh-page-jwebmeister-aoc2022] 
(it runs in your browser)

[![aoc2022_day12_pathfinder_webapp](/assets/images/aoc2022_day12_pathfinder.png)][gh-page-jwebmeister-aoc2022]

<!--more-->
---

I did peek at a few solutions from others. I sometimes peeked when I ran into roadblocks, but I always peeked after I completed a challenge, curious to see how others approached it. 

I'm glad I did! 

I learned a lot by repeating the challenges using different approaches, "inspired by" (read: copying) other people, and learning of + how to use several new (to me) Rust crates. It's one of the reasons I'm coding in Rust, a helpful community and lots of useful open source code and libraries (crates).

Some folks were also going beyond just solving the challenges, going on to build interactive apps that visualise the challenge and their solution. One that stood out was [fasterthanli.me][fasterthanlime-aoc2022], I highly recommend checking it out if you're interested in a series of articles detailing Rust solutions to the aoc2022 challenges. 

Inspired by others going beyond just solving the challenges, I decided to make an interactive web app visualising one of the challenges and my solution for it. Specifically [day 12][aoc2022-day12] of the aoc2022 challenges, a [pathfinding][wiki-pathfinding] problem. 

I attached a screenshot of the interactive web app near the start of this post, but you can play with the *interactive web app* in your browser here: [jwebmeister.github.io/aoc2022][gh-page-jwebmeister-aoc2022]

---

The challenge for [day 12][aoc2022-day12]:
- `Goal`: find the `minimum number of steps` required to go from the `Start` location at ground level, to the `End` location 25 units above ground. 
- Travel from each cell is limited to the four closest orthogonally adjacent neighbouring cells, i.e. `North`, `South`, `East`, `West` neighbours.
- Travel is only permitted if the `elevation` of the destination cell is `at most 1 unit greater` than the current cells `elevation`.
- (Travel is also allowed if the destination cells elevation is less than or equal to the current cells elevation.)

In terms of solving the challenge, I solved it using [Breadth First Search (BFS)][wiki-bfs].  

The app visualises each step of the BFS as it progresses through the challenges grid of cells, tracking:
- `current` cells being evaluated for their next move, 
- `visited` cells together with the `previous` cell they were travelled from, making up several paths,
- when the `goal` end location cell has been reached, the `path` that reached it is determined by *backtracking* through the paths of the `visited` cells and their `previous` cells, until the start location cell has been reached, and 
- the `length of the path` to determine the minimum number of steps required to reach the goal.

It looks cool watching it run through the big grid!

---

One item of mild interest is that my current implementation is non-deterministic. The specific path from the start location to the end goal location can vary between runs. However, the minimum number of steps required to reach the goal does not vary.

Looking through my code, I used the Rust `std::collections` implementations of `HashMap` and `HashSet` for the BFS. By default, these implementations use a randomly seeded hashing algorithm, according to the [docs for HashMap][rust-doc-hashmap], with `HashSet` being an implementation of `HashMap` according to [docs for HashSet][rust-doc-hashset].  

That explains it!  

It should be fairly trivial to change over to a deterministic hashing algorithm, or to use different data structure implementations, but the solution for the challenge only needed the *number of minimum steps* to reach the goal, so I haven't bothered to change it.

---

In terms of tooling and crates for the web app, I used [egui + eframe][gh-repo-egui] and [eframe template][gh-repo-eframe-template] for the GUI framework. I had used them before, just not deployed to Wasm before. 

I found [egui + eframe][gh-repo-egui] easy to learn and use, and surprisingly performant considering it's an immediate mode GUI.

The [eframe template][gh-repo-eframe-template] has instructions on their github repo for deploying to Wasm using [Trunk][trunk-rs]. 

Deploying to Wasm was relatively painless, though I concede the web app I built is fairly simple. A few easily diagnosed issues were solved by being "inspired by" (read: copying or using) smarter / more experienced / better looking peoples code and crates.

As examples:

- **Couldn't open files from Wasm**. Solved by being "inspired by" [woelper's egui_pick_file github repo][gh-repo-egui-pick-file].
- **Couldn't get systems current timestamp now() in Wasm**. Solved by using the [Chrono crate][gh-repo-chrono].
- **Trunk `serve`, web app didn't work**. Used `Chrome developer tools` to see the very descriptive error message, leading me to the Chrono crate mentioned above.
- **Trunk `serve`, web app didn't work or was outdated version**. Solved by going into the `Site Settings` in Chrome and deleted cached data.

One item on my "next steps" list is to figure out how to embed an egui web app within a web page, with relative position (e.g. app position moves when scrolling down the page), and multiple other elements, e.g. a blog post like this.

Every attempt I've made so far to embed the egui app within a web page, has the app move (paint) to the top of the browser after any interaction, instead of staying in-place halfway down the page where it was initialised.  This might be a limitation of egui, it's rendering backend, or something else entirely, but I haven't dived deep enough to pin-point and confirm the root-cause, nor figure out any workarounds.

---

I've waffled on long enough. There's hopefully enough useful information in this post to make reading it worthwhile, otherwise, there are links to the web app and code below.

You can run the egui app in your browser at [jwebmeister.github.io/aoc2022][gh-page-jwebmeister-aoc2022]

You can find the code at [github.com/jwebmeister/aoc2022][gh-repo-jwebmeister-aoc2022]


[rust-lang]: https://www.rust-lang.org/
[rust-doc-hashmap]: https://doc.rust-lang.org/std/collections/struct.HashMap.html
[rust-doc-hashset]: https://doc.rust-lang.org/std/collections/struct.HashSet.html

[aoc2022]: https://adventofcode.com/2022
[aoc2022-day12]: https://adventofcode.com/2022/day/12

[gh-page-jwebmeister-aoc2022]: https://jwebmeister.github.io/aoc2022
[gh-repo-jwebmeister-aoc2022]: https://github.com/jwebmeister/aoc2022

[gh-repo-egui]: https://github.com/emilk/egui
[gh-repo-eframe-template]: https://github.com/emilk/eframe_template/

[trunk-rs]: https://trunkrs.dev/
[gh-repo-egui-pick-file]: https://github.com/woelper/egui_pick_file
[gh-repo-chrono]: https://github.com/chronotope/chrono

[fasterthanlime-aoc2022]: https://fasterthanli.me/series/advent-of-code-2022/
[wiki-bfs]: https://wikipedia.org/wiki/Breadth-first_search
[wiki-pathfinding]: https://wikipedia.org/wiki/Pathfinding