# 🚀 Deploying to a Live Public URL (HuggingFace Spaces)

This gets you a link like `https://huggingface.co/spaces/Harivansh124/text-summarizer` that anyone can open and try — the same way your Loan Prediction project is live on Streamlit.

The deployment-ready files are already prepared in `deploy/huggingface-space/` (Dockerfile, requirements.txt, Space README with the required config header, app.py, index.html). You just need to (1) publish your trained model weights and (2) push those files to a new Space.

---

## Step 1 — Push your trained model to the HuggingFace Hub

Your `saved_summary_model/` folder is gitignored (too large for GitHub), so the deployed app needs to load it from the Hub instead of from disk. Add this as a new cell at the **end** of `text_summarizer.ipynb`, after the model is trained and saved:

```python
from huggingface_hub import login

login()  # paste an HF access token (Settings → Access Tokens → New token, "Write" role)

model.push_to_hub("Harivansh124/t5-samsum-summarizer")
tokenizer.push_to_hub("Harivansh124/t5-samsum-summarizer")
```

Run it once. This creates a public model repo at `huggingface.co/Harivansh124/t5-samsum-summarizer` — you can check it's there afterwards.

> If you'd rather not retrain, you can instead upload the existing `saved_summary_model/` folder directly through the HuggingFace website: **New Model → Files → Upload files**, dragging in `config.json`, `pytorch_model.bin` / `model.safetensors`, `tokenizer_config.json`, `spiece.model`, etc.

## Step 2 — Create the Space

1. Go to [huggingface.co/new-space](https://huggingface.co/new-space)
2. **Owner:** your account · **Space name:** `text-summarizer`
3. **SDK:** choose **Docker** (not Gradio/Streamlit — we're deploying the FastAPI app as-is)
4. **Hardware:** Free (CPU basic) is enough for `t5-small`
5. Click **Create Space**

## Step 3 — Push the deployment files

The Space is its own git repo, separate from your GitHub repo. Clone it and copy in the prepared files:

```bash
git clone https://huggingface.co/spaces/Harivansh124/text-summarizer
cd text-summarizer

# copy in the prepared deployment files from your project folder
cp /path/to/T5-Text-Summarizer-SAMSum/deploy/huggingface-space/* .

git add .
git commit -m "Deploy T5 text summarizer"
git push
```

Build takes a few minutes (installing torch + transformers). Once it finishes, your app is live at:

```
https://huggingface.co/spaces/Harivansh124/text-summarizer
```

## Step 4 — Link it everywhere

Once it's live, add the URL to:
- The **🌐 Live Demo** line at the top of `README.md` (marked with a placeholder — replace it)
- Your LinkedIn post (`LINKEDIN_POST.md`) — swap the "link in comments" line for the actual Space URL
- Your resume / portfolio site, alongside the Loan Prediction Streamlit link

---

### Notes

- **Cold starts:** free Spaces sleep after inactivity; the first request after a while takes ~20-30s while it wakes up and loads the model. This is normal.
- **Updating the model later:** if you retrain and push a new version to the Hub model repo, the Space picks it up automatically on next restart — no need to touch the Space's code.
- **Alternative (Render/Railway):** if you'd rather not use HuggingFace Spaces, the same `Dockerfile` works there too — just set the `MODEL_SOURCE` environment variable to `Harivansh124/t5-samsum-summarizer` on whichever platform you use.
