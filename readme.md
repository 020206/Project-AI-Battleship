**Project Name**: Project AI Battleship
**Created By**: Kelompok 5
**Date**: 6 Maret 2026

## 1. Executive Summary

### 1.1 Project Overview

- **Tujuan Project**: Membuat bot AI dalam permainna battleship
- **Scope Project**:
  - Analisis dataset Battleship (Moves, Squares, Games)
  - Data preprocessing dan profiling
  - Penggabungan dataset
  - Transformasi data untuk kebutuhan analitik
  - Evaluasi performa AI 
- **Expected Outcomes**:
  - Dataset terintegrasi hasil merge
  - Insight performa AI (win rate, jumlah langkah, dll)
  - Struktur data yang siap digunakan untuk pengembangan AI
- **Timeline**:
  - Pengumpulan data: Minggu 1
  - Analisis & preprocessing: Minggu 2
  - Transformasi & integrasi: Minggu 3
  - Evaluasi & dokumentasi: Minggu 4
  

### 1.2 Stakeholders

- **Project Owner**: Kelompok 5
- **Team Members**:
  - Data Engineer: Adam Noverian
  - Data Analyst: Ghofur Akbar M
  - Project Manager: Alfiansyah Wahyu Pratama

## 2. Data Source Analysis

### 2.1 Data Game Moves

#### Source Details

- **Dataset Name**: Battleship Game Moves
- **URL/Access Point**: https://github.com/cliambrown/battleship-data/blob/main/battleship_game_moves.csv
- **Data Owner**: https://github.com/cliambrown/battleship-data

### Data Analys

- **Format Data**: CSV 
- **Dataset**:
  - battleship_game_moves.csv → 1008 baris, 6 kolom
  - battleship_game_squares.csv → 2400 baris, 7 kolom
  - battleship_games.csv → 59710 baris, 6 kolom
- **Deskripsi**:
  Dataset berisi log permainan Battleship dengan berbagai informasi seperti mode AI,      hasil permainan, jumlah langkah, dan posisi kapal.

## 3. Data Understanding & Struktur Data

### 3.1 Struktur Dataset

- **Moves**:
  - id
  - ai_mode_id
  - autoplay
  - ai_win
  - moves
  - games  
- **Squares**:
  - id
  - ai_mode_id
  - autoplay
  - ai_win
  - ai_ships
  - square
  - games
- **Games**:
  - id
  - timestampUTC
  - ai_win
  - moves
  - autoplay
  - ai_mode_id


#### 3.2 Penjelasan Field Penting

- **ai_mode_id**:
  - 1 = random
  - 2 = probability
  - 3 = learning
- **autoplay**:
  - 0 = manual
  - 1 = otomatis
- **ai_win**:
  - 0 = player menang
  - 1 = AI menang
- **square**:
  - Posisi papan (1-100)

## 4. Data Profiling 

### Analisis statistik sederhana:

- Tidak terdapat missing value (null = 0)
- Semua data bertipe integer
- Data bersih dan konsisten
### Contoh Insight

- Moves memiliki hingga 84 variasi langkah
- Squares memiliki 100 posisi grid
- Games memiliki hampir 60 ribu data permainan

## 5. Data Integration & Struktur Data

### 5.1 Relasi Data

**Dataset dihubungkan melalui:**
- id
- ai_mode_id

### 5.2 Klasifikasi Kolom
**Key/Relasi**
 - id
 - ai_mode_id
**Numerik**
 - Moves
 - games
 - square
 - timestampUTC
**Turunan/Tambahan**
 - ai_win
 - autoplay
 - ai_ships
### Data Transformation
**Beberapa proses transformasi yang dilakukan:**
 - Standarisasi ai_mode_id
 - Validasi Boolean
 - Merge Dataset
 - Konversi Timestamp
 - Feature Engineering:
   - Win Rate AI
   - Rata-rata langkah
   - Frekuensi posisi kapal

## 7. Validasi Data
### Hasil Validasi:
 - Struktur data sesuai
 - Tidak ada missing value
 - Tidak ada duplikasi pada primary key
 - Nilai boolean konsisten
 - Tipe data seragam (integer)

## 3. Data Flow & Arsitektur

### 3.1 Data Flow

```mermaid
graph TD
    A[Data.go.id] --> D[Data Lake]
    B[Kaggle Dataset] --> D
    C[Weather API] --> D
    D --> E[Data Warehouse]
    E --> F[Analytics Layer]
    F --> G[Dashboard]
```

### 3.2 ETL Process Design

- **Extraction Methods**:
  - Data.go.id: Monthly batch download
  - Kaggle: One-time bulk load
  - Weather API: Real-time streaming
- **Transformation Rules**:
  - Standardize timestamps to UTC+7
  - Geocode station locations
  - Normalize weather conditions
- **Loading Procedures**:
  - Incremental loads for streaming data
  - Full refresh for monthly batches
- **Scheduling**:
  - Weather data: Every 5 minutes
  - Usage data: Daily at 00:00
  - Statistics: Monthly at 1st

%% System Architecture Diagram
graph TD
subgraph Data Sources
A[Data.go.id] --> ETL
B[Kaggle Dataset] --> ETL
C[Weather API] --> ETL
D[Research Data] --> ETL
end

subgraph Data Processing
    ETL[ETL Layer]
    DL[(Data Lake)]
    DW[(Data Warehouse)]
    ETL --> DL
    DL --> DW
end

subgraph Analytics
    AN[Analytics Engine]
    DS[Data Science Models]
    DW --> AN
    DW --> DS
end

subgraph Applications
    API[REST API]
    DASH[Dashboard]
    AN --> API
    DS --> API
    API --> DASH
end
%% ETL Workflow
sequenceDiagram
participant S as Source Systems
participant E as Extraction
participant T as Transformation
participant L as Loading
participant DW as Data Warehouse

S->>E: Raw Data
E->>T: Extracted Data
T->>L: Transformed Data
L->>DW: Loaded Data
---



**Kita ingin menganalisis hubungan antara tingkat pendidikan, pengangguran, dan pendapatan di suatu negara.**

**Dataset:**

* **World Bank Open Data:** Data tentang tingkat pendidikan ([https://data.worldbank.org/](https://www.google.com/url?sa=E&q=https%3A%2F%2Fdata.worldbank.org%2F))
* **ILOSTAT:** Data tentang tingkat pengangguran ([https://ilostat.ilo.org/](https://www.google.com/url?sa=E&q=https%3A%2F%2Filostat.ilo.org%2F))
* **Our World in Data:** Data tentang pendapatan per kapita ([https://ourworldindata.org/](https://www.google.com/url?sa=E&q=https%3A%2F%2Fourworldindata.org%2F))
