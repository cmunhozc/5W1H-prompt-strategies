# 5W1H-prompt-strategies

This project explores various prompting strategies for the 5W1H task (Who, What, Where, When, Why, How) using zero-shot, few-shot, and Chain-of-Thought (CoT) approaches. 

## Table of Prompts Used

| **Prompt Number**   | **Description**              | 
|--------------------|------------------------------|
| P1  | **(zero-shot)** is a prompt that defines the extraction task. In the system role, general instructions are given, general rules are established, and it is emphasized that the responses must be directly based on the provided content. In the user role, the news article is provided, including the headline, lead, and body.   | 
| P2  | **(zero-shot)** builds upon P1 by adding a detailed description of each 5W1H element.         | 
| P3  | **(zero-shot)** extends P2 by adding the instruction, “Only use excerpts from the provided context.           | 
| P4  | **(one-shot)** adds to P3 an example that includes a news article and the expected responses.           | 
| P5  | **(few-shot)** builds on P4 by adding a second example along with the expected answers.           | 
| P6  | **(few-shot)** builds on P5 by adding a third example with the corresponding expected answers.           | 
| P7  | **(Extractive COT, ours)** defines guidelines for removing irrelevant text. It specifically asks to remove sentences in the body of the text that do not directly relate to the headline and lead of the news. It includes one example. After irrelevant text is filtered out, the 5W1H extraction is performed using one-shot prompting.           | 
| P8  | **(Extractive COT, ours)** mirrors P7 but uses few-shot prompting based on two examples.           | 
| P9  | **(Extractive COT, ours)** follows the same logic as P8 but incorporates three examples.           | 
| P10  | **(Question-level COT, ours)** introduces complex reasoning for each question using one example. The reasoning per question is based on annotation guidelines used in [Evaluating the Inverted Pyramid Structure through Automatic 5W1H Extraction and Summarization](https://api.semanticscholar.org/CorpusID:216033759).           | 
| P11  | **(Question-level COT, ours)** mirrors P10 but with two examples, making it COT few-shot.           | 


