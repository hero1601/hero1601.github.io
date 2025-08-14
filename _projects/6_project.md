---
layout: page
title: Document-Chat
description: An AI-powered document chat application enabling conversational interaction with documents.
img: assets/img/document-chat-bg.jpg
importance: 1
category: work
---

This project is an **AI-powered document chat application** that allows users to conversationally interact with uploaded documents such as PDFs.  
Powered by **LangChain**, **LLaMA** (`llama3-70b-8192`), and **HuggingFace embeddings**, it transforms static document content into a dynamic, searchable chat experience.

The system offers **optional user login**:
- **Login mode**: Enables personalization, **persistent chat history**, and document recall when users return.  
- **Guest mode**: Lets users explore documents without storing personal data.  

It supports **multiple concurrent chat sessions**, so users can:
- Keep different documents in different chats without mixing contexts.  
- Switch between chats to query multiple sources in parallel.

Built using **Python** and **Streamlit**, this app delivers a balance of interactivity, scalability, and privacy.

[🔗 View the code on GitHub](https://github.com/hero1601/document-chat)  
[🚀 Try the Live App](https://document-chatting.streamlit.app)  

---

### Project Goals
- Enable **real-time conversational AI** over uploaded documents.  
- Integrate **LangChain** and **LLaMA** for accurate, context-aware retrieval.  
- Provide **privacy flexibility** through login or guest mode.  
- Implement **persistent chat history** for returning logged-in users.  
- Support **multiple independent chats** to organize queries by topic/document.  

---

### Features
- **Multi-document & multi-chat support** – work with different PDFs simultaneously.  
- **Persistent chat history (login mode)** – pick up conversations where you left off.  
- **Guest mode** – instant, privacy-respecting access without data retention.  
- **AI-powered Q&A** – retrieval-augmented generation with semantic search.  
- **Fast similarity search** – HuggingFace `all-MiniLM-L12-v2` embeddings + FAISS vector store.  
- **Streamlit-based interactive UI**, accessible online without install.  

![UI Screenshot](assets/img/ui-screenshot.png)

---

### Privacy & Access Modes
The app is built with **privacy-first** functionality:  
- **Login mode**: Saves chats and documents for future sessions.  
- **Guest mode**: Runs without storing any information.

<div style="text-align: center; margin-top: 1rem;">
  <video controls class="img-fluid rounded z-depth-1" width="75%">
    <source src="{{ '/assets/img/privacy_modes.mp4' | relative_url }}" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>

---

### Multiple Chat Sessions
Users can open **multiple independent chats**, each working with its own set of documents — perfect for organizing queries by topic or project.

<div style="text-align: center; margin-top: 1rem;">
  <video controls class="img-fluid rounded z-depth-1" width="75%">
    <source src="{{ '/assets/img/multi-cha.mp4' | relative_url }}" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>

---

### Chat History for Returning Users
When users log in, they can **view and resume all past conversations**, making it easier to continue research without re-uploading documents.

<div class="col-sm mt-3 mt-md-0" style="text-align: center;">
    {% include figure.liquid path="assets/img/chat-history.png" title="Output Dataset Visualization" class="img-fluid rounded z-depth-1 w-50" %}
</div>

---

### Technical Overview
- **Document Processing**  
  - PDF loading and text chunking for optimized retrieval.  
  - Semantic embeddings via HuggingFace models.  
  - Vector database storage in FAISS.

- **Conversational AI**  
  - LangChain’s `ConversationalRetrievalChain` for retrieval-augmented generation.  
  - LLaMA (`llama3-70b-8192`) for high-quality, context-grounded answers.  
  - Separate memory per chat session.  

- **Session Management**  
  - Multi-chat handling for multiple document sets.  
  - Persistent storage for logged-in users.  
  - Temporary, in-session storage for guest mode.  

<div class="col-sm mt-3 mt-md-0" style="text-align: center;">
    {% include figure.liquid path="assets/img/doc-chat-archi.png" title="Architecture" class="img-fluid rounded z-depth-1 w-50" %}
</div>

---

### Key Takeaways
- Combines **semantic search** with **generative AI** for powerful document exploration.  
- **Multiple concurrent chat sessions** keep work organized.  
- **Persistent chat history** boosts return-user productivity.  
- Privacy-respecting **guest mode** encourages adoption.  
- Fully deployed online for instant access.

---

This project is an example of how **retrieval-augmented generation** can be extended with **multi-session management** and **chat memory persistence** to create a seamless and intelligent document assistant.
