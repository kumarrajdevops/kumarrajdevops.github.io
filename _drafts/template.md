---
title: "Post Template & Kitchen Sink"
date: 2026-03-12 17:00:00 +0530
categories: [Blogging, Tutorial]
tags: [template, markdown]
description: "A comprehensive template exhibiting all supported markdown features for the Chirpy theme."
math: true
mermaid: true
# image: /assets/img/sample/mockup.png
---

## Headings

### H3 Heading
{: .mt-4 .mb-0 }

## Typography

- **Bold** and _Italics_
- [Links](https://google.com)
- Inline code: `const x = 10;`
- Filepath: `/etc/hosts`{: .filepath}

## Prompts

> This is a tip prompt.
{: .prompt-tip }

> This is an info prompt.
{: .prompt-info }

> This is a warning prompt.
{: .prompt-warning }

> This is a danger prompt.
{: .prompt-danger }

## Media

![Image Alt Text](/assets/img/posts/mockup.png){: w="700" h="400" .shadow }
_This is an image caption_

### Video Embed

{% include embed/youtube.html id='Balreaj8Yqs' %}

## Code Blocks

```python
def hello_world():
    print("Follow the Chirpy style!")
```
{: file="hello.py" }

## Math

$$
\begin{equation}
  E = mc^2
\end{equation}
$$

## Mermaid

```mermaid
graph TD
    A[Start] --> B{AI Agent?}
    B -- Yes --> C[Follow Style Guide]
    B -- No --> D[Human writes anyway]
```
