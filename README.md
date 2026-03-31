# Applied-AI-Builder-DDR-Report-Generation-
AI-powered DDR generator I built. DDR stands for Detailed Diagnostic Report. The idea is simple: a property inspector or surveyor uploads their raw documents
Link - https://diagnostic-report-generator--amit-sanjaysanj.replit.app/reports


Loom Video Script (3–5 minutes)
Use this word-for-word or adapt it. Timestamps are a guide.

[0:00 – 0:30] — Introduction

"Hi — I'm going to walk you through an AI-powered DDR generator I built. DDR stands for Detailed Diagnostic Report. The idea is simple: a property inspector or surveyor uploads their raw documents — an inspection report, a thermal survey, any images — and the system reads all of them together and automatically produces a structured, client-ready report. No copy-pasting, no manual merging."

[0:30 – 1:30] — What it does (live demo)

"Here's the dashboard. I can see all previous reports, search through them, and click in to read any one. Let me create a new one."

Click 'New Diagnostic'

"I give the report a title — say, a property address. Then I add my data sources. Each source has a filename, the document text I paste in, and an image upload area for inspection photos or thermal images. I can add multiple documents — for example, one for the visual inspection report and one for the thermal survey."

Show the image drop zone

"Images are attached per document — so the AI knows which images came from which source. Once everything is in, I hit 'Initiate Diagnostic'."

Start the stream

"The report streams in real-time, section by section. You can watch it build."

[1:30 – 2:30] — How it works (architecture)

"Under the hood there are two services. The frontend is React with a dark professional UI. The backend is a Node/Express API with a PostgreSQL database using Drizzle ORM."

"When you submit, the backend stores your documents and images in the database, then sends everything to OpenAI's vision model — GPT-5.2. The images go as high-resolution vision inputs, not just thumbnails."

"The system prompt is where the real work happens. I built a two-stage prompt: first, the AI does a silent pre-analysis — it builds a topic map across all documents, identifies what each source says about each area, and flags agreements, conflicts, and gaps. Then it writes the seven-section report based only on that internal analysis."

"The seven sections are: Issue Summary, Area-wise Observations, Root Cause, Severity Assessment, Recommended Actions, Additional Notes, and Missing or Unclear Information. That last section is important — it forces the AI to explicitly flag anything that was absent or contradictory, rather than quietly filling in the blanks."

"Images are stored as base64 in the database and served through a dedicated endpoint. In the report, the AI embeds images inline under the exact observation they support."

[2:30 – 3:30] — Limitations

"A few honest limitations worth knowing about."

"First — document input is text-only right now. You paste in the document content rather than uploading a PDF directly. A production version would add PDF parsing so users can upload files as-is."

"Second — the AI is only as accurate as the documents provided. If an inspection report is vague or poorly written, the output will reflect that. The prompt instructs the model never to invent facts and to mark gaps as 'Not Available', but the quality ceiling is set by the source material."

"Third — there's no user authentication yet. All reports are visible to anyone with access to the app. Adding Replit Auth would be a quick fix for a real deployment."

"Fourth — for very large document sets, the context window could become a constraint. Currently there's no chunking or summarisation strategy for documents that exceed the model's context limit."

[3:30 – 4:30] — How I would improve it

"Four improvements I'd prioritise:"

"One — PDF and DOCX upload. Parse the files server-side so users don't have to copy and paste text."

"Two — Per-report access control. Add authentication and let users share reports via a secure link."

"Three — Export to PDF. The final report renders in markdown — generating a clean, branded PDF export for the client would be straightforward with a library like Puppeteer or a React-to-PDF approach."

"Four — Confidence scoring. For each finding, the AI could output a confidence level based on how many sources corroborate it. A finding confirmed by both a visual inspection and a thermal scan should carry more weight than one mentioned in a single document. Surfacing that to the user adds transparency."

[4:30 – 5:00] — Close

"The core design goal was reliability over UI polish — accurate extraction, honest handling of gaps and conflicts, and a report format that a client can actually read. Hit me up with any questions."

