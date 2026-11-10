# Research Agent

A command-line AI agent that researches a topic for you. It pulls background
from Wikipedia, finds relevant academic papers through OpenAlex, and explains
what it found in a clear, readable way. It keeps the full conversation in
memory, so you can ask follow-up questions in the same chat.

**Status:** scoping complete, build in progress.

## Goal
Given a topic, the agent gets background from Wikipedia, finds relevant papers
on OpenAlex, and presents a readable answer with links, remembering earlier
turns in the same chat.

## Who it's for
Students and curious readers who want a quick, sourced overview of a topic
before going deeper.

## Tools
- `get_wikipedia_summary(topic)` returns the page title, a short summary and a link
- `search_papers(query, max_results, sort_by)` returns title, year, citation count
  and link for each paper, ranked by relevance (default) or re-sorted by citations
- `get_paper_details(work_id)` returns the details for one paper found earlier

## Tech
- Python
- Gemini API (`google-genai`): chat sessions and automatic function calling
- Wikipedia REST API
- OpenAlex API

## Example conversation (target behavior)
```
You: Tell me about diffusion models.
Agent: Short background from Wikipedia, then 3 relevant papers, each with year,
       citation count, link and a one-line note on why it matters.
You: Which of those is the most cited?
Agent: Answers from the earlier results without repeating the topic or
       searching again.
```
This will be replaced with a real run once the agent works.

## Out of scope (for now)
- Web UI or any front end (command line only)
- General web search
- Reading PDFs or full paper text
- Saving research between runs (vector store / long-term memory)
- Multi-agent setups
- Async requests (tools are called one at a time, so plain `requests` is enough)

## Done when
- A topic question triggers at least one Wikipedia call and one OpenAlex call
- Every paper mentioned comes from API results, with title, year and a working
  link, and none are invented
- A follow-up question about an earlier result is answered correctly in the
  same chat
- If a page isn't found or an API call fails, the agent says so instead of
  guessing
- It runs from a fresh clone by following the setup steps in this README