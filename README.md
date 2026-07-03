This repository contains my deliverables for Project 4 in CSC 6400: 
System Administration and Maintenance. The goal of the project is to size 
a small AI estate, classify its data, and provide evidence that the pgvector 
extension is installed and functioning.

## Repository Contents

- **SIZING.txt**  
  Full sizing of the AI estate, including:
  - Model weights (13B INT4)
  - Vector database (5M × 1536 halfvec + HNSW)
  - RAG corpus and fine‑tuning dataset (with explicit assumptions)
  - Total estate size (“this is what we are buying”)
  - Tiering table (hot / warm / cold / archive)
  - Grounding in my actual storage audit (`df`, `lsblk`)
  - pgvector predicted vs measured size

- **data_classification.yaml**  
  Governance and tiering policy for all estate assets.  
  Follows the structure of the example in the professor’s repository.

- **pgvector_proof.txt**  
  Short description of how I created and measured the `chunks` table using 
  pgvector, plus the measured size (32 kB).  
  A screenshot is included in the repo.

- **REPORT.docx**  
  Narrative explanation of the estate sizing, tiering decisions, storage audit, 
  and governance policy.

## How to Reproduce the pgvector Proof

The pgvector setup script is provided by the professor in the course code 
repository:

https://github.com/mlitman/system-admin-and-maintenance-code

To reproduce my pgvector proof:

1. Clone the professor’s repository:
git clone https://github.com/mlitman/system-admin-and-maintenance-code.git 

2. Navigate to the pgvector setup script:
cd system-admin-and-maintenance-code/04-storage-administration/code/

3. Run the script on your PostgreSQL instance:
sudo -u postgres psql -f pgvector_setup.sql

My measured output was **32 kB**, which is expected for an empty pgvector table 
(metadata + page alignment).
