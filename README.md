# Purpose

The purpose of these standards are so we have a common way of working. That is beneficial because it means it's easier to get started in different projects and work with new team members.

This is not meant to restrict our way of working. For instance deciding between `express` and `hapi` is pointless because they both have their strengths and weaknesses, but deciding on a code style the purpose of a code style is bringing people together on coding standards ([i.e.](https://lmgtfy.com/?q=why+coding+standards+are+important)).

Qualities of a good choice of standard are:

- Gets out of the way;
- Is flexible to support multiple scenarios;
- Is not restricting;
- Is safe, production ready, and project members have experience with it;
- Promotes good coding practices;

There are very good reasons to have a common way of doing things in YLD, justifications for not complying with these may be "we have no ownership over these choices" but not "I don't agree with them so I'm not using them".

# Javascript Code Style

## eslint with the `eslint-config-airbnb-base` preset, `eslint-config-airbnb` for React projects;

We can start a project to extend one of those bases if we find we have issues with some rules.

## Webpack and Babel

Rollup and Bublé might be tempting but we don't have any production experience with them, as soon as someone starts getting some at home experience we can start doing safer things with this on clients and then bigger things.

# Deployment

- If you have AWS, use as much managed infrastructure as you can: less ops work;

- Use `docker-machine` with the appropriate driver (e.g. [AWS EC2](https://docs.docker.com/machine/drivers/aws/), [digital ocean](https://docs.docker.com/machine/drivers/digital-ocean/), [Google GCE](https://docs.docker.com/machine/drivers/gce/), [lots of drivers](https://docs.docker.com/machine/drivers/))

It's a good common vendor abstraction.
