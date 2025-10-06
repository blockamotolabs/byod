# BYOD - Bring Your Own Data

Community cache repository for [Termina](https://ordinals.com/content/7bdc2aeab14b6c56a7fc6746cbd0b8092d08eb2d0d820e43b67613cf39f36614i0) - Bitcoin Ordinals Metaverse Bitmap console.

## What is this?

This repository contains crawled data for Bitmap Districts that you can import into Termina to accelerate your exploration of the Bitcoin Ordinals ecosystem. Instead of crawling from scratch, you can import community-validated data and build upon it.

## Cache Contents

The `crawl_cache.json` file contains:
- **Reinscriptions**: District numbers that have been reinscribed
- **Children**: District numbers that have child inscriptions
- **Parents**: District numbers that have parent inscriptions
- **Sessions**: Crawl session logs tracking which ranges have been checked

## Importing the Cache

### Step 1: Download the Cache

Download the latest `crawl_cache.json` file from this repository.

### Step 2: Import into Termina

1. Open Termina in your browser
2. Run the command: `CRAWL file`
3. Select the `crawl_cache.json` file you downloaded
4. Termina will automatically merge the data with your existing cache (if any) and remove duplicates

You'll see output like:
```
✓ Merged 12,345 reinscriptions (+5,678 new)
✓ Merged 8,901 children (+2,345 new)
✓ Merged 1,234 parents (+567 new)
Cache updated successfully!
```

### Step 3: Start Exploring

The data is now ready for you to explore!

## Contributing Your Data

Help expand the community cache by contributing your crawled data!

### Step 1: Export Your Cache

In Termina, run: `CRAWL save`

This downloads a file named `crawl_cache_[timestamp].json` with your local cache.

### Step 2: Prepare Your Contribution

Before submitting a pull request, ensure there are additions to the index, and do not remove any existing data (this will be ignored).

### Step 3: Submit a Pull Request

1. Fork this repository
2. Create a new branch: `git checkout -b crawl-range-[start]-[end]`
   - Example: `crawl-range-10000-20000`
3. Add your cache file or merge your data into the existing `crawl_cache.json`
4. Create a pull request with:
   - **Title**: `Crawl data for districts [start]-[end]`
   - **Description**: Include:
     - District range covered
     - Date of crawl
     - Number of new reinscriptions/children/parents found

### Example PR Description

```
District Range: 10000-20000
Crawl Date: 2025-10-05
New Reinscriptions: 234
New Children: 89
New Parents: 12

Complete crawl of districts 10000-20000 with comprehensive reinscription
and children checks.
```

## Validation Process

Any additions to the data will be spot-checked and validated before accepted.

## Cache Schema

The cache file structure:

```json
{
  "reinscriptions": [0, 1, 42, 123, ...],
  "children": [5, 10, 99, ...],
  "parents": [7, 15, 88, ...],
  "sessions": [
    {
      "range": "0-10000",
      "type": "reinscriptions+children",
      "timestamp": 1728123456789,
      "counts": {
        "reinscriptions": 234,
        "children": 89
      }
    }
  ]
}
```

## Why Contribute?

- **Accelerate the Community**: Help others explore faster
- **Build the Index**: Create the most comprehensive Bitmap Districts index
- **Collaboration**: Work together to map the Bitmap landscape

## Support

For questions or issues, open an issue in this repository.
