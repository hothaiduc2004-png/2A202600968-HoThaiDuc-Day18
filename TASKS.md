# Lab 18 Task List

## 1. Setup
- [ ] Start Qdrant: `docker compose up -d`
- [ ] Install dependencies: `pip install -r requirements.txt`
- [ ] Copy env template: `cp .env.example .env`
- [ ] Fill `OPENAI_API_KEY` if available
- [ ] Run baseline: `python naive_baseline.py`

## 2. Implement modules

### M1 Chunking (`src/m1_chunking.py`)
- [ ] `chunk_semantic()`
- [ ] `chunk_hierarchical()`
- [ ] `chunk_structure_aware()`
- [ ] Verify with `pytest tests/test_m1.py`

### M2 Hybrid Search (`src/m2_search.py`)
- [ ] `segment_vietnamese()`
- [ ] `BM25Search.index()` and `.search()`
- [ ] `DenseSearch.index()` and `.search()`
- [ ] `reciprocal_rank_fusion()`
- [ ] Verify with `pytest tests/test_m2.py`

### M3 Reranking (`src/m3_rerank.py`)
- [ ] `CrossEncoderReranker._load_model()`
- [ ] `CrossEncoderReranker.rerank()`
- [ ] Verify with `pytest tests/test_m3.py`

### M4 Evaluation (`src/m4_eval.py`)
- [ ] `evaluate_ragas()`
- [ ] `failure_analysis()`
- [ ] Verify with `pytest tests/test_m4.py`

### M5 Enrichment (`src/m5_enrichment.py`)
- [ ] Implement enrichment flow
- [ ] Single-call or separate functions for chunk enrichment
- [ ] Ensure fallback when no API key
- [ ] Verify with `pytest tests/test_m5.py`

## 3. Run the pipeline
- [ ] Run: `python src/pipeline.py`
- [ ] Run: `python main.py`
- [ ] Run: `python check_lab.py`
- [ ] Confirm no TODO markers: `grep -r "# TODO" src/m*.py`

## 4. Deliverables
- [ ] `src/m1_chunking.py`
- [ ] `src/m2_search.py`
- [ ] `src/m3_rerank.py`
- [ ] `src/m4_eval.py`
- [ ] `src/m5_enrichment.py`
- [ ] `src/pipeline.py`
- [ ] `analysis/failure_analysis.md`
- [ ] `analysis/reflections/reflection_[HọTên].md`
- [ ] `reports/ragas_report.json`

## 5. Reflection file
Create `analysis/reflections/reflection_[HọTên].md` with:
- Mapping lecture concepts to code
- Challenges and debugging
- Project action plan + timeline
