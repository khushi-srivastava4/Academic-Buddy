# Academic-Buddy
Academic Buddy — AI-Powered Learning Assistant
Problem Statement

Students often have hundreds of pages of lecture notes and previous-year question papers (PYQs), but finding relevant information, identifying important topics, and preparing efficiently for exams is difficult.

To solve this, I built Academic Buddy, an AI-powered academic assistant that transforms course materials into an interactive learning system capable of answering questions, generating quizzes, analyzing PYQs, and creating personalized revision plans.

System Architecture

The project follows a full-stack AI architecture consisting of:

Frontend
React.js
Context API for global state management
Axios for API communication
React Router for navigation
Backend
FastAPI
REST APIs
Pydantic validation
Async request handling
Storage Layer
ChromaDB (Vector Database)
SQLite (Structured Analytics Database)
AI Layer
Gemini API
Groq API (Fallback)
Retrieval-Augmented Generation (RAG)
Feature 1: Lecture Notes Chat (RAG System)

This is the core feature.

Workflow
Step 1: Upload Lecture Notes

Students upload PDFs/PPTs.

The system:

PDF
 ↓
Text Extraction
 ↓
Chunking
 ↓
Embedding Generation
 ↓
ChromaDB Storage
Step 2: Chunking

Instead of sending an entire 100-page PDF to the LLM:

Documents are divided into chunks
Chunk size ≈ 1500 characters
Overlap ≈ 200 characters

This preserves context while improving retrieval accuracy.

Step 3: Embedding Generation

Each chunk is converted into a dense vector representation using embedding models.

Example:

"Fick's First Law"
↓
[0.12, -0.45, 0.89, ...]

These embeddings capture semantic meaning rather than keywords.

Step 4: Vector Storage

Embeddings are stored in ChromaDB.

Each chunk stores:

Text
Page Number
Source File
Chunk Index
Embedding Vector
Step 5: Question Answering

When a user asks:

"What is Fick's First Law?"

The system:

Query
 ↓
Embedding
 ↓
Similarity Search
 ↓
Top-K Chunks Retrieved
 ↓
Prompt Construction
 ↓
Gemini/Groq
 ↓
Answer
Step 6: Citation-Based Response

The generated answer includes:

Source File
Page Number

This improves trust and reduces hallucinations.

Feature 2: Quiz Generation

Students can generate quizzes from uploaded material.

Pipeline
Topic
 ↓
Retrieve Relevant Chunks
 ↓
Prompt LLM
 ↓
Generate Questions

Supports:

MCQ
Short Answer
Numerical Questions

Difficulty Levels:

Easy
Medium
Hard

Users can generate multiple questions per topic.

Feature 3: Answer Evaluation

Implemented an LLM-as-a-Judge architecture.

Process

Input:

Question
Model Answer
Student Answer
Marks

The LLM:

Compares concepts
Checks correctness
Awards marks
Generates feedback

Output:

{
 "score":4,
 "feedback":"Good explanation but missing assumptions."
}
Feature 4: PYQ Intelligence Engine

One of the most unique parts.

Upload PYQ Papers

Students upload:

Midsem Papers
Endsem Papers
Quiz Papers
Question Extraction

The LLM extracts structured information:

Topic
Subtopic
Marks
Difficulty
Question Type
Year

Example:

Question:
Explain Fick's First Law. [5]

Stored As:

Topic: Diffusion
Marks: 5
Type: Theory
Difficulty: Easy
Year: 2022
Storage

Stored in SQLite.

Over time, this creates a structured exam database.

Analytics Generated

The system computes:

Topic Frequency
Diffusion → 15 times
Phase Diagram → 12 times
Heat Treatment → 9 times
Marks Distribution
Average Marks per Topic
Exam Trends
Frequently Repeated Topics
High Weightage Areas
Emerging Topics
Feature 5: Personalized Revision Planner

Uses:

Uploaded Notes
PYQ Statistics
Days Left for Exam

to generate:

Priority Topics
High Weightage
High Frequency
Weak Areas
Daily Study Plan

Example:

Day 1 → Diffusion
Day 2 → Phase Diagram
Day 3 → Heat Treatment
Feature 6: User Analytics

Tracks:

Quiz History
Scores
Topics Attempted
Accuracy
Chat History
Questions Asked
Topics Covered
Recommendations

Uses performance history to suggest:

Topics to Revise
Weak Areas
Engineering Challenges Solved
1. Hallucination Reduction

Used:

RAG
Source Citations
Strict Prompting

instead of relying on LLM memory.

2. LLM Quota Failures

Implemented:

Gemini
   ↓
Automatic Fallback
   ↓
Groq

for reliability.

3. Hybrid Storage Design

Used:

ChromaDB

for semantic retrieval

and

SQLite

for structured analytics.

This separation improved efficiency.

Scale of Processing

Current System Handles:

Documents
Lecture PDFs
PPTs
PYQ Papers
Processing Pipeline

For a 100-page PDF:

100 pages
↓
~300 chunks
↓
300 embeddings
↓
Stored in ChromaDB
APIs Developed

Around 15+ REST APIs, including:

Upload
Chat
Quiz Generation
Answer Checking
PYQ Analytics
Revision Planning
Profile Management
Recommendations
Technologies Used
Frontend
React.js
Context API
Axios
React Router
Backend
FastAPI
Pydantic
Databases
ChromaDB
SQLite
AI/ML
RAG
Vector Embeddings
Semantic Search
Gemini API
Groq API
Others
PDF Parsing
Prompt Engineering
REST APIs
