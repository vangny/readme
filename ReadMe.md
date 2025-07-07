# Purpose of This Repository

A few notes before you dive into this doc:

- This is a living document — a personal journal of my evolving thoughts on software engineering. It reflects my experience, not universal truths. I update it when something shifts in how I think or work. You're welcome to read along.
- Expect strikethroughs and annotations as I keep outdated thoughts around as a record of how I’ve changed/grown.
- I'm opinionated but not dogmatic, nothing here is set in stone. 
- This is my personal workflow, and does not perfectly reflect how I contribute to a team or codebase. The best workflow when working with others is the team's workflow.
- If you want the full history of the doc, [check the commit log](https://github.com/vangny/readme/commits/main/).

# Navigation
1. [Project Architecture](#project-architecture)
2. [Local Development](#local-development)
3. [Tests](#tests)
4. [Project Planning](#project-planning)
5. [Process](#process)
6. [Tools](#tools)
7. [Bucket List](#bucket-list)

# Project Architecture
I like monoliths. I like microservices. I like using the right tool for the right job.

When it comes to starting a project, I default to a monoliths. There's little to no reason why you would need to take advantage of microservices so early on in development. There's no scaling issues (you have no users) and there shouldn't be any organizational issues (you have no code), so why add another layer of complexity? We should strive to keep things as simple as possible. I will say, however, monoliths should try to be organized and modular (aka modular monoliths). That way we can take advantage of microservices at the technical level if/when we get to that point.

I default to a layered architecture due to how common and familiar it is.

I have tried experimenting with using a vertical slice architecture in small projects as opposed to the generic layer approach and I kind of like it. It's not better or worse, it's different. The best thing about it is code colocation. It's easy to scan, easy to maintain, and very scalable. With that said, it feels like maintainers must know what they're doing within the codebase otherwise the architecture crumbles away really quickly. *I say that, but it almost feels like it would be hard to do so with how everything is organized? I don't know. It definitely deserves to be looked at again and maybe from a different perspective* 

> 📝
> 
> I'm a big fan of modular monoliths and will use microservices when I can argue it'll benefit the project at a technical level and not just at an organizational level.
> 
> I default to a layered architecture but have dabbled in vertical slice


# Local Development Environment
In the past I've tried to keep things really minimalistic. Just my code editor, the default terminal and Postman for when I didn't want to use `curl`. 

Then I went through a couple editor phases- starting with Sublime, a brief stint with WebStorm, and then I mained VS Code for the past couple of years. I've recently given Cursor a try and it's not bad. It's just another flavor of VS Code with good tab completion. I have not tried vibe coding nor do I have the want to.

I also started diving into the terminal, doing things like using iterm2, adding plugins, and switching to kitty and WezTerm (current). I know of Ghostty, am a fan of Mitchell Hashimoto, but haven't found a reason to move over. Maybe if I ever decide to switch to NeoVim or Helix then I'll switch terminals too for the fun of it.

As far as actual tools that I like to incorporate in a project locally, all I really need is Docker. Docker compose is life. At the very least I containerize my DB for local development. This provides me with an isolated space alongside consistency and portability.

I'll add in nginx whenever I want to get a little fancy and that's really about it.

> 📝
> 
> Current dev setup involves: a MacBook Pro, Cursor as my editor, WezTerm as my terminal, Postman for some API related tasks, and Obsidian for notes.
> 
> I like utilizing Docker compose to containerize my local DB and occasionally nginx.
> 
> Oh, and Catppuccin


# Tests
Everyone's favorite topic. Testing is great. What isn't great is having my architecture determined by tests along with wasting time creating tests that will ultimately be refactored by the end. 

Test Driven Development (TDD) can be okay in very specific cases; if there are components that are going to be used consistently and will more than likely never change (like a parser) then I'll likely incorporate something similar to TDD.

Outside of that, TDD has the potential of wasting a lot of time. Software Development is a zero sum. The time that I spend to get tests up and running for non-existent code with non-concrete solutions is time I'm not spending on coding the actual feature or fixing the bug. Not only that, I am very likely to build the solution at least twice over before I feel good about the implementation (a prototypical phase before the final solution). This means I wasted time on those initial tests because the implementation and ending result are different now which means I'll need to rewrite the tests.

Let's talk about another fun topic: code coverage. Code coverage tells you one thing: the quality of tests. In my experience if you are adding proper tests as they implement features and fix bugs, code coverage should naturally sit above 70%. So yes, a target/floor should be established. The problem comes when the target is much higher as it then encourages developers to write tests for the sake of writing tests instead of focusing on writing **quality** tests. This wastes time and energy in the present, and will likely waste more time and energy down in the future when an inevitable refactor comes along.

Lastly, the beautiful big three types of tests: unit tests, end-to-end (E2E) tests, and integration tests. While all three have their place in a codebase, they shouldn't be treated the same.

Unit tests are the most helpful tests to implement early on. But that doesn't mean they should be treated as concrete or all-knowing. As the project grows they are the most likely to break, have bugs, and impede progress. You shouldn't be surprised when you end up just tossing some of these away. Thus, I spend the least time incorporating unit tests. 

E2E tests are second in my priority of tests. They're great when it comes to ensuring an entire system works, but when they break they'll likely lead to some unwanted and intense conversations with your rubber duck. I like to make sure these tests are strong and only cover high traffic features and edge cases. Spend time on these once and you should never have to touch these unless the system has fundamentally changed.

Integration tests are what I consider the sweet spot and spend the most effort on. They test for the validity of the system (not the the extent of E2E tests) while having a better debugging process than E2E tests. I implement these where I can.

> 📝
> 
> I like implementing tests along the way instead of following the ways of TDD as it allows me to be more productive and produce higher quality code. 
>
> I incorporate unit tests early, but do not prioritize them.
>
> I write just enough E2E tests to cover high traffic features and edge cases.
>
> I value integration tests the most as they test at a high enough level while being maintainable and easier to debug compared to E2E tests.


# Project Planning
These are simplified guidelines that I use when planning out a project.

1. Clarify The Goals
	1. Why are you making this project?
	2. Who is it for?
	3. What's so special about it?
	4. What's the format?
2. Write User Stories
3. Figure Out The Data Models
4. Set Your MVP Limits
5. Very Rough Sketch
	1. DO NOT WIREFRAME- grab your ipad or a piece of paper and a pen. Treat it as a literal sketch, it should be crude and simple. We're way too early to start thinking of actual designs for any feature and it'll likely change 20 times over the course of development
6. Determine the Scale of the Project
	1. How long should the MVP take
	2. How long should the entirety of the Project take
	3. How many users will be utilizing this project?
		1. Will it even support users outside of you? Maybe a few? Maybe north of a thousand?
7. Starting Tech Stack

At this point I'll be piecing out tickets for the MVP and start developing.

>📝 No summary here


# Process
A better section name would be **Agile** because that is THE process these days.

I like Agile. Agile's core principles are great and most if not all Engineers should give the manifesto a read. I love it when the team can do the following:
	1. Iterate as fast as possible
	2. Pivot when needed
	3. Discuss about immediate features 
	4. Have a simple and flexible process

I dislike Agile. Agile at a corporate level devolves into an overly complicated process with the focus shifting to developing more processes rather than focusing on getting shit done. It's a rigid process that slows things down- we over plan things before even attempting to address whatever issue we're looking at. We're not working with wood here (yet), the thought process of "measure twice, code once" doesn't exist in software.

Then we have those that dislike individual teams having their own processes because it "looks messy" or "unorganized". What happens next? A net is cast over the entire org and numerous processes are created that spawn nested processes because each team handles things differently. So now teams are left with more processes specific to their team while having to deal with this awkward globalization of processes that slows everything down. They'll then take bits and pieces of scrum (which at this point is an umbrella of thousands processes) and sprinkle it everywhere while using Jira/Trello/AirTable/etc. And then they label it "Agile". Oof.

> 📝
> 
> Agile can be great when engineers follow the core values. Anymore than that and I find you get stuck in an endless loop of building processes atop of processes. At the end of the day we're not here to build processes, we're here to build software.
>
> "Agile is doing what is valuable and not doing what is not"
> -Somebody smarter than me


# Tools
These are the tools on my tool belt, not every tool in my workshop.

- Git
	- Default to GitHub as provider
- JavaScript/TypeScript
	- Node.js
	- React
	- Next.js
- Python
- SQL
	- MySQL
	- Postgres
- NoSQL
	- DynamoDB
	- MongoDB 
- Docker
- AWS
- GraphQL

> 📝 No summary here


# Bucket List
These are technologies that I have some interest in taking a look at. They vary from just reading the docs to taking a deep dive.

- [Jujutsu](https://github.com/jj-vcs/jj)
	- Why not?
	- Not a deep dive
		- Use it for a small personal project- could even just be a throwaway for this
- [Rust](https://www.rust-lang.org/)
	- Most likely the next language to experiment on
	- Would mark the beginning of diving deeper into lower level code than web development
	- More than likely a deep dive
- [Zig](https://ziglang.org/)
	- Maybe once it hits 1.0
		- I'll take a look at docs once it hits 1.0
- [Elixir](https://elixir-lang.org/)
	- Functional Programming!
	- Concurrency!
	- It feels like a really niche language that could get me into trouble vs learning Rust
	- Challenges Rust in interest
- [Helix](https://helix-editor.com/) or [NeoVim](https://neovim.io/)
	- Leaning towards Helix
	- Demystify the world of editing code on the terminal and begin my ricing arc

> 📝 No summary here