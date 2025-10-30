---
layout: post
title: "Simplicity Matters"
date: 2025-10-29 10:00:00 +0100
categories: engineering serverless
---

I'm back at PostNL (which I very much enjoy 😇), working on a greenfield PoC. PostNL runs on AWS with a heavy focus on serverless—Lambda, API Gateway, DynamoDB.
These tools are powerful, but they come with complexity. Lambda has its quirks, DynamoDB isn't exactly beginner-friendly, and the abstractions add layers you need to understand.

My own approach is different. For side projects, I stick to AWS free tier or [Dokku](https://dokku.com/)—a self-hosted PaaS that handles deployments without ceremony.
It's not revolutionary, but it works and supports everything I need. When I'm building something, I find myself reaching for boring, simpler tools.
They let me ship quickly without fighting the infrastructure.

<br>

## The Project

The assignment seemed straightforward: build a PoC with serverless components, a frontend, and some early users.
PostNL has a DevEx team that maintains [Projen](https://projen.io/), which handles project scaffolding and configuration.

We started with a Next.js app exported as static HTML. One page, no routing, just a simple interface. But requirements evolved (as they always do),
and we decided to move Next.js into a Lambda function—essentially a mini monolith where frontend and backend live together.

Initially, this worked well. Until it didn't.

We had to use a different CDK construct to deploy Next.js to Lambda. It had a bug, which we fixed and submitted a PR for. But the pipeline also slowed down significantly—builds were taking much longer than before.

Eventually, we got it working locally and deployed it to Lambda. The app ran. We were happy.

Then we integrated the auth system. That's when everything broke.

When we deployed with auth, we hit issue after issue. I'll keep it short: it took me four days to *not* get it working. I scrapped it and rebuilt the whole thing in one day using React and plain Lambda functions with API Gateway.

<br>

## What I Learned

We innovated where nobody asked us to. The Next.js-in-Lambda approach was an assumption, not a requirement. The complexity wasn't justified.

I should have pushed back harder when I saw the warning signs. I hadn't deployed Next.js this way before, and it showed. More importantly, the client didn't need it. A simpler stack would have delivered value faster.

Simplicity isn't just about speed, it's about leverage. Simpler systems are easier to understand, faster to debug, and more maintainable. Innovation needs to earn its spot. If you can't explain why the complexity is necessary, it probably isn't.

Keep it boring until boring doesn't work.

---

*This post was written with the help of AI, but the experiences and thoughts are my own.*
