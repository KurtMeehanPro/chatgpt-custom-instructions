# ChatGPT Custom Instructions

## tl;dr

This repository contains a version-controlled set of simple, custom instructions I developed for working with ChatGPT.

Be sure not to miss the section [Lessons and (Fun?) (Scary?) Surprises](#lessons-and-fun-scary-surprises).

## Repository Contents

- `README.md` the document you're reading now
- `custom-instructions.txt` aptly named

## Setup

- Download the file and place it in the correct location. See the [section below](#where-the-instructions-can-be-placed) this for details.
- custom-instructions.txt has a section for variables/constants where a user must set his/her specifics. I use them like this.

```
## Variables/Constants
TIMEZONE = Eastern or PST or Wherever
LOCATION = City, State or Wherever
```

## Where the instructions can be placed

As of October 2nd, 2026, these settings are found in this location along with details about using an AGENTS.md file:

`ChatGPT/Codex App -> Settings -> Personalization -> Custom Instructions`

At that location, the following text can be found:

`"Codex instructions - Edit the AGENTS.md file on the selected machine. Repository instructions may also apply.` [Learn more](https://learn.chatgpt.com/docs/agent-configuration/agents-md#create-global-guidance)"

## Background

The project began with a simple problem: I found myself repeatedly asking for the same kinds of information in the same format. Rather than continue restating those requirements in every conversation, I formalized them into reusable functions and routines. The result is a small instruction system that defines specific behaviors, output formats, and reusable routines that can be invoked consistently across conversations.

## Approach

The instructions are organized around small reusable functions that can be combined into larger routines.

For example, an individual function may define how a timestamp should be returned, while a routine may specify several functions that should execute together and in a particular order.

A simplified structure looks like this:
- Each function defines a narrow responsibility and an expected output format
- Routines compose those functions into repeatable workflows

```text
Functions
├── Timestamp()
├── Weather()
└── ChatDuration()

Routines
├── Intro Routine (comprises Functions)
└── Outro Routine (comprises Functions)
```

## Design Goals

- **Consistency**: Repeated requests should produce predictable output.

- **Reusability**: Common behaviors should be defined once and reused.

- **Composability**: Small functions can be combined into larger routines.

- **Explicit behavior**: Instructions can say when a routine should run and what it should do.

- **Version control**: Changes should be reviewable and reversible.

## Why This Repository Exists and Why Git/GitHub

Custom instructions are easy to edit, but they are also easy to lose track of as they evolve. I wanted a better way to:

- preserve previous versions
- review changes before adopting them
- document why changes were made
- experiment without losing a known-good version
- treat configuration as something worth maintaining deliberately
- open it up to collaboration with others

Git and GitHub were a natural fit. Instead of treating the instructions as disposable text in an application settings page, I began treating them more like configuration or source code.

This project is deliberately small, but it demonstrates something I value in larger engineering work as well: tools should conform to a useful workflow rather than remain informal just because the underlying artifact is small or simple.

Also, as we begin to work more and more with AI agents, I see it as very likely that we will want certain actions taken by AI agents on our behalf, even mundane ones, to be explicitly configured to our liking. I envision this will include explicitness in:
- convenient ways to trigger the action
- the format in which we want to receive the output
- sources used in the action
- security/control (i.e. don't do this even if you hit a blockage. report to me instead)

## Lessons and (Fun?) (Scary?) Surprises

1. One of the lessons from this project is that even lightweight configuration benefits from structure once it begins to evolve.

2. One of the BIG surprises from this project is that a small, (hopefully) harmless form of the [Paperclip Maximizer](https://en.wikipedia.org/wiki/Instrumental_convergence#Paperclip_maximizer) reared its head. Continue reading the [I Am Become Paperclip](#i-am-become-paperclip) section for Details.

## I Am Become Paperclip
During one chat, I had forgotten to ask for the Intro Routine at the beginning of the session. At the end of the chat, I called for the Outro Routine, which gets a fresh timestamp and calculates the chat duration. It worked as intended and gave the correct chat duration.

But then I realized that the Outro Routine explicitly makes use of the timestamp given in the Intro Routine... So how could the Outro Routine work if I had never called the Intro Routine? Something didn't smell right. You can imagine Lt. Detective Columbo scratching his head and saying "Just one more thing..."

When I asked ChatGPT for an explanation, it explained that it used the metadata from the conversation start in order to achieve the goal... I had never intended this. In fact, when I had asked previously, ChatGPT had told me that it didn't have such metadata (which I found hard to believe anyway). This supposed lack of metadata information regarding time was one of the things prompting me to develop the Timestamp routine in the first place!

I find all of this surprising and alarming at the same time. Unintended consequences and perverse instantiation are things we must always keep in mind, lest we all end up [paperclips](https://en.wikipedia.org/wiki/Instrumental_convergence#Paperclip_maximizer).

