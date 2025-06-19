# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

### Quick Start (Example with Transformer paper)
```bash
# Using OpenAI API (requires OPENAI_API_KEY)
cd scripts && bash run.sh

# Using open-source models with vLLM
cd scripts && bash run_llm.sh

# Using LaTeX source instead of PDF
cd scripts && bash run_latex.sh      # OpenAI
cd scripts && bash run_latex_llm.sh  # vLLM
```

### Environment Setup
```bash
# Install dependencies
pip install -r requirements.txt

# Or install selectively
pip install openai     # For OpenAI API
pip install vllm       # For open-source models
pip install tiktoken   # For evaluation
```

### Evaluation
```bash
# Reference-free evaluation
cd codes/
python eval.py --paper_name Transformer --pdf_json_path ../examples/Transformer_cleaned.json --data_dir ../data --output_dir ../outputs/Transformer --target_repo_dir ../outputs/Transformer_repo --eval_result_dir ../results --eval_type ref_free --generated_n 8 --papercoder

# Reference-based evaluation (requires gold repository)
cd codes/
python eval.py --paper_name Transformer --pdf_json_path ../examples/Transformer_cleaned.json --data_dir ../data --output_dir ../outputs/Transformer --target_repo_dir ../outputs/Transformer_repo --gold_repo_dir ../examples/Transformer_gold_repo --eval_result_dir ../results --eval_type ref_based --generated_n 8 --papercoder
```

## Architecture

### Multi-Agent Pipeline
Paper2Code uses a sequential 3-stage pipeline with specialized AI agents:

1. **Planning Stage** (`1_planning.py`): 4-step planning process
   - Overall plan → Architecture design → Logic design → Config generation
   - Outputs: `planning_artifacts/`, `planning_config.yaml`

2. **Analysis Stage** (`2_analyzing.py`): Detailed logic analysis
   - Analyzes each planned file's requirements and dependencies
   - Outputs: `analyzing_artifacts/`

3. **Coding Stage** (`3_coding.py`): Sequential code generation
   - Generates files following dependency order from planning
   - Outputs: `{paper_name}_repo/` (final repository)

### File Structure
- `codes/`: Core pipeline scripts (numbered 0-3 for sequence)
- `scripts/`: Shell scripts for different execution modes
- `data/`: Benchmark datasets and evaluation prompts
- `examples/`: Sample papers (Transformer) and outputs
- `outputs/`: Generated artifacts and repositories

### Key Components
- **Dual Implementation**: Each stage has both OpenAI (`*_planning.py`) and vLLM (`*_planning_llm.py`) versions
- **Artifact Management**: Stages communicate through structured JSON/YAML files
- **Cost Tracking**: Accumulated API cost monitoring across stages
- **Preprocessing**: `0_pdf_process.py` cleans paper JSON format for AI processing

### Data Flow
```
PDF/LaTeX Paper → Cleaned JSON → Planning Artifacts → Analysis Artifacts → Code Repository → Evaluation Scores
```

### Configuration
- Environment variables: `OPENAI_API_KEY` for OpenAI models
- Model selection: Default vLLM model is `deepseek-ai/DeepSeek-Coder-V2-Lite-Instruct`
- Evaluation: Uses `o3-mini` for quality scoring (1-5 scale)