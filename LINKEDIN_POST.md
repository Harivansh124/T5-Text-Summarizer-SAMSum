🚀 New project: Text Summarizer — Fine-Tuned T5 Transformer (HuggingFace NLP / Generative AI)

Continuing my hands-on AI/ML portfolio, this one turns any block of text — notes, explanations, articles, conversations — into a short, clean summary.

📌 What it does: paste your content, get back a concise one-line summary — generated live by a fine-tuned transformer, served through a FastAPI backend with a simple web UI.

🔧 How it was built:
• Base model: T5-small, fine-tuned on the SAMSum conversational dataset (4,000 text-summary pairs)
• Framed as a pure text-to-text task (T5's native seq2seq format)
• 6 training epochs — validation loss converged smoothly to 0.348 with no overfitting
• Inference via beam search (num_beams=4) for fluent, non-repetitive output
• Same preprocessing pipeline reused in training and inference, so the model always sees text the way it was trained

🧰 Stack: PyTorch · HuggingFace Transformers · FastAPI · vanilla JS frontend

This project rounds out the NLP side of my portfolio alongside CNN (vision), RL (decision-making), and clustering (unsupervised) work — building toward a well-rounded, applied AI/ML Engineer skill set.

Grateful to Shraddha Ma'am [@ tag her here] for the guidance through this learning journey. 🙏

Code + full write-up on GitHub (link in comments 👇)

#MachineLearning #NLP #GenerativeAI #Transformers #HuggingFace #PyTorch #FastAPI #DeepLearning #AIEngineer #Python #TextSummarization

---
NOTE FOR HARIVANSH: LinkedIn @mentions only work if typed directly in the LinkedIn post box (it needs to resolve to her actual profile) — I can't embed that from here. When posting, type "@" then her name where marked above and pick her profile from the dropdown.
