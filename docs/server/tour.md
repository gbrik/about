---
layout: markdown
title: Sourcegraph tour
permalink: docs/tour
---

Sourcegraph is a code search and intelligence tool for developers. It lets you search and explore all of your organization's code on the web, with integrations into your existing tools. See the [Sourcegraph overview](/docs/overview) for more general information.

Let's take a tour around Sourcegraph to see how it helps with common developer tasks.

---

## Code review: gain context on changed code

As a developer who is reviewing a pull request or diff, I need to understand the changed code to see whether it'll have unexpected negative impacts or if there are other necessary changes that were accidentally omitted.

Using Sourcegraph makes you a more effective code reviewer because code intelligence makes it much easier to drill down into the implementation (to verify correctness of the change) and enumerate call sites (to verify completeness of the change).

Requirements:

- [Install Sourcegraph](/docs/) and add repositories
- [Install the integration for your code host/review tool](/docs/integrations)

Workflow:

1.  Visit a pull request or code review in your web browser.
1.  Hover over source code in the diff (in added, unchanged, or deleted code) to see hover tooltips with documentation and **Go to definition** and **Find references** actions.
1.  Use these actions while reviewing the diff, such as to ensure that all call sites of a modified function are updated to account for any new assumptions or behavior.

To try this on an open-source pull request, [install the browser extension](/docs/features/browser-extension/) and visit [gorilla/websocket#342](https://github.com/gorilla/websocket/pull/342/files). Use **Find references** to see all of the cases in which the newly added `AllowClientContextTakeover` is used.

---

## Example code: learn how a particular function should be called

As a developer who's adding a new feature, I need to know how I should call a particular function.

Viewing cross-references (internal and external) on Sourcegraph is a great way to learn how to use a function or library, because it shows you how it's _actually_ being used, not just what the (possibly outdated or incomplete) documentation might suggest.

Requirements:

- [Install Sourcegraph](/docs) and add repositories
- [Install the browser extension and editor plugin](/docs/integrations) for a faster way to initiate searches (optional)

Workflow:

1.  Search on Sourcegraph for the name of the function you're trying to call. If you've installed any integrations, use those to initiate the search; otherwise use the search box on the homepage of your organization's internal Sourcegraph instance.
1.  Find and click on a search result that refers to the function you're looking for. (If needed, narrow your search using the suggested search filters below the search box, or by [adding your own filters](/docs/search/query-syntax).)
1.  Click on the name of the function in the code file (if it's not already highlighted).
1.  Click **Find references** to see how the function is called. (If the function is called by other repositories, go to the **External references** tab in the panel to see those calls, too.)
1.  Click through to various function call sites and use the after-line blame's authorship and recency information to gauge the quality of the call site as an example.

To try this on an open-source repository, start by searching for [repo:dgrijalva/jwt-go parsewithclaims](https://sourcegraph.com/search?q=repo:dgrijalva/jwt-go+parsewithclaims) and follow the steps above to view internal and external references for the [`ParseWithClaims`](https://sourcegraph.com/github.com/dgrijalva/jwt-go/-/blob/token.go#L92:6$references) function.

---

## Explore/read code: understand what a function does and how it works

As a new developer on a project, I need to understand the implementation details of a certain part of the code.

Navigating your code with code intelligence on Sourcegraph is a great way to understand code better, because it works across all of your repositories (and all versions) without additional configuration, and it lets you share links with teammates if you need to ask specific questions about pieces of code.

Requirements:

- [Install Sourcegraph](/docs) and add repositories
- [Install the browser extension and editor plugin](/docs/integrations) for a faster way to initiate searches (optional)

Workflow:

1.  Search on Sourcegraph to locate the part of the code you're interested in. If you've installed any integrations, use those to initiate the search; otherwise use the search box on the homepage of your organization's internal Sourcegraph instance.
1.  Find and click on a relevant search result or search suggestion. (If needed, narrow your search using the suggested search filters below the search box, or by [adding your own filters](/docs/search/query-syntax).)
1.  Read through the code, clicking on a token and then **Go to definition** to navigate to its definition as needed.
1.  If you have unanswered questions, use the blame information to determine who wrote the code, and send them a Sourcegraph link to the relevant code along with your specific questions.

To try this on an open-source repository, start by searching for [repo:Microsoft/node-jsonc-parser getLocation](https://sourcegraph.com/search?q=repo:Microsoft/node-jsonc-parser+getLocation) and follow the steps above to navigate to the implementation of the [`getLocation`](https://sourcegraph.com/github.com/Microsoft/node-jsonc-parser@e31983089c88114c7cc17f8c729feb493295c69d/-/blob/src/impl/parser.ts#L26:17) function. From there, keep drilling down until you get to the [`createScanner`](https://sourcegraph.com/github.com/Microsoft/node-jsonc-parser@e31983089c88114c7cc17f8c729feb493295c69d/-/blob/src/impl/scanner.ts#L13:17) function.

---

## Debug issues: see what changed related to a function call that's erroring in production

As a developer responsible for a service that's running in production, I need to respond to a crash report with a stack trace by quickly identifying and fixing the problem.

Diff search on Sourcegraph is a great starting point for your investigation into what broke, because it shows you all recent changes that match your query.

Requirements:

- [Install Sourcegraph](/docs) and add repositories
- [Install the browser extension and editor plugin](/docs/integrations) for a faster way to initiate searches (optional)

Workflow:

1.  Perform a diff search on Sourcegraph with the name of the function that the stack trace originates from, such as `type:diff myCrashingFunctionName`. If you've installed any integrations, use those to initiate the search; otherwise use the search box on the homepage of your organization's internal Sourcegraph instance.
1.  Scroll through the search results, which show you all commits (and diffs) that match the function name, newest first. (If needed, narrow the diff search by [adding search filters](/docs/search/query-syntax).)
1.  Find and click on a relevant search result. On the search results page, clicking on the commit message brings you to the diff (with code intelligence), and clicking on the code in the commit diff brings you to the full file at the revision before or after the commit.
1.  Use **Go to definition** and **Find references** to understand the implementation changes and callers

<!-- TODO(sqs): add open-source examples -->