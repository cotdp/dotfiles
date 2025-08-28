# AI Model Selection Guide

**IMPORTANT**: Do not change AI models in existing code unless explicitly requested. When creating new AI features or asked to select a model, use the following guidance to choose the most appropriate option.

## When to Choose Different Model Types

### Cost-Effective Models (Default Choice)
- **Simple tasks**: Basic coding, Q&A, documentation
- **High-volume applications**: Batch processing, automated responses
- **Fine-tuning**: Custom model training

### Reasoning Models
- **Complex problem-solving**: Multi-step analysis, strategic planning
- **Math and logic**: Calculations, proofs, puzzles
- **Research analysis**: Data synthesis, comparative studies

### Multimodal Models  
- **Image analysis**: Chart reading, visual data extraction
- **Mixed content**: Text + image inputs, document analysis

### Specialized Models
- **Search + AI**: Real-time information with reasoning
- **Image generation**: Creative visuals, diagrams, art

## OpenAI Models

| Model | Best For | Pricing (Input/Output per 1M tokens) |
|-------|----------|--------------------------------------|
| `gpt-5-nano` | Most cost-effective for general tasks, fine-tuning, high-volume apps | $0.05 / $0.40 |
| `gpt-5-mini` | Balanced performance/cost for moderate complexity tasks | $0.25 / $2.00 |
| `gpt-5` | Latest flagship with advanced reasoning, multimodal capabilities | $1.25 / $10.00 |
| `gpt-4.1-nano` | Fast, focused tasks with good efficiency | $0.10 / $0.40 |
| `gpt-4o-mini` | Efficient multimodal (text + images) processing | $0.15 / $0.60 |
| `o3-mini` | Cost-effective reasoning for logic, math, step-by-step problems | $1.10 / $4.40 |
| `o4-mini` | Latest small reasoning model with enhanced capabilities | $1.10 / $4.40 |
| `o3` | High-performance reasoning for complex analysis | $2.00 / $8.00 |
| `o3-pro` | Advanced reasoning for most complex problems | $20.00 / $80.00 |
| `gpt-image-1` | Image generation with multiple sizes and quality levels | Varies by quality |

## Perplexity Models (Search + AI)

| Model | Best For | Pricing (Input/Output per 1M tokens) |
|-------|----------|--------------------------------------|
| `sonar` | Quick facts, news updates, simple Q&A, high-volume apps | $1.00 / $1.00 + fees |
| `sonar-pro` | Complex queries, competitive analysis, detailed research | $3.00 / $15.00 + fees |
| `sonar-reasoning` | Logic puzzles, math problems with transparent reasoning | $1.00 / $5.00 + fees |
| `sonar-reasoning-pro` | Complex problem-solving, research analysis, strategic planning | $2.00 / $8.00 + fees |
| `sonar-deep-research` | Academic research, market analysis, comprehensive reports | $2.00 / $8.00 + extras |

*Note: All Perplexity models include additional request fees. Total cost = Token costs + Request fees*

## Claude Models

| Model | Best For | Pricing (Input/Output per 1M tokens) |
|-------|----------|--------------------------------------|
| `claude-sonnet-4` | Coding agents, software development, complex workflows, analysis | $3.00 / $15.00 |
