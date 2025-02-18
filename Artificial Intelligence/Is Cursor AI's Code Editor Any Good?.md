[Is Cursor AI's Code Editor Any Good?](https://randomcoding.com/blog/2024-09-15-is-cursor-ais-code-editor-any-good/)
====================================

-   14 September 2024
-   [ai](https://randomcoding.com/tags/ai/),
-   [nodejs](https://randomcoding.com/tags/nodejs/),
-   [javascript](https://randomcoding.com/tags/javascript/),
-   [evaluation](https://randomcoding.com/tags/evaluation/)

**TL;DR** - Cursor probably has the best developer experience out of all the AI code editors I've used. This is largely because of the multi-file code generation using Composer and the diff-viewer UX that they use to quickly show the changes applied to the code base.

Read on!

I write code almost every day and have been for the past couple of decades. When I started writing code, I didn't have auto-complete or even auto-correct. And now, we have LLM-empowered IDEs just generating entire projects for you. Amazing times! Still, sometimes it can be hard to filter out the signal from the noise.

Last week I tried out the 'new hotness' in the AI IDE space - [Cursor](https://www.cursor.com/). They recently raised [60 million](https://www.cursor.com/blog/series-a) in their Series A and everyone on Twitter has been raving about how good their code generation is. Cursor is built on top of Visual Studio Code, so if you're familiar with VSCode, then you'll feel right at home.

To test out its capabilities, I tried creating an exercise-tracking web app. Here are the features I wanted.

-   Track workouts and metadata like duration and calories burned
-   A workout would have multiple exercises that target a muscle group
-   Exercises have multiple sets
-   And sets would have a number of reps and a weight

Pretty basic stuff that tested the IDE's ability to generate multiple entities and create relationships between them.

![A screenshot of a web app showing a listof recent workouts, calories burned and duration](https://randomcoding.com/img/4hEmSRFi0n-1306.webp)Workouts -> Exercises -> Sets

Code Generation [#](https://randomcoding.com/blog/2024-09-15-is-cursor-ais-code-editor-any-good/#code-generation)
-----------------------------------------------------------------------------------------------------------------

First, a quick word about [Composer](https://changelog.cursor.sh/#037---composer-beta).

I've never used anything like it before. Composer has a friction-free developer experience that makes the development flow feel a lot more natural. Most of the tools I use that have AI baked in have the code generation functionality in a separate window. Anytime you ask it for suggestions, it will generate the code in that window, and then (in the better tools) you can apply the code or (in the less mature ones) you can copy/paste the changes.

With Composer, you can create a project and group requests together and your instructions are applied across the whole project. You can add specific files from your project that provide additional context.

Cursor does its thing and then the Composer UI recommends all the changes that should be done across files and you can review the diff and then apply all or part of it. You can keep iterating in this view until you get what you need.

This has a big impact on someone who doesn't know programming and which parts of the code that should be updated, as Composer does all the work.

![A screenshot of Composer generating code andrequesting permission to apply the changes across multiple files](https://randomcoding.com/img/fXdtp_Q_E2-2437.webp)Composer doing its thing

Composer is still in beta, but you can turn it on from settings.

You also have all the other forms of code generation like AI auto-complete, AI chat, and in-place code editing. All of these features use the diff mode to apply code changes to your files, which is great.

You can see a full list of the released features here : <https://www.cursor.com/features>

Code Quality [#](https://randomcoding.com/blog/2024-09-15-is-cursor-ais-code-editor-any-good/#code-quality)
-----------------------------------------------------------------------------------------------------------

Most LLM-based AI don't have trouble with basic code generation like boilerplate code and basic CRUD applications. It's also great at more complex code generation tasks like algorithms. It's everything in between that they struggle with - at least in my experience.

I opened up two separate editors, one for the API using nodejs and one for the web app using VueJS.

### Coding the API with Nodejs [#](https://randomcoding.com/blog/2024-09-15-is-cursor-ais-code-editor-any-good/#coding-the-api-with-nodejs)

I used Composer and started prompting the creation of controllers, models, and routes. It took a couple of tries to get it organized properly because the AI liked dumping it all together. The API methods just had filler methods as I intended.

![A screenshotof Cursor's file view showing the API split into the controller, migration,routes and config folders.](https://randomcoding.com/img/yumkytpuru-479.webp)Took a couple of prompts to get to this file organization

I then asked it to create the DB schema using SQL Lite, which took a couple of iterations as the data types were generic. But it ended up with a decent schema.

```
const sqlite3 = require("sqlite3").verbose();
const db = new sqlite3.Database("./database.sqlite", (err) => {
  if (err) {
    console.error("Error connecting to the database:", err.message);
  } else {
    console.log("Connected to the SQLite database.");
    createSchema();
  }
});

function createSchema() {
  db.serialize(() => {
    db.run(`CREATE TABLE IF NOT EXISTS muscle_groups (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      category TEXT NOT NULL,
      name TEXT NOT NULL UNIQUE
    )`);

    db.run(`CREATE TABLE IF NOT EXISTS exercises (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      muscle_group_id INTEGER NOT NULL,
      name TEXT NOT NULL UNIQUE,
      FOREIGN KEY (muscle_group_id) REFERENCES muscle_groups(id) ON DELETE
CASCADE ON UPDATE CASCADE
    )`);
.
.
.
    console.log("Database schema created successfully");
    db.close();
  });
}
```

And in the last step, I got it to install [sequelze](https://sequelize.org/) and generate some models that were used by the controller to return the correct API responses.

#### Closing Remarks [#](https://randomcoding.com/blog/2024-09-15-is-cursor-ais-code-editor-any-good/#closing-remarks)

Pretty smooth execution for the basics. The biggest issue it had was that Cursor created a circular dependency that could only be solved by moving the entity associations to another file.

About 60% of the instructions needed multiple iterations because the decision-making and assumptions made in the code generation weren't good, so those needed better prompts. Some of the prompts were pretty detailed and you could argue that defeats the point of using an AI to do the work for you, but requiring specifics just comes with the territory.

### Coding the Web Application with VueJS [#](https://randomcoding.com/blog/2024-09-15-is-cursor-ais-code-editor-any-good/#coding-the-web-application-with-vuejs)

I chose VueJS because I'm more familiar with it than React and could evaluate the code that's being put out. Cursor gave me the instructions to set up the Vue CLI and get it running locally. I then added Bootstrap CSS to give it a basic style (at the time, I didn't think of asking it to change the styles).

With a couple of prompts, I was able to get it to create all the CRUD views for all the entities I had in my API. At one point I asked it to use a store and then it updated the code to a much cleaner approach using stores and services to connect to the API.

![A screenshot of Cursor's file viewshowing the web application split into separate folders like components,helpers, services and stores](https://randomcoding.com/img/wCfve_n0nH-453.webp)File list for the web application

The code was mostly fine, if a little too verbose. It used components so it didn't repeat form code in the CRUD views, but it didn't break down the smaller UI components so those weren't repeated across files.

I also asked it to create more modern UIs and it came up with some decent (if bland) options.

![A screenshot ofUI of the web application that was designed](https://randomcoding.com/img/6aSRZXanA4-1337.webp)It's much better than me at designing, that's for sure

#### Closing Remarks [#](https://randomcoding.com/blog/2024-09-15-is-cursor-ais-code-editor-any-good/#closing-remarks-1)

While the actual code itself was fine, I had to prompt quite a few times to get better code organisation. It did a pretty good job cleaning up the UI using the Bootstrap framework that I added.

Verdict [#](https://randomcoding.com/blog/2024-09-15-is-cursor-ais-code-editor-any-good/#verdict)
-------------------------------------------------------------------------------------------------

Really impressive in terms of the developer experience. I think this is the direction that AI code tools need to take. I loved using the IDE and the features, everything felt pretty seamless. It was a good choice for them to build on top of VSCode.

Code quality was pretty much what you get from any standard LLM. And somewhat expectedly, the LLM doesn't do great in the noncode writing parts of software development. Picking a good solution, organizing the code and keeping the solution consistent are all parts of a developer's core skillset.

I think we're pretty much at the point where you can have nontechnical people generate a prototype to validate any idea without any coding knowledge. The artifacts might not stand the test of time, but if that prototype is enough to raise some funding or show the value of some idea, then it served its purpose.

For me, LLM-based AI tools have been really good at solving units of work but not so great at the larger piece. I use these tools all the time to do things like generating boilerplate or unit tests but I don't think they are anywhere near replacing developers in a team. Having said that, the gap between devs who have AI tools and those who don't are going to be pretty big. I **want** the AI to handle the boring bits so that I can focus more on the more interesting parts of my job.

-   Previous: [The Passport Saga](https://randomcoding.com/blog/2024-05-05-the-passport-saga/)