# BYOD - Bring Your Own Data

Community cache repository for [Termina][https://ordinals.com/content/7bdc2aeab14b6c56a7fc6746cbd0b8092d08eb2d0d820e43b67613cf39f36614i0] - Bitcoin Ordinals Metaverse Bitmap console.

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

For questions or issues:
- Open an issue in this repository
- Join the Termina community discussions
- Check the [Termina documentation](https://github.com/blockamotolabs/termina)

---

## WorldTree Data

The `worldtree.json` file contains complete hierarchical trees of bitmap districts with enriched inscription data.

### What's in worldtree.json?

The WorldTree cache includes:
- **Complete District Trees**: Full hierarchical structure of parent-child relationships for bitmap districts
- **Inscription Info**: ID, sat number, content type, and other metadata for each inscription
- **Decoded Metadata**: CBOR-decoded metadata fields when available
- **Text Content**: Indexed content from text-based inscriptions for search

### Structure

Each district tree in the cache contains:
```json
{
  "sat": 1234567890,
  "districts": [123, 456],
  "treeJson": {
    "index": 0,
    "info": {
      "id": "abc123...i0",
      "sat": 1234567890,
      "contentType": "text/plain",
      "metadata": {...}
    },
    "children": [...],
    "reinscriptions": [...]
  },
  "timestamp": 1728123456789
}
```

## Importing WorldTree Data

### Step 1: Download the WorldTree

Download the latest `worldtree.json` file from this repository.

### Step 2: Import into Termina

1. Open Termina in your browser
2. Run the command: `WORLDTREE file`
3. Select the `worldtree.json` file you downloaded
4. Termina will merge the data with your existing WorldTree cache

You'll see output like:
```
✓ Imported 150 district trees
✓ Total inscriptions: 2,345
WorldTree cache updated successfully!
```

## Building Your Own WorldTree Data

You can contribute to the community cache by building and enriching WorldTree data for specific district ranges.

### Prerequisites

First, you need crawl data to know which districts to build trees for:
1. Import `crawl_cache.json` (see above) OR run your own crawl
2. This identifies which districts have reinscriptions, children, or parents

### Building Trees

Build trees for all discovered districts:
```
WORLDTREE bitmap
```

Or build for a specific range:
```
WORLDTREE bitmap 0 1000
```

### Enriching with Data

After building trees, enrich them with inscription data:

**Option 1: Full enrichment (recommended for contributions)**
```
WORLDTREE bitmap full
```
This builds each tree and fully enriches it before moving to the next.

**Option 2: Step-by-step enrichment**
```
WORLDTREE bitmap info         # Fetch inscription info (content types, etc.)
WORLDTREE bitmap metadata     # Decode CBOR metadata
WORLDTREE bitmap content      # Index text content for search
```

**Option 3: Quick enrichment**
```
WORLDTREE bitmap enrich       # All three steps sequentially
```

All commands support district ranges:
```
WORLDTREE bitmap full 0 100   # Build and enrich districts 0-100
```

### Exporting Your WorldTree

Once you've built and enriched your trees:
```
WORLDTREE save
```

This downloads `worldtree_[timestamp].json` with your complete cache.

## Contributing WorldTree Data

Help build the most comprehensive Bitcoin Ordinals district map!

### Step 1: Build and Enrich

1. Import the latest `crawl_cache.json` to know which districts to process
2. Choose a district range that needs coverage (check existing worldtree.json to see what's missing)
3. Build and enrich your chosen range:
   ```
   WORLDTREE bitmap full [start] [end]
   ```
4. Export your data:
   ```
   WORLDTREE save
   ```

### Step 2: Prepare Your Contribution

Before submitting:
- Ensure all inscriptions in your range are fully enriched (info + metadata + content)
- Verify the data quality by viewing several trees in Termina
- Note any districts that failed or have missing data

### Step 3: Submit a Pull Request

1. Fork this repository
2. Create a new branch: `git checkout -b worldtree-[start]-[end]`
   - Example: `worldtree-5000-10000`
3. Either:
   - Add your file as `worldtree_[start]-[end].json`, OR
   - Merge your data into the existing `worldtree.json`
4. Create a pull request with:
   - **Title**: `WorldTree data for districts [start]-[end]`
   - **Description**: Include:
     - District range covered
     - Date of build/enrichment
     - Number of trees added
     - Total inscriptions enriched
     - Any districts that had issues

### Example PR Description

```
District Range: 5000-10000
Build Date: 2025-10-08
Trees Added: 42
Total Inscriptions: 1,247
Enrichment: Full (info + metadata + content)

Complete WorldTree build and enrichment for districts 5000-10000.
All text-based inscriptions indexed for search.

## Quality Guidelines

For WorldTree contributions:
- ✅ Full enrichment (info + metadata + content) preferred
- ✅ Verify data accuracy by viewing trees in Termina
- ✅ Include district range in filename/PR description
- ❌ Don't remove existing tree data

---
