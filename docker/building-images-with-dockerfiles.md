---
title: Building Images using Dockerfiles(Under Construction)
description: Details on how to create Docker Images using Dockerfiles
published: true
date: 2022-09-02T12:20:05.954Z
tags: how-to, docker, dockerfile
editor: markdown
dateCreated: 2022-09-02T12:20:05.954Z
---

# Dockerfiles

> The Dockerfile is a text-based build instruction file that enables us to define the content of the Docker image and automate image creation.
{.is-info}

# Format

The format for a Dockerfile is as follows:

`INSTRUCTION arguments`

# Instruction 

<br>

## FROM

- Must be the first instruction of any Dockerfile.
- Sets the base image to be created
- By default, the latest tag will be used unless a specific tag is specified
- There can be more than one FROM instruction in one Dockerfile to create multiple images

**SYNTAX**

`FROM <image>` or `FROM <images>:<tag>`

If you want to use a private image not on the Docker Hub, the syntax should be:

`[registry_hostname[:port]/][user_name/](repository_name:version_tag)`

<br>

---

<br>

## RUN

The run instruction runs a command and generates a new layer of the image which is automatically committed to the end result. Run can be used in two ways:

`RUN <command>` - Shell form
`RUN ["executable", "param1",....,"paramN" ]` - Exec form