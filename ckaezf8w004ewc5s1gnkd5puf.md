## How to Ask Effective Questions: A Practical Guide for Developers

Learning is a journey that never ends. At every point in your career, you will keep learning, re-learning, and un-learning.

The ability to find answers to problems is key, and these answers can be gotten by either debugging, googling, or asking questions. These are skills everyone should learn.

While asking questions is great, doing it the wrong or less effective way might lead to many hours of unproductive work. In this article, I'll show you how to ask effective questions, become a better googler, and hone your problem-solving skills.

## The Read Search Ask Method

freeCodeCamp came up with this amazing method for their students called the [Read Search Ask](https://www.freecodecamp.org/forum/t/how-to-get-help-when-you-are-stuck-coding/19514) method where you can solve your problems efficiently alongside respecting other people’s time, too. It is expected that you follow these three steps in order before you ask a question.

- **Read** the error or documentation
- **Search** Google or Stackoverflow
- **Ask** for help

### 🔬📚 Read

**Read your Errors**

The first step to finding a solution(s) to your problem is understanding the problem itself. Many developers ask questions without understanding the problem. Remember you want to ask questions efficiently and respect the individual you will be asking. Most often, the answers to your bugs are in the errors themselves. It wouldn't be nice to ask questions that you could have solved yourself if you had read the errors themselves.

One great way to debug your errors is to log the error on your console or terminal and read the errors. Five things can happen at this stage:

- You identify the bug
- You determine the location of the bug (possible a file or section of your code)
- You understand the cause(s) of the bug
- You outline possible fixes of the bug
- You implement the possible fixes

Most often, just this step alone can help you solve your problem, and the more you practice this, the better you become at debugging and fixing issues. Some bugs might be more complex than your capacity, and you need to seek external help or resources.

**Read Documentation**

Let's assume you couldn't fix your issues from the first step (but you could identify the bug at least); then you need to read some documentation. This might not apply to all bugs, but ensure to run your issue through this step before moving to the next. After identifying your bug, it's time to determine the cause and outline possible fixes.

> Documentation is a set of documents provided on paper, or online, or on digital or analogue media, such as audio tape or CDs. Examples are user guides, white papers, on-line help, quick-reference guides. Paper or hard-copy documentation has become less common. ~ [Wikipedia](https://en.wikipedia.org/wiki/Documentation)

Documentation serves as the official guide of a particular programming language, framework, library, or technology. The best place to get first-hand resources on a specific issue is to check the technology's official help guide. You might have misconfigured something, installed some wrong package, forgot to import something, and reading the tech's docs responsible for the bug will help you find a fix quickly. Recently I was working on a Gatsby project, and I ran into some console errors and a blank white page in production; meanwhile, this didn't occur in development.

```
TypeError: t.test is not a function
```

So vague, right? After identifying the bug location, reading the docs, and trying out several fixes, I discovered that in the gatsby google analytics plugin configuration, I left the array meant to avoid sending pageview hits from custom paths empty.

```
plugins: [
    {
      resolve: `gatsby-plugin-google-analytics`,
      options: {
        trackingId: 'UA-XXXXXXXX-1',
        head: false,
        anonymize: true,
        respectDNT: true,
        exclude: [''],
        pageTransitionDelay: 0,
      }
]
```

After 3 hours of reading the error, identifying the bug, and reading Gatsby docs, I figured that the `exclude` array had no values in them, and removing this fixed my issue since I didn't need to exclude any page after all. This shows why you should spend some time debugging. It might take some time; it will be frustrating, the bug might look stupid, the fix might be simple, but it's worth it. The more time you spend debugging, the better you become, and the faster you will fix even more complex bugs next time.

![EWOBv1cXgAEhi7N.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1588248728371/qXwmBU8Fm.jpeg)
~ [meme src :)](https://twitter.com/dabit3/status/1252987819368353792)

### 🔍 Search

Now you have read your errors and several docs, but your bug is becoming more complex, it's time to search the web "effectively." One best place to search for solutions to your issues is [Google](https://google.com) since it already crawls content from several webpages, dev communities and docs like [StackOverflow](https://stackoverflow.com/), [Hashnode](https://hashnode.com/), [FreeCodeCamp News](https://www.freecodecamp.org/news/), [MDN](https://developer.mozilla.org/en-US/docs/Web), [CSS tricks](https://css-tricks.com/), [Hackernoon](https://hackernoon.com/), amongst many others.

Here are some best Google search tips you can try to get answers better efficiently:

- Add a specific domain to channel your search to a particular website and save some time. You can append the `site: sitename` to your search, and it'll return only results from that website.

![Screen Shot 2020-05-12 at 12.49.06 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1589268176790/vwk3EmzK9.png)
- Search for specific titles and text in specific sites. This will allow your results to include resources related to the title or text keyword you specified.

> intitle:axe

> intitle:axe intext:web ui testing

> intitle:axe intext:web ui testing site:bolajiayodeji.com

![Screen Shot 2020-05-12 at 12.48.59 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1589268185857/KA_B5_TTq.png)

- Add specific keywords to your search and pull out individual details like file paths. If your bug is related to Python, add it to your search query; if related to Objects, add it. This will streamline the results to a wider range of possible resources related to your bug as there are Objects in just almost every programming language.

-  Google automatically omits most non-alphanumeric characters from your queries. Symbols like **`!@#$%^&*(){}[]<>** are not included in your search. You can hence focus on more specific keywords, as discussed above.

- Copy and paste your errors (removing specific information); there is a 99.9% chance that someone else has encountered the same error and has maybe opened some issue or written an article about it. Never underestimate the power of StackOverflow and GitHub issues.

- Search within the past few years since programming changes in just some time. This will ensure you don't hit redundant resources.

- Reiterate, try different keywords and more general keywords multiple times and open multiple tabs until you find an answer. This might be awkward at first, but as you consistently do this, you'll get better, and with time it will take you less time and tabs to find an answer.

### 🗨️ Ask

Now comes the sought diamond. I would advise, before you ask ANY question, ensure you have completed steps 1 and 2. This might be hard, but the earlier you get used to this, the better you grow. I've had people ask me questions, and when I copy and paste their question on Google, the first result answers the question 100%, and this doesn't feel great. Most often, I'll have to send the link to them; meanwhile, they could have done this themselves and save me some time alongside increasing their problem-solving skill.

Even if your next-door neighbor works at Google, if your Dad is a Software Engineer, if your close friend has two years' experience than you, try not to ask them questions until you have invested time into finding solutions yourself. This would help you:

- Build more self-confidence as you won't need to rely so much on others. (What if that close friend is unavailable to respond to you someday, what will you do?!)
- Save the time of whomever you are planning to ask questions. There are tons of developers worldwide, and you might not be the only one asking that same person questions. By completing steps 1 and 2 first, you are also helping others with lesser experience than you or more complex problems to get answers quickly.
- Build your problem-solving, debugging, research, and googling skills. These are essential skills that will help you become a better developer. You only master a skill when you consistently practice it, so ensure to practice this regularly and watch yourself grow and master the art.

%[https://twitter.com/iambolajiayo/status/1255694731482365952]

---

But let's say that you have completed both steps, and you still need external help from a mentor, senior developer, team lead, the local community, group, or friend. How then do you ask questions effectively?

- Complete step 1 and ensure you understand the problem already
- Complete step 2 so you might at least have gotten some insights into possible causes and solutions of the problem
- Now, make some of your research; you are either asking the question in dev communities like [Stackoverflow](https://stackoverflow.com/) or [Hashnode](https://hashnode.com/) or requesting help from an individual you feel has more experience than you.
- Developers answering questions on dev communities are sacrificing their time to help you. Help them also by asking "clear and concise questions." It would help if you chose your words deliberately and precisely, constructing your sentences carefully to avoid confusion. From step 1 and step 2, properly draft your questions based on:
  - The "problem" you have encountered 
  - Your thoughts on what you think might be wrong, "based on your research."
  - Proof of research efforts (Devs would be happier to help you once they see you have made some effort already). Add links to resources you have checked and solutions you have tried already
  - Be conversant with tools like [CodePen](https://codepen.io/), [CodeSandBox](https://codesandbox.io/), [GitHub Gist](https://gist.github.com/), [Repl.it](https://repl.it/), and [GitHub](https://github.com/) so you can easily provide a link to a snippet of your code, a working project or [mimimal reproduction](https://gist.github.com/Rich-Harris/88c5fc2ac6dc941b22e7996af05d70ff) without having to type so much text. **Please try as much as possible not to paste code that is more than one line in chat.**
  - Take clean and clear screenshots where necessary. Most often, you can take a snapshot of your console errors for smaller issues. Ensure you don't strain the eyes of whomever you are asking a question. Take specific and clear screenshots related to your error.
- Be sure you're asking the right person or community. Don't ask a python related question to someone who knows just Java. Your research from the previous step will help you here. It's also great to bookmark specific communities, individuals, or groups where you will regularly ask questions based on how effective their responses have been to you.
- Now, don't be afraid to ask. I've had my share of toxic responses from people who respond with comments like "this is simple," "come on, google it," "you should know this," and you might have too :(. The internet is a combination of good and toxic individuals who might be or not welcoming. Be confident in yourself; you have done your part by completing steps 1 and 2, so ask the question freely.

## Conclusion

You don't need to "know it all"; you need to "know it and know-how and where to find more knowledge."

Dear 10x, Senior, "It's Simple," Engineer, please note that you're hurting developers who ask questions. I had to battle so much with my self-confidence some years ago, and it took me a while to get over it. There is so much for learners to battle with already (learning, imposter syndrome, and personal issues). Please don't add to it, be welcoming, make them feel like they belong here, and support them.

Your response can intentionally or unintentionally influence someone's decision to ask questions freely next time. If you can't or won't be available, you can either not respond at all or respond friendly with feedback. Refer people to your friends if you don't have the capabilities to attend to them, give constructive criticism, and ensure you don't leave a question without feedback or impact.

> Beginner developers need support. Learning to code is hard, especially if you're doing it alone. If you're learning in a traditional classroom, be sure to network with the other students. Do homework together. Discuss the problems. If you're learned online, it's very easy to get discouraged. Find chat spaces with others on a similar journey and use that space to encourage one another. Twitter also makes the experts accessible to you (reason #49948 why I love Twitter). Find the experts in whatever it is you're learning and consume their content. Ask them questions if you need to. The key is not to do it alone. ~ [Angie Jones](https://twitter.com/techgirl1908)

The industry is increasing daily; we are all trying to learn and get better at different levels. A lot of developer [communities](https://bolajiayodeji.com/best-developer-communities-to-be-part-of-in-2020-ck7ugplig01a9zis174d7zrnk) are supportive and making resources available for consumption. Ensure you are a part of this movement, consume available resources, contribute to these resources, and be a helper in any way you can.

Thank you to all the amazing developers across the globe, creating and sharing content/ projects. Your contribution(s) are the pillars holding the tech ecosystem today. 🙏💙

> Quick note, I interview awesome women in tech on the [She Inspires](https://hashnode.com/series/she-inspires-cjt0d02lq001e7ps2wo420g15) at [Hashnode](https://hasnode.com) where I understand the current health of the tech industry, get insights from their personal and career growth, and inspire other women to become better. Read all past interviews [here](https://hashnode.com/series/she-inspires-cjt0d02lq001e7ps2wo420g15); trust me, it's worth your time. :)

Don't spend your entire life waiting for the best time making that move, write that article, build that side-project, apply for that job, or ask that question today. The best time is always now!