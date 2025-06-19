# Paper2Code: Simple Explanation

Paper2Code is a system that **automatically turns research papers into working code**. Think of it as having an AI read a scientific paper and then write the code to implement what the paper describes.

## How It Works (Simple Overview)

**Input**: You give it a research paper (PDF or LaTeX)
**Output**: You get a complete code repository that implements the paper's method

The system works like having **3 AI specialists** work together:

1. **Planner AI**: Reads the paper and creates a detailed plan
   - "What files do we need?"
   - "How should the code be organized?"
   - "What are the main components?"

2. **Analyzer AI**: Studies each planned component in detail
   - "How exactly should this function work?"
   - "What are the dependencies between files?"

3. **Coder AI**: Writes the actual code
   - Creates all the files in the right order
   - Follows the plan and analysis from the previous steps

## Real Example

If you feed it the famous "Attention Is All You Need" paper (which introduced Transformers), it will:
- Read and understand the paper
- Plan out a Transformer implementation
- Write Python files with attention mechanisms, encoder/decoder layers, etc.
- Give you a working Transformer implementation

## How to Use It

**Super Simple Usage**:
```bash
# Set your OpenAI API key
export OPENAI_API_KEY="your-key-here"

# Run it (processes the example Transformer paper)
cd scripts
bash run.sh
```

**Cost**: About $0.50-$0.70 using OpenAI's models

**What You Get**:
- A folder called `outputs/Transformer_repo/` with working Python code
- All the files needed to run a Transformer model
- Configuration files and documentation

## Different Ways to Run It

1. **With OpenAI** (easiest, costs money): `bash run.sh`
2. **With Free Models** (free, needs more setup): `bash run_llm.sh`
3. **With LaTeX source** (if you have the paper's LaTeX): `bash run_latex.sh`

## What Makes It Special

- **Multi-step thinking**: Unlike simple code generation, it plans first, then analyzes, then codes
- **Understands context**: It reads the whole paper to understand what to implement
- **Creates complete projects**: Not just code snippets, but full working repositories
- **Quality evaluation**: Can score how good the generated code is

## Use Cases

- **Researchers**: Quickly implement papers you're reading
- **Students**: Get working code to understand complex algorithms
- **Developers**: Bootstrap implementations of new AI techniques
- **Reproducibility**: Help make research more reproducible by automating implementation

The system essentially democratizes the ability to turn cutting-edge research into working code, even if you don't have the time or expertise to implement it from scratch.