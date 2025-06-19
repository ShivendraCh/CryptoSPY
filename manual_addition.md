# CryptoSPY Manual Configuration Requirements

This document outlines all the manual configurations and additions required for the CryptoSPY application to work properly.

## 1. Environment Variables (.env file)

Create a `.env` file in the root directory (`d:\CryptoSPY\`) with the following variables:

```
# API Configuration
API_V1_STR=/api/v1
PROJECT_NAME=CryptoSPY

# CORS Configuration
BACKEND_CORS_ORIGINS=["http://localhost:3000"]

# Database Configuration
SQLALCHEMA_DATABASE_URI=sqlite:///./cryptospy.db

# GPU Configuration
USE_GPU=true

# Report Configuration
REPORT_FOOTER="CryptoSPY | Your Organization Name"
```

## 2. Blockchain API Credentials

The application requires API keys for various blockchain networks. Add the following to your `.env` file:

```
# Ethereum API Keys
ETHERSCAN_API_KEY=your_etherscan_api_key
INFURA_API_KEY=your_infura_api_key

# Bitcoin API Keys
BLOCKCYPHER_API_KEY=your_blockcypher_api_key

# BSC API Keys
BSCSCAN_API_KEY=your_bscscan_api_key

# Solana API Keys
SOLANA_RPC_URL=your_solana_rpc_url

# Polygon API Keys
POLYGONSCAN_API_KEY=your_polygonscan_api_key
```

## 3. Model Weights and Files

### 3.1 BERT4ETH Model

Download the required files from Google Drive:
- Transaction Dataset: [Phishing Account](https://drive.google.com/file/d/11UAhLOcffzLyPhdsIqRuFsJNSqNvrNJf/view?usp=sharing), [De-anonymization(ENS)](https://drive.google.com/file/d/1Yveis90jCx-nIA6pUL_4SUezMsVJr8dp/view?usp=sharing), [De-anonymization(Tornado)](https://drive.google.com/file/d/1DMbPSZMSvTYMKUZg3oYKFrjPo2_jeeG4/view?usp=sharing), [Normal Account](https://drive.google.com/file/d/1-htLUymg1UxDrXcI8tslU9wbn0E1vl9_/view?usp=sharing)
- Place these files in the `d:\CryptoSPY\models\BERT4ETH-master\Data\` directory

### 3.2 RevTrack Model

Download the pre-trained model checkpoints:
- Download from the [RevTrack GitHub repository](https://github.com/MITIBMxGraph/RevTrack/tree/main/checkpoints/RevTrack)
- Place these files in the `d:\CryptoSPY\models\RevTrack-main\checkpoints\RevTrack\` directory

### 3.3 Node Embeddings for RevTrack

Download the node embedding file:
- Download `raw_emb.pt` from [Google Drive](https://drive.google.com/file/d/1UBLRxiEg0SK_sWoOWe-55nLOniV9I4HX/view?usp=sharing)
- Place it in the `d:\CryptoSPY\models\RevTrack-main\data\elliptic\raw\` directory

## 4. Elliptic2 Dataset

Download the Elliptic2 dataset:
- Download from [Kaggle](https://www.kaggle.com/datasets/ellipticco/elliptic2-data-set) or [elliptic.co/elliptic2](http://elliptic.co/elliptic2)
- Extract the following files to `d:\CryptoSPY\models\Elliptic2-main\dataset\`:
  ```
  dataset
  ├── background_edges.csv
  ├── background_nodes.csv
  ├── connected_components.csv
  ├── edges.csv
  └── nodes.csv
  ```

## 5. Environment Setup

### 5.1 Python Environment

Create a Python virtual environment:
```bash
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

### 5.2 Frontend Dependencies

Install frontend dependencies:
```bash
cd cryptospy-frontend
npm install
npm install @headlessui/react vis-data --save --legacy-peer-deps
```

## 6. GPU/CUDA Drivers (Optional)

If you want to use GPU acceleration:
1. Install CUDA Toolkit 11.2 or later
2. Install cuDNN compatible with your CUDA version
3. Ensure PyTorch and TensorFlow can detect your GPU

## 7. Email/Webhook Configuration (Optional)

For notifications and alerts, add the following to your `.env` file:

```
# Email Configuration
SMTP_SERVER=smtp.example.com
SMTP_PORT=587
SMTP_USERNAME=your_email@example.com
SMTP_PASSWORD=your_email_password
NOTIFICATION_EMAIL=recipient@example.com

# Webhook Configuration (for integration with other systems)
WEBHOOK_URL=https://example.com/webhook
WEBHOOK_SECRET=your_webhook_secret
```

## 8. API Key Protection (Optional)

To secure the API with an API key, add the following to your `.env` file:

```
# API Security
API_KEY_HEADER=X-API-Key
API_KEY=your_secure_api_key
```

## Running the Application

### Backend

From the root directory:
```bash
cd d:\CryptoSPY\
python -m uvicorn app.main:app --reload
```

### Frontend

From the frontend directory:
```bash
cd d:\CryptoSPY\cryptospy-frontend\
npm run dev
```

## Troubleshooting

- If you encounter `ModuleNotFoundError: No module named 'app'`, make sure you're running the command from the root directory (`d:\CryptoSPY\`)
- If models fail to load, check that all model files are in the correct directories
- For GPU-related issues, try setting `USE_GPU=false` in your `.env` file