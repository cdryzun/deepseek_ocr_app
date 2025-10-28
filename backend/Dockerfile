# Backend Dockerfile - FastAPI + DeepSeek-OCR
FROM harbor.cpinnov.run/devops/pytorch:25.09-py3

ENV HTTP_PROXY="http://10.16.18.2:34567" \
    HTTPS_PROXY="http://10.16.18.2:34567" \
    ALL_PROXY="http://10.16.18.2:34567"

ENV PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1 \
    HF_HOME=/models

WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --upgrade pip --proxy http://10.16.18.2:34567  && pip install -r requirements.txt --proxy http://10.16.18.2:34567

# Copy backend code
COPY main.py .

EXPOSE 8000

# Use uvicorn with reasonable workers for GPU workload
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--workers", "1"]