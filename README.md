# Swara Transformer — Raag Bhairav Melody Generation

A small PyTorch Transformer experiment that learns next-token patterns from a sequence of Hindustani classical music swaras associated with **Raag Bhairav**, then generates a short token sequence and converts it into a simple synthesized WAV file.

This is an educational generative-model prototype. It is not a validated model of raag grammar or a substitute for performance by a trained musician.

## Repository contents

| File | Description |
| --- | --- |
| `Bhairav.ipynb` | Notebook containing tokenization, Transformer training, generation, and WAV synthesis |
| `generated_bhairav.wav` | A generated audio artifact committed to the repository |
| `README.md` | Project documentation |

## How it works

1. **Tokenization:** reads whitespace-separated swara tokens from a text file named `bhairav.txt`, appending an end-of-sequence token to each phrase.
2. **Training examples:** forms next-token prediction sequences with a context length of 16 tokens.
3. **Transformer:** uses 64-dimensional token and positional embeddings, a two-layer Transformer encoder with four attention heads, and a linear vocabulary prediction head.
4. **Training:** optimizes next-token cross-entropy with AdamW for 100 epochs in the notebook.
5. **Generation:** starts from a short swara seed and samples further tokens.
6. **Audio synthesis:** maps selected swaras to semitone offsets relative to a configurable tonic and creates a WAV file using sine waves.

The current audio conversion is intentionally simple: it uses one fixed-duration sine tone per swara. It does not model the timbre, meend, gamak, ornamentation, or expressive timing of a real instrument or vocalist.

## Important input requirement

The notebook opens `bhairav.txt`, but **that input file is not present in the repository tree**. You must provide it in the notebook's working directory before running the data-loading cell. Each non-empty line should contain one phrase as whitespace-separated tokens using the notation expected by the notebook, for example:

```text
S r G M P d N S'
S' N d P M G r S
```

This example illustrates the expected format only; use a source dataset you have permission to use, and document its provenance and license before sharing a research dataset. Token spelling must match the notation used in the generation seed and note-mapping code.

## Run in Google Colab

1. Open `Bhairav.ipynb` in Colab.
2. Upload `bhairav.txt` to the runtime, or mount storage and change the input path.
3. Select **Runtime → Run all** to execute cells in order.
4. Confirm that the training cells complete without errors.
5. The audio-generation cell writes `generated_bhairav.wav` in the current working directory. Download that file from the runtime if needed.

The notebook uses Python, NumPy, PyTorch, and SciPy. A GPU is optional for this small model; CPU execution is also possible.

## Reproducibility and current status

- The committed WAV file is an example output, not a benchmark.
- The notebook's stored cell outputs may reflect execution from different points in development. Restart the runtime and run cells in sequence when reproducing the experiment.
- Since the training text is not included, a fresh run cannot reproduce the committed output without the corresponding input data.
- There is no held-out evaluation, perplexity report, or expert assessment of raag conformity currently documented in this repository.
- The notebook contains an optional Git/GitHub upload section. It is not required to train or generate audio. Never put a personal access token in a notebook or commit a credential.

## Future work

- Include a documented and appropriately licensed swara dataset.
- Separate training and validation phrases and report token-level metrics.
- Check generated sequences against explicit Bhairav constraints and obtain musical evaluation from knowledgeable practitioners.
- Replace sine-wave rendering with a soundfont or instrument-aware synthesis pipeline.

## License

No explicit license file was identified in the repository when this README was prepared. Add a license and clarify the data license before redistributing code or training material.
