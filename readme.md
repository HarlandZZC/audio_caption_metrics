# Audio Caption Evaluation Repository

This is a repository designed to evaluate the effectiveness of Audio Caption. Most of the code is adapted from [https://github.com/Labbeti/aac-metrics.git](https://github.com/Labbeti/aac-metrics.git). A big thanks to them!

## Usage Instructions

1. Clone the repository into your audio caption working directory:

   ```bash
   cd path_to_your_audio_caption_repo
   git clone https://github.com/HarlandZZC/audio_caption_metrics.git
   ```

2. Download the required weight files:

   ```bash
   python ./audio_caption_metrics/download.py
   ```

3. Evaluate default metrics:

   ```python
   from audio_caption_metrics.functional.evaluate import evaluate

   candidates: list[str] = ["a man is speaking", "rain falls"]
   mult_references: list[list[str]] = [
       ["a man speaks.", "someone speaks.", "a man is speaking while a bird is chirping in the background"],
       ["rain is falling hard on a surface"]
   ]

   corpus_scores, _ = evaluate(candidates, mult_references)
   print(corpus_scores)
   # dict containing the score of each metric: "bleu_1", "bleu_2", "bleu_3", "bleu_4", "rouge_l", "meteor", "cider_d", "spice", "spider"
   # {"bleu_1": tensor(0.4278), "bleu_2": ..., ...}
   ```

4. Evaluate DCASE2024 metrics
    To compute metrics for the DCASE2023 challenge, just set the argument `metrics="dcase2024"` in `evaluate` function call.

    ```python
    corpus_scores, _ = evaluate(candidates, mult_references, metrics="dcase2024")
    print(corpus_scores)
    # dict containing the score of each metric: "meteor", "cider_d", "spice", "spider", "spider_fl", "fer", "fense", "vocab"
    ```
