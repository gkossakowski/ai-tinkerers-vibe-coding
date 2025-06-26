## Introduction

I'm working on a new project with a senior engineer who has expertise in product development and front-end engineering. I have more expertise in AI engineering and back-end and systems engineering. We are working on a web product called Unpitched. We are in the very early stages of brainstorming this product. Our constraint is that we want to ship it in three weeks. We are both senior, just to remind you. And we want to create a PRD, or project requirements document, for this project.

Here's a rough idea of the product with main thought behind it:

```
Many startup founders stumble when talking to potential customers—defaulting to “pitch mode” instead of learning. The main idea is to operationalise the best practices from The Mom Test book by Rob Fitzpatrick. Our app helps founders prepare for the interviews, check interviews against the best practices, for example detecting founders switching to pitch mode rather than learning about the customer. 

The key enabling technology is to use LLMs to help with the process. LLMs let us provide the "magic" of taking unstructured brain dump and conversation transcripts, and performing tasks that human (e.g. external consultant) would do.

The result? Faster validation cycles, fewer false positives, and a founder team that can talk to users with the same confidence they write code—all because an opinionated workflow makes it impossible to take shortcuts. Stop guessing, start learning, and ship products customers actually need.
```

For now, the task will be to brainstorm details of the project and identify key missing assumptions or unclear ideas behind the product. After going back and forth a few times, we will write down the PRD. I'll give you an example of a PRD from another project that worked really well. You should focus on extracting the style of writing, which is very concise and to the point. The style of planning uses the walking prototype idea in terms of sequencing tasks, and it discusses technology, user flows and all those things. So you should focus on the structure and fine details of the plan, of the PRD. And we would like to emulate this for this new project. You should take note of any other details of the example PRD that you think are important for the new PRD.

This new project is code-named Unpitched for now. Our priority for this PRD and the scope we'll be discussing is to ship a working end-to-end product. The absolute priority is getting the core functionality working, and creating a wow experience for the user. Security, privacy, etc. are not a priority for now. This is due to the time constraint, and PoC nature of the project.

---

We had some brainstorming session already. We tried to figure out "jobs-to-be done" for the product (as addressing users' needs). Here's a dump of the summary of that session:
```markdown
This meeting focused on designing a tool to help with customer interviews and recruitment processes, particularly for technical founders who struggle with conducting effective non-pitching interviews.

### Product Components

- **Pitch Creation**: An internal tool to help articulate hypotheses about what's being built and for whom. Input is an unstructured "braindump" from founders, and output is a structured pitch document with clear hypotheses.
- **Interview Scenario Preparation**: Guiding users through creating an interview structure with best practices. This includes generating questions and providing a step-by-step interview script.
- **Question Analysis**: Evaluating interview questions against best practices and providing feedback on question quality.
- **Interview Analysis**: Providing feedback on conducted interviews, analyzing whether the interviewer pitched instead of listening, balanced speaking time appropriately, and followed the planned structure.
- **Future Features**: Question saturation tracking, collective analysis across interviews, identifying repeatable patterns, and question improvement suggestions, create a "dry run with LLM" feature for practicing interviews

### Development Priorities

- Desktop as the primary target platform, with mobile as secondary
- Create a "walking skeleton" or "tracer bullet" approach to development
- Focus on shipping a working end-to-end product that users can log in and use
- Build an "opinionated software" that guides users through the best practices
```

These are not great but give you some starting points and rough ideas.

## Piggybacking on the Circleback

There's this AI notetaking app called Circleback: http://circleback.ai

It stands out as the best at extracting action items, numeric data, key insights, non-obvious points, etc. from a meeting. It handles audio meetings, has an option to upload audio recordings, and it's excellent at transcribing the meeting.

For Unpithced, we plan to directly integrate with Circleback. It's either a manual integration where users will be asked to manually paste the transcript of the meeting and Circleback-generated summary, or an automatic integration where we will use Circleback's API to get the transcript and summary. This is yet to be decided, probably based on the time required to implement the integration.

## The origin of the idea

I (Grzegorz) recently helped a technical team with their very early stage product development. The first thing I noticed is that they were clearly breaking principles of The Mom Test, especially drifting into pitch mode, and spinning wheels as a result.

Patrick (the other senior engineer) has joined the project and we want to explore the idea of creating the "digital twin" to the Mom Test book.

## Non-priorities

- market evaulation
- competition evaluation
- RWD support for mobile devices
- data privacy and security

We should assume that this is a PoC and a fun project to work on. The go-to-market strategy is not a priority at this stage. A tiny go-to-market strategy is to launch at the Warsaw AI Tinkerers event that is due in four weeks.

## Example PRD

Here's the example of a PRD that worked really well for the project called `store.new`:
``````markdown
<!--
Here should go the example `new.store` PRD. see examples/unpitched-prd-brainstorming.md where a prompt with this example is fully assembled
You can also take a look at the source of that example that lives in its original repo here: https://github.com/yournextstore/new.store/blob/main/docs/new-store-prd.md
-->
``````

## Your task

Carefully analyze the initial outline of the project or the initial direction and let's brainstorm on the product, especially in the time constraint of 20 days. What do you think should be a set of features or good ideas that we should consider? Or do you have open questions? Or do you even think this is a good idea as a product? And also I gave you a very detailed and a real example of a PRD. Let me know if it's not too long for you. Maybe it's overwhelming and there are too many details and it's hard to analyze. So let's focus on those two things for now and we'll be going back and forth for a while.
