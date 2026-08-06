FROM python:3.10-slim

WORKDIR /app

# System deps for torch/sentencepiece build
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

COPY app.py .
COPY index.html .

# HuggingFace Spaces (Docker SDK) expects the app to listen on port 7860
ENV MODEL_SOURCE="Harivansh124/t5-samsum-summarizer"
EXPOSE 7860

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]
