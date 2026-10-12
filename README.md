# 4Chain: Blockchain-Based Academic Credential Verification System

A secure, decentralized platform designed to issue, store, and verify academic credentials and certificates immutably using blockchain technology and InterPlanetary File System (IPFS) storage.

---

## About The Project

Traditional academic credential verification relies on centralized institutional databases or manual paper checks, making certificate tampering and forgery difficult to catch efficiently. 4Chain solves this by hashing credential metadata, storing verifiable documents decentralized via IPFS, and anchoring verification proofs to ensure tamper-proof authenticity and instant QR-code verification.

---

## Tech Stack

* **Backend:** Python, Flask
* **Decentralized Storage:** IPFS (InterPlanetary File System)
* **Blockchain Integration:** Smart contracts / Verification hashing
* **Document Processing:** PDF generation, PyMuPDF, qrcode generation

---

## Core Features

* **Immutable Credential Issuance:** Generates unique cryptographic hashes for student transcripts and certificates.
* **Decentralized Storage:** Offloads heavy PDF payloads to IPFS while storing only lightweight pointers and hashes on-chain.
* **Instant QR Code Verification:** Embeds dynamic verification URLs and hashes directly into generated PDF credentials for rapid scanning.
* **Tamper Detection:** Instantly flags altered documents by comparing real-time file hashes against immutable blockchain records.

---

## System Architecture & Workflow

```mermaid
graph TD
    %% Define Node Styles
    classDef userNode fill:#f4f4f9,stroke:#666,stroke-width:2px,rx:10,ry:10;
    classDef systemNode fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,rx:10,ry:10;
    classDef storageNode fill:#fff3e0,stroke:#f57c00,stroke-width:2px,rx:10,ry:10;
    classDef chainNode fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,rx:10,ry:10;

    %% Issuance Flow
    A[Issuer / Admin] -->|Submits Data| B(Backend API)
    B -->|Generates PDF & Hash| C{Document Processor}
    C -->|Embeds QR Code| D[Credential PDF]
    C -->|Uploads File| E[(IPFS Network)]
    E -->|Returns CID Hash| B
    B -->|Anchors Hash| F[(Blockchain Ledger)]
    
    %% Verification Flow
    G[Verifier / Recruiter] -->|Scans QR or Uploads PDF| H(Verification Service)
    H -->|Fetches File via CID| E
    H -->|Validates Immutable Hash| F
    F -.->|Tamper Status| H
    H -.->|Authenticity Result| G

    %% Apply Styles
    A,G class:userNode;
    B,H,C class:systemNode;
    E class:storageNode;
    F class:chainNode;

```

---

## Project Structure

```text
4chain/
├── app/
│   ├── routes/         # API endpoints for issuance and verification
│   ├── services/       # IPFS integration and hashing logic
│   ├── utils/          # PDF generation and QR code embedding
│   └── templates/      # Frontend views / dashboard templates
├── blockchain/         # Smart contracts and connection scripts
├── requirements.txt    # Python dependencies
└── run.py              # Application entry point

```

---

## Getting Started

### Prerequisites

* Python 3.10+
* Local or remote IPFS node running
* Git

### Installation & Setup

1. **Clone the repository:**
```bash
git clone https://github.com/alishajamal/4chain.git
cd 4chain

```


2. **Create and activate a virtual environment:**
```bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate

```


3. **Install dependencies:**
```bash
pip install -r requirements.txt

```


4. **Configure environment variables:**
Create a `.env` file in the root directory and configure your IPFS provider and blockchain endpoints:
```env
IPFS_HOST=127.0.0.1
IPFS_PORT=5001
BLOCKCHAIN_RPC_URL=your_rpc_url_here

```


5. **Run the application:**
```bash
python run.py

```



---

## Contributors & Collaborative Roles

This project was built as a collaborative effort with shared responsibilities across the backend architecture:

* **Alisha Jamal:** cryptographic hash generation, IPFS storage integration, and QR code embedding.
* **Devansh:** Blockchain integration and core backend logic.
