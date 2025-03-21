# deepseek-ai-deepseek-math-7b-instruct-FineTuned

## Overview
EmojiMath is an AI-powered math solver that interprets and solves arithmetic equations represented using emojis. This project fine-tunes the **DeepSeek-Math-7B-Instruct** model using **LoRA** to understand and solve emoji-based equations. The model is deployed using **Gradio** for an interactive experience.

## Features
✅ Fine-tuned **DeepSeek-Math-7B-Instruct** for emoji-based equations  
✅ Uses **LoRA** for efficient fine-tuning  
✅ Dataset of emoji math problems in JSON format  
✅ Deployed using **Gradio** for real-time interaction  
✅ Supports **Hugging Face Transformers** and **Unsloth** for optimization  

## Dataset
The dataset consists of simple emoji-based arithmetic problems with solutions and explanations. Example:
```json
{
    "problem": "🍎 + 🍎 + 🍎 = 12",
    "solution": "🍎 = 4",
    "explanation": "Dividing both sides by 3: 12 ÷ 3 = 4."
}
```

## Installation
To set up and run the project, follow these steps:

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/LaibaZaffar/deepseek-ai-deepseek-math-7b-instruct-FineTuned

```

### 2️⃣ Install Dependencies
```bash
pip install -q unsloth bitsandbytes transformers accelerate peft trl datasets gradio
```

### 3️⃣ Set Up Hugging Face Token
set it in your environment:
```bash
export HF_TOKEN=your_huggingface_api_token
```

### 4️⃣ Run Fine-Tuning
```bash
python train.py
```

### 5️⃣ Launch the Gradio App
```bash
python app.py
```
This will start a **Gradio** interface where you can enter emoji equations and get AI-generated solutions.

## Model Fine-Tuning
We used **LoRA** for efficient fine-tuning:
```python
model = FastLanguageModel.get_peft_model(
    model,
    r=64,
    target_modules=["q_proj", "k_proj", "v_proj", "o_proj",
                    "gate_proj", "up_proj", "down_proj"],
    lora_alpha=32,
    lora_dropout=0.05,
    bias="none",
    use_gradient_checkpointing="unsloth"
)
```

## Testing the Model
Once trained, test the model with different emoji equations:
```python
test_cases = [
    "🍎 + 🍎 = 15",
    "🍌 × 4 = 20",
    "🍪 + 🍪 = 8"
]
results = test_model(model, tokenizer, test_cases)
```

## Gradio Interface
We use **Gradio** for a simple web-based interface:
```python
def solve_math_problems(input_cases):
    test_cases = input_cases.split("\n")
    results = test_model(model, tokenizer, test_cases)
    output = "\n".join([f"{p}: {s}" for p, s in results])
    return output

iface = gr.Interface(
    fn=solve_math_problems,
    inputs=gr.Textbox(lines=5, placeholder="Enter emoji equations here..."),
    outputs="text",
    title="EmojiMath",
    description="Turn emojis into equations and watch AI crack the code!"
)
iface.launch()
```

## Future Enhancements
🚀 Expand the dataset with more complex emoji equations  
🚀 Optimize for **multi-modal learning** to include both emojis and numbers  

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository
2. Create a new branch (`git checkout -b feature-branch`)
3. Commit your changes (`git commit -m "Added new feature"`)
4. Push to the branch (`git push origin feature-branch`)
5. Open a Pull Request

## License
This project is licensed under the **MIT License**.


