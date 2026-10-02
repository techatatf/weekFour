# Week 4 Master Glossary: The Pitch & Shipping Real Apps

Welcome to the **Week 4 Master Glossary** for *The Pitch: Storytelling for Impact*! This document brings together all the core technical keywords, web development terms, pitching concepts, and mobile integration tools covered across Episodes 14 through 17.

---

## 📅 Episode Breakdown Quick-Nav
* **Episode 14**: Frontend UI & Streamlit Web Apps
* **Episode 15**: Cloud Deployment, Secrets & Git Debugging
* **Episode 16**: The PSI Pitching Framework & Soft Skills
* **Episode 17**: Mobile WhatsApp Integration, Flask Webhooks & Series Finale

---

## 🚀 Episode 14: Building the App UI (Streamlit)

> **High School Pitch:** Imagine you built a super-smart robot brain on your computer, but the only way to talk to it is by typing complex terminal commands. None of your friends can use it! Streamlit is like a magic spell that turns your Python code into a beautiful, clickable website with buttons, sliders, and chat boxes in just a few lines of code—no HTML or CSS required.

---

### 1. Streamlit
* **What it is in plain English:** A Python framework that turns data scripts and AI backends into interactive web applications automatically.
* **High School Analogy:** Think of Streamlit like a web app construction kit. Instead of building a house brick-by-brick with HTML and CSS, you just say "add a slider here and a chat box there," and Streamlit instantly builds the webpage for you.
* **Spotting it in the Video Script:** The tutor opens Google Colab on camera and asks, *"How many of your friends could use this?"* Answer: *"Zero."* Then, with just two lines of code (`import streamlit as st` and `st.title()`), a browser page opens up at `localhost:8501`.

---

### 2. Streamlit Rendering Model (Top-to-Bottom Rerun)
* **What it is in plain English:** The unique way Streamlit runs your code: every single time a user touches any control on the page (clicks a button, moves a slider, or types a word), Streamlit re-executes the *entire* Python script from line 1 all the way to the bottom.
* **High School Analogy:** Imagine reading a comic book from page 1 every time you turn on a light switch in your room. It makes building apps super simple because you don't have to write complex event-listeners, but it means your script forgets everything unless you save it in a special "backpack" (Session State).
* **Spotting it in the Video Script:** On-screen text card: `[Every interaction = full script rerun]`. The tutor warns that because of this rerun behavior, Python apps are *stateless* by default.

---

### 3. Session State (`st.session_state`)
* **What it is in plain English:** Streamlit's built-in memory bank (a Python dictionary) that persists data across script reruns.
* **High School Analogy:** Imagine taking a test where the teacher wipes your desk clean every 30 seconds. Session State is like a secret notebook under your desk where you write down your past answers so you don't lose them when the desk gets wiped.
* **Spotting it in the Video Script:** In Part 2, the tutor shows that without `if "messages" not in st.session_state: st.session_state.messages = []`, typing a second message in the chat causes the first message to disappear forever! With Session State, past chat messages persist even when you adjust a sidebar slider.

---

### 4. Core Widgets (`st.text_input`, `st.button`, `st.slider`, `st.selectbox`, `st.file_uploader`, `st.chat_input`)
* **What it is in plain English:** Interactive visual controls that allow users to send data or commands to your app.
* **High School Analogy:** Widgets are like the dashboard controls in a car—steering wheels, buttons, and dials that let you control the engine without touching the raw machinery under the hood.
* **Spotting it in the Video Script:** During the "Widget Tour", the tutor adds five core controls:
  1. `st.text_input` — for typing queries.
  2. `st.button` — for submitting actions.
  3. `st.slider` — placed in the sidebar to adjust AI "temperature" (creativity).
  4. `st.selectbox` — for picking between models (e.g., Claude Haiku vs. Sonnet).
  5. `st.file_uploader` — for dragging and dropping diary files (`.txt` or `.json`).

---

### 5. Layout Tools (`st.sidebar`, `st.columns`)
* **What it is in plain English:** Commands used to arrange elements visually on the screen rather than stacking everything in a single vertical column.
* **High School Analogy:** Like organizing your bedroom with shelves and room dividers instead of throwing all your clothes into one big pile in the middle of the floor.
* **Spotting it in the Video Script:** 
  * `st.sidebar`: Holds configuration settings (sliders, buttons) so they stay neatly pinned on the left side of the screen while chatting.
  * `st.columns([2, 1])`: Creates a side-by-side split view—2 units of screen width for the main chat window, and 1 unit on the right for displaying retrieved grounding diary sources.

---

### 6. `st.rerun()`
* **What it is in plain English:** A command that tells Streamlit: *"Stop what you're doing right now and restart the script execution from line 1 immediately!"*
* **High School Analogy:** Hitting the "Reset" button on a video game console to refresh the game state instantly.
* **Spotting it in the Video Script:** In Exercise 2, when creating a "Clear History" button, you set `st.session_state.messages = []` and then call `st.rerun()`. Without `st.rerun()`, the old chat messages would remain stuck on the user's screen until they typed another message!


---

## ☁️ Episode 15: Deployment (Hosting Your App)

> **High School Pitch:** You built an awesome web app on your laptop, but right now it's stuck at `http://localhost:8501`—meaning nobody in the world can see it unless they're physically sitting in your chair. Deploying is like uploading your app to the cloud so anyone on Earth can open it on their phone with a simple shareable link!

---

### 1. Localhost (`localhost:8501`) vs. Publicly Hosted App
* **What it is in plain English:** Localhost is your private, local computer sandbox. A Publicly Hosted App is hosted on cloud servers with a real web address (`https://...`).
* **High School Analogy:** Localhost is like playing a single-player video game saved on your local hard drive. Hosting it online is like launching a multiplayer server where all your friends can join in.
* **Spotting it in the Video Script:** The tutor points at `http://localhost:8501` in the terminal and states: *"This works. It is also useless to anyone who isn't sitting at this laptop."* Episode 15 takes that local app and gives it a public URL.

---

### 2. Pre-Flight Deployment Checklist (`requirements.txt`, `.env`, `.gitignore`)
* **What it is in plain English:** The three foundational configuration files required before publishing any project to the internet.
* **High School Analogy:** Packing your backpack before a field trip:
  * `requirements.txt` = The packing list (tells the cloud computer what software packages to install).
  * `.env` = Your VIP pass / secret diary (stores secret API keys safely on your private computer).
  * `.gitignore` = The security guard (ensures your private `.env` diary never gets packed or exposed online).
* **Spotting it in the Video Script:** On-screen text card: `[Three files before any deploy]`. The tutor highlights that leaking API keys by forgetting `.gitignore` is the single most common public deployment mistake!

---

### 3. Repository Secrets / Secrets Management
* **What it is in plain English:** A secure settings vault provided by cloud hosts to store confidential keys and passwords without hardcoding them into public software scripts.
* **High School Analogy:** Storing your house key inside a combination lockbox on the front porch instead of taping the key directly to the front door.
* **Spotting it in the Video Script:** In Hugging Face Spaces (`Settings > Repository secrets`) and Streamlit Community Cloud (`Advanced settings > Secrets`), students paste `ANTHROPIC_API_KEY = "sk-..."`. This lets the deployed app access Claude while keeping the public code completely free of sensitive secrets.

---

### 4. Deployment Hosts: Hugging Face Spaces vs. Streamlit Community Cloud
* **What it is in plain English:** Two cloud platforms that host Streamlit apps for free.
* **High School Analogy:** 
  * **Hugging Face Spaces**: Like building custom furniture from scratch with Git commands—gives you total control, but takes a little manual assembly.
  * **Streamlit Community Cloud**: Like ordering pre-assembled furniture linked to your GitHub account—every time you push new code (`git push`), it automatically updates the live website with zero extra steps.
* **Spotting it in the Video Script:** The tutor deploys the exact same Ep14 app to both platforms, demonstrating that there is no single "correct" host—only trade-offs between manual control (Spaces) and automated ease (Streamlit Cloud).

---

### 5. Deployment Logs & Debugging (Build vs. Run Errors)
* **What it is in plain English:** The live text output generated by cloud servers showing step-by-step how your app is being assembled and executed.
* **High School Analogy:** Like reading the diagnostic report from a car mechanic when your engine won't start—it tells you whether you ran out of gas (Build error) or popped a tire while driving (Run error).
* **Spotting it in the Video Script:**
  * **Build Failure**: Fails early while installing packages (e.g. misspelling a package in `requirements.txt`).
  * **Run Failure**: Fails after launch when running code. The tutor deliberately pushes a typo (`st.titel()`) live on camera! The log displays `AttributeError: module 'streamlit' has no attribute 'titel'`, showing students exactly where the typo occurred.

---

### 6. Git Rollback (`git revert HEAD`)
* **What it is in plain English:** A Git command that instantly undoes your most recent code commit and restores the previous working state of your website.
* **High School Analogy:** Using "CTRL+Z" (Undo) for an entire published website when a new update breaks the live app.
* **Spotting it in the Video Script:** The tutor explains two ways to respond to a broken deployment: "fix forward" (fix the typo and push again) or "roll back" (`git revert HEAD && git push`). Rollback is your emergency safety net when you need the website working again immediately!


---

## 🎤 Episode 16: The Pitch (Storytelling for Impact)

> **High School Pitch:** You spent weeks writing complex code and building an AI app—now you have 90 seconds to convince a room full of people why it matters! Pitching isn't about bragging with big words; it's about telling a simple, human story that makes anyone instantly understand the problem you solved.

---

### 1. The PSI Framework (Problem, Solution, Impact)
* **What it is in plain English:** A battle-tested 3-part structure for delivering a clear, persuasive 90-second presentation.
  * **Problem (15s)**: A pain point stated in 1 clear sentence that the audience already feels.
  * **Solution (20s)**: What you built, explained in 1 plain-language sentence without technical jargon.
  * **Impact (55s)**: A live demo and concrete proof showing the real-world value.
* **High School Analogy:** Like a movie trailer: it hook you with the struggle, introduces the hero, and shows an epic 10-second action scene that makes you want to buy a ticket immediately.
* **Spotting it in the Video Script:** The tutor contrasts two pitches on camera:
  * *Bad Pitch*: *"We leveraged a state-of-the-art retrieval-augmented generation pipeline with vector embeddings..."* (Boring, confusing jargon).
  * *PSI Pitch*: *"I built an app that reads your old diary entries and answers questions about your own life in seconds."* (Clear, relatable, powerful).

---

### 2. Format C (Presenter-to-Camera)
* **What it is in plain English:** A direct video filming format where the presenter speaks directly into the camera lens with no slides, split screens, code overlays, or animated distractions.
* **High School Analogy:** Talking face-to-face with a friend in a quiet room instead of trying to shout over a loud video game screen.
* **Spotting it in the Video Script:** Ep16 is the series' first pure Format C production. The tutor uses eye contact, calm timing, and clear voice delivery to prove that human connection and trust matter just as much as technical skills.

---

### 3. The 12-Year-Old Test
* **What it is in plain English:** A rule of thumb for simplifying technical descriptions—if a smart 12-year-old student cannot understand your solution statement, it contains too much jargon and needs further simplification.
* **High School Analogy:** Explaining how a car works by saying "it takes you places fast" instead of "it uses an internal combustion engine with four-stroke fuel injection cycles."
* **Spotting it in the Video Script:** In Scene 2, the tutor states: *"Solution. One sentence, plain language, no acronyms... If a smart twelve-year-old wouldn't follow it, simplify it more."*

---

### 4. Specificity & The Single Proof Point
* **What it is in plain English:** Using one real, undeniable moment or live working demo rather than making generic claims or listing dozens of confusing stats.
* **High School Analogy:** Proving you can throw a basketball full-court by sinking a shot live in front of the crowd, rather than boasting about your practice stats.
* **Spotting it in the Video Script:** During the live 90-second pitch, the tutor opens the app on a phone and asks: *"What did I eat the week I started this job?"* The live app answers instantly. One concrete moment makes the claim believable!

---

### 5. Three Common Pitch Mistakes
* **What it is in plain English:** The three trapdoors that ruin technical presentations:
  1. **Leading with Technology**: Talking about RAG pipelines, APIs, and safety layers instead of what the user gets.
  2. **Vague Problem Statements**: Saying "people suffer from information overload" instead of a tangible struggle like "I can never find notes from last month."
  3. **No Proof**: Making big claims without showing a live working demo or concrete example.
* **High School Analogy:**
  1. Bragging about the recipe ingredients instead of serving the delicious cake.
  2. Complaining that "life is hard" instead of fixing a broken shoe lace.
  3. Claiming you can play guitar without actually playing a song.
* **Spotting it in the Video Script:** In Scene 3, the tutor counts these three mistakes on their fingers directly to camera, showing how to avoid each one.


---

## 📱 Episode 17: Mobile Integration & Series Close

> **High School Pitch:** A fancy web app looks great on a laptop, but millions of people around the world don't own laptops—they use messaging apps on their phones! By connecting your AI backend to WhatsApp, you take your project out of the lab and put it directly into the hands of real users anywhere in the world.

---

### 1. Full System Architecture
* **What it is in plain English:** The complete end-to-end pathway that connects a real user to your AI engine across different platforms.
* **High School Analogy:** The postal system: Message written by user -> dropped in mailbox (WhatsApp) -> sorted by regional post office (Twilio) -> delivered to your house (Flask Webhook) -> processed by your brain (SafeLLM / Claude AI) -> reply mailed back!
* **Spotting it in the Video Script:** In 17A, the tutor presents a static system architecture diagram recapping all 17 episodes:
  `User on WhatsApp -> Twilio Sandbox -> Flask Webhook -> SafeLLM Guardrails -> Anthropic API -> Response returned to WhatsApp`.

---

### 2. Twilio WhatsApp Sandbox
* **What it is in plain English:** A developer tool that lets you send and receive WhatsApp messages programmatically using Python code without needing a formal Meta Business registration.
* **High School Analogy:** A free trial pass at a gym that lets you test out all the equipment before paying for a full membership.
* **Spotting it in the Video Script:** In 17B, the tutor opens the Twilio console, gets a sandbox phone number (`+1 415 523 8886`), texts a keyword (`join <keyword>`) from their phone, and instantly links their phone to the development server.

---

### 3. Flask Webhook (`@app.route("/webhook")`)
* **What it is in plain English:** A lightweight Python web server endpoint that sits waiting to receive HTTP messages sent by outside services (like Twilio).
* **High School Analogy:** A digital doorbell for your server. When a user sends a text on WhatsApp, Twilio "rings the doorbell" (sends an HTTP POST request to `/webhook`), and Flask automatically answers and processes the message.
* **Spotting it in the Video Script:** The tutor writes the webhook route in `webhook.py`. When an incoming message arrives, Flask extracts the text, runs it through `format_for_mobile()`, calls `SafeLLM.call()`, and returns XML instructions to Twilio.

---

### 4. `ngrok` Tunneling
* **What it is in plain English:** A tool that creates a secure, public HTTPS web link pointing directly to a server running locally on your laptop.
* **High School Analogy:** Opening a temporary tunnel through a castle wall so a delivery driver outside can hand a package directly to you inside your room.
* **Spotting it in the Video Script:** In 17B, Flask runs locally on port 5000 (`http://localhost:5000`). Running `ngrok http 5000` generates a public link like `https://abc123.ngrok.io`. The tutor pastes this link into Twilio's Sandbox Settings so Twilio knows where to send incoming WhatsApp messages.

---

### 5. Mobile-First Design Rules (`format_for_mobile()`)
* **What it is in plain English:** Rules for formatting text outputs so they look clean, readable, and respectful on phone screens.
  * **Rule 1 (No Markdown)**: Strip asterisks (`*`) and headers (`#`) because WhatsApp doesn't render standard markdown cleanly.
  * **Rule 2 (1,000 Character Limit)**: Truncate long responses so users aren't overwhelmed by massive walls of text on small mobile displays.
  * **Rule 3 (Plain Text & Structure)**: Use clear, simple numbered sentences rather than bullet points with dashes.
  * **Rule 4 (Media Handling)**: Detect voice notes or images (`NumMedia > 0`) and gently remind the user to send text.
* **High School Analogy:** Writing a quick text message to a friend instead of mailing them a 10-page printed essay.
* **Spotting it in the Video Script:** The tutor writes `format_for_mobile()` in 11 lines of Python, using Regular Expressions (`re.sub`) to strip markdown symbols before sending the AI response to WhatsApp.

---

### 6. Accessibility & Persona Reach
* **What it is in plain English:** Designing AI technology so it can be accessed by diverse communities who may lack high-speed internet, computers, or technical knowledge.
* **High School Analogy:** Building a ramp at the entrance of a building so everyone can enter, regardless of whether they walk or use a wheelchair.
* **Spotting it in the Video Script:** In 17C, the tutor highlights three key real-world personas reached through WhatsApp mobile integration:
  1. **Student**: A first-generation college student needing midnight AI homework help from a feature phone.
  2. **Health Worker**: A rural clinic nurse looking up medical protocols during a home visit.
  3. **Farmer**: A smallholder farmer checking crop market prices without needing an expensive data plan.

