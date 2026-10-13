# Week 2 Lab Worksheet
Name: murat mustafa karateke
Program: Software Engineering / Computer Programming
Level I aimed for today: Core

## Before you run the lie
What do you expect `live done` to print, and why?
I expect it to print `undefined` because the JSON object returned by the API uses the property `completed` instead of `done`. Accessing a non-existent property on a JavaScript object returns `undefined`.

## After you run the lie
lecture example, title: undefined
live title: delectus aut autem
live done: undefined
Why did TypeScript allow this?
TypeScript allowed this because we used "Type Assertion" (`as Task`), which explicitly tells the compiler to skip type checking and trust that the data matches the declared type, even if it does not at runtime.

## typecheck
Paste the error from `src/honest.ts` before you comment the line out.
Type 'unknown' is not assignable to type 'CreateTask'.

## Activity 1
What printed for todo 99999?
Fetch failed with status: 404 (and then it returned null).

What printed for the dead address (the network error)?
Network error: TypeError: fetch failed (or similar network error message).

Which of those two did `fetch` throw for?
`fetch` only threw an exception for the dead address (the network error). For the 404 response (todo 99999), it did not throw an error; instead, `response.ok` evaluated to false.

## Activity 3 — Outside feed
Paste the form boundary output (saved / refused lines).
saved: { title: 'Design database schema', status: 'doing', projectId: 1, dueDate: '2026-10-20' }
refused: Title cannot be empty
refused: Invalid enum value. Expected 'open' | 'doing' | 'done', received 'finished'
refused: Expected number, received string
refused: Required

Paste the outside-feed output.
— outside feed —
starting fetch...
got data
imported: { ok: true, task: { title: 'delectus aut autem', status: 'open', projectId: 1 } }
starting fetch...
Fetch failed with status: 404
missing todo: null

In one sentence: why was the raw to-do refused by `createTask` even though it has a title?
The raw to-do was refused because it lacks the `status` and `projectId` properties, which are explicitly required by the `CreateTaskSchema`.

## Exit question
Where is the boundary in this program, and what do you trust after the data has crossed it?
The boundary is the validation step where we use `zod.safeParse()` to check unknown incoming data against our schemas. Once the data successfully crosses this boundary, we fully trust its shape, properties, and data types throughout the rest of our application.