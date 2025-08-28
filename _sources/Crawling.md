# Crawling Data

Proses untuk Crawling data yaitu, 

## 1. Install Library Sprynger

Untuk memasang library Python resmi Springer Nature, jalankan:

```bash
!pip install sprynger
```

## 2. Menyiapkan API Key
Setiap pencarian membutuhkan API Key dari Springer Nature agar kita diizinkan mengambil data.
Daftar di Springer Nature Developer di https://dev.springernature.com/#api

## 3. Script Crawling Python

Setelah mendapatkan api key dari Springer Nature Developer, masukkan API yang telah didapat ke dalam code dibawah ini, dan saya mengimplementasikannya dengan menggunakan keyword web mining

### A. Keyword Web Mining 

```python
import requests
import pandas as pd

# API Key Meta API
api_key = "00e6e834d8efc1827d4b56d5091e03b1"
keyword = "web mining"

url = "https://api.springernature.com/meta/v2/json"
params = {
    "q": f'keyword:"{keyword}"',
    "api_key": api_key,
    "p": 10  # jumlah hasil per request
}

response = requests.get(url, params=params)

# List untuk menyimpan semua record
all_records = []

if response.status_code == 200:
    data = response.json()
    total_results = data['result'][0].get('total', 0)
    print(f"Total hasil: {total_results}\n")
    
    for record in data.get("records", []):
        doi = record.get('doi', 'N/A')
        title = record.get('title', 'No title')
        abstract = record.get('abstract', 'No abstract')
        print(f"DOI: {doi}")
        print(f"Title: {title}")
        print(f"Abstract: {abstract}\n")
        
        # Simpan record ke list
        all_records.append({
            "keyword": keyword,
            "doi": doi,
            "title": title,
            "abstract": abstract
        })
else:
    print("Error:", response.status_code, response.text)

# Simpan ke CSV
if all_records:
    df = pd.DataFrame(all_records)
    csv_filename = f"{keyword.replace(' ', '_')}.csv"  # hasil: web_mining.csv
    df.to_csv(csv_filename, index=False, encoding="utf-8")
    print(f"✅ Data berhasil disimpan ke {csv_filename}")

```
Hasil yang didapatkan adalah 


### B. Keyword Web Usage Mining 

``` python
import requests
import pandas as pd

# API Key Meta API
api_key = "00e6e834d8efc1827d4b56d5091e03b1"
keyword = "web usage mining"

url = "https://api.springernature.com/meta/v2/json"
params = {
    "q": f'keyword:"{keyword}"',
    "api_key": api_key,
    "p": 10  # jumlah hasil per request
}

response = requests.get(url, params=params)

# List untuk menyimpan semua record
all_records = []

if response.status_code == 200:
    data = response.json()
    total_results = data['result'][0].get('total', 0)
    print(f"Total hasil: {total_results}\n")
    
    for record in data.get("records", []):
        doi = record.get('doi', 'N/A')
        title = record.get('title', 'No title')
        abstract = record.get('abstract', 'No abstract')
        print(f"DOI: {doi}")
        print(f"Title: {title}")
        print(f"Abstract: {abstract}\n")
        
        # Simpan record ke list
        all_records.append({
            "keyword": keyword,
            "doi": doi,
            "title": title,
            "abstract": abstract
        })
else:
    print("Error:", response.status_code, response.text)

# Simpan ke CSV
if all_records:
    df = pd.DataFrame(all_records)
    csv_filename = f"{keyword.replace(' ', '_')}.csv"  # keyword_web_mining.csv
    df.to_csv(csv_filename, index=False, encoding="utf-8")
    print(f"\n✅ Data berhasil disimpan ke {csv_filename}")

```
