Customer Support Router Dashboard 🚀

Internship Assessment Submission | Single-page AI-powered customer triage & routing console designed for maximum resilience, accessibility, and speed.

An interactive client-side workspace that processes customer complaints, dynamically injects category-specific instructions, routes issues into three triage domains (Refund Request, Technical Issue, General Inquiry), and outputs structured analysis using the OpenAI ChatGPT API (gpt-4o-mini).

🛠️ Tech Stack & Architecture

Frontend UI: Semantic HTML5, CSS3, and dynamic Tailwind CSS (delivered via CDN).

Icons: Lucide Icons (scalable SVGs via CDN).

Engine Logic: Vanilla JavaScript (ES6+), stateless execution, single-file architecture.

AI Orchestration: OpenAI API Platform (gpt-4o-mini via client-side REST fetches).

🎯 Why ChatGPT (gpt-4o-mini)?

During the evaluation phase (detailed in the accompanying Engineering_Log_Final_DOC.md), the application migrated away from Google Gemini and Anthropic Claude due to key-format conflicts and CORS restrictions. The shift to OpenAI introduces key architectural advantages:

Server-Enforced JSON Mode: By declaring response_format: { type: "json_object" } in the API payload, we eliminate the need for brittle client-side regex string parsing. The server guarantees clean JSON matching our exact keys: severity, reply, and summary.

Standardized Bearer Authentication: OpenAI uses standard Authorization: Bearer sk-... headers. This removes the account-level credential issues and URL parameter query leaks encountered with Gemini.

No Dynamic CORS Overrides: Unlike Anthropic Claude, which mandates dangerous origin-bypass flags (such as anthropic-dangerous-direct-browser-access), OpenAI natively supports clean, client-side fetches directly from web browsers in test sandboxes.

✨ Key Features & Defensive Engineering

Zero-Dependency Portability: Compiled entirely within a single file (index.html). No Node modules, bundlers, or heavy frameworks required. Just open and run.

Fault-Tolerant Mock Fallback: If the API times out, rate limits (HTTP 429), or encounters invalid credentials, a unified exception handler intercepts the failure and immediately loads category-specific mock datasets. The dashboard never freezes, crashes, or displays raw errors.

Strict XSS Protection: To prevent Cross-Site Scripting (XSS) payload injections from customer complaints or LLM responses, all dynamic text contents are mapped strictly using textContent rather than innerHTML.

Request Lifeline Guard: Network connections are wrapped using a browser-native AbortController set to abort transactions strictly at 30 seconds if the API stalls.

Dynamic Prompt Injection: Seamlessly updates the underlying system instructions passed to the API depending on the active triage domain dropdown, tailoring the response tone, context, and severity levels.

Accessible Markup: Structured with clear ARIA landmarks, logical keyboard tab indexing, visual focus rings, and a dynamic aria-live alert banner to accommodate assistive screen-reading technologies.

🏁 Quick Start

As a zero-dependency, client-only single-page application (SPA), getting started is instant:

Option A: Local Browser Launch

Clone this repository to your local machine:

git clone https://github.com/CODEalvii/customer-supportRouter-dashboard


Double-click index.html to open it in any modern web browser.

Option B: Local Server (Recommended for Lucide SVGs)

Launch the directory inside VS Code.

Click Go Live via the Live Server extension (http://127.0.0.1:5500).



Form Submission: The user fills out the complaint, chooses a triage category, and clicks Analyze & Route.

Local Input Verification:

If the complaint field is blank, form processing stops immediately, the textarea is auto-focused, and a warning is declared.

If the API Key field is blank, the app immediately switches to Mock Sandbox Mode and renders mock templates.

If a key is entered, it must pass the format check (starting with sk-) before a network transaction is generated.

Active REST Query: Constructs payload wrapping category rules and complaint texts into a POST request toward api.openai.com, bound by an AbortController watchdog timer.

Display & State Recovery: Parses responses cleanly, triggers CSS pulse-in animations to highlight cards, updates dynamic success/warning banners, and releases form-submission lockdowns.

📝 Engineering Logs

A detailed log of the development process is included in this repository as Engineering_Log_Final_DOC.md. The document lists:

An analysis of other API providers (Gemini, Claude, OpenAI).

A record of 4 production bugs encountered during development, along with their root causes and manual code resolutions.

Comprehensive results for 10 robust brute-force test cases, covering prompt injection attacks, blank submissions, and multi-byte character strings.

An evaluation of AI collaboration versus manual software engineering.

🛡️ License

This project was built strictly as part of an Internship Assessment Challenge over a 72-hour period. It represents independent logic implementation, architectural planning, and defensive engineering practices.
