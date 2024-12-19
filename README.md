# 5W1H-prompt-strategies

This project explores various prompting strategies for the 5W1H task (Who, What, Where, When, Why, How) using zero-shot, few-shot, and Chain-of-Thought (CoT) approaches. 

## Table of Prompts Used

| **Prompt Number**   | **Description**              | 
|--------------------|------------------------------|
| P1  | P1 (zero-shot) is a prompt that defines the extraction task. In the system role, general instructions are given, general rules are established, and it is emphasized that the responses must be directly based on the provided content. In the user role, the news article is provided, including the headline, lead, and body.   | 
| P2  | P2 (zero-shot) builds upon P1 by adding a detailed description of each 5W1H element.         | 
| P3  | P3 (zero-shot) extends P2 by adding the instruction, “Only use excerpts from the provided context.           | 
| P4  | P4 (one-shot) adds to P3 an example that includes a news article and the expected responses.           | 
| P5  | P5 (few-shot) builds on P4 by adding a second example along with the expected answers.           | 
| P6  | P6 (few-shot) builds on P5 by adding a third example with the corresponding expected answers.           | 
| P7  | P7 (Extractive COT, ours) defines guidelines for removing irrelevant text. It specifically asks to remove sentences in the body of the text that do not directly relate to the headline and lead of the news. It includes one example. After irrelevant text is filtered out, the 5W1H extraction is performed using one-shot prompting.           | 
| P8  | P8 (Extractive COT, ours) mirrors P7 but uses few-shot prompting based on two examples.           | 
| P9  | P9 (Extractive COT, ours) follows the same logic as P8 but incorporates three examples.           | 
| P10  | P10 (Question-level COT, ours) introduces complex reasoning for each question using one example. The reasoning per question is based on annotation guidelines used in [https://api.semanticscholar.org/CorpusID:216033759].           | 
| P11  | P11 (Question-level COT, ours) mirrors P10 but with two examples, making it COT few-shot.           | 

```plaintext
    messages=[
      {
        "role": "system",

        "content": f"""You will be provided with two short text responses from a news article. One is the real response, and the other is a generated response produced by a generative model. The evaluation will focus on the '{question_}' question from the 5W1H framework.
                      Your task is to evaluate the generated response by comparing it with the real response, focusing on the following four criteria:

                      1. **Consistency**: Determine whether the generated response aligns factually with the real response. Are the facts in the generated text accurate and in line with the real information? Penalize any inaccuracies or fabricated details. Provide a score from 1 (poor) to 5 (excellent) and justify your reasoning.
                      2. **Fluency**: Evaluate the grammatical correctness and readability of the generated response. Is the text well-written, free of grammatical errors, and easy to understand? Provide a score from 1 (poor) to 5 (excellent) and justify your evaluation.
                      3. **Relevance**: Determine if the generated response contains only the essential information related to the question without including irrelevant details or redundant content. Provide a score from 1 (poor) to 5 (excellent) and explain your reasoning.

                      For each criterion, please assign a score between 1 and 5, accompanied by a brief explanation of the score."""
      },
      {
        "role": "user",
        "content": (f"You are provided with two short text responses for the '{question_}' question:\n"
                    f"Real: {real_}\n"
                    f"Generated: {predict_}\n\n"
                    "Please evaluate the following aspects based on the provided context:"
                    "1. **Consistency**: <score from 1 to 5> /// <brief explanation>\n"
                    "2. **Fluency**: <score from 1 to 5> /// <brief explanation>\n"
                    "3. **Relevance**: <score from 1 to 5> /// <brief explanation>\n"
        )
      }
    ],
    temperature = 0.2,
    max_tokens  = 2000,
    top_p       = 0.1
  )

---
