# imgbeddings

A Python package to generate embedding vectors from images, using [OpenAI](https://openai.com)'s robust [CLIP model](https://github.com/openai/CLIP) via HuggingFace Transformers. These image embeddings, derived from an image model that has seen the entire internet up to mid-2020, can be used for many things: unsupervised clustering (e.g. via [umap](https://umap-learn.readthedocs.io/en/latest/)), embeddings search (e.g. via [faiss](https://github.com/facebookresearch/faiss)), and using downstream for other framework-agnostic ML/AI tasks.

- The model is ONNX INT8-quantized, meaning it's 20-30% faster on the CPU, much smaller on disk, and doesn't require PyTorch or TensorFlow as a dependency!
- Runs on a GPU, with extra speed increases on a T4/V100 due to INT8!

## Real-World Demo Notebooks

You can read how to use imgbeddings for real-world use cases in these Jupyter Notebooks:

- [Cats vs. Dogs](examples/cats_dogs.ipynb): image clustering and building a cat/dog classifier
- [Pokémon](examples/pokemon.ipynb): most-similar image search
- [Image Augmentation](examples/augmentation.ipynb): generated embedding resilience to altered inputs

## Quick Example

More formal documentation will be added soon.

## Ethics

The [official paper for CLIP](https://openai.com/blog/clip/) explicitly notes that there are inherent biases in the finished model, and that CLIP shouldn't be used in production applications as a result. My perspective is that having better tools free-and-open-source to _detect_ such issues and make it more transparent is an overall good for the future of AI, especially since there are less-public ways to create image embeddings that aren't as accessible. At the least, this package doesn't do anything that wasn't already available when CLIP was open-sourced in January 2021.

If you do use imgbeddings for your own project, I recommend doing a strong QA pass along a diverse set of inputs for your application, which is something you should always be doing whenever you work with machine learning, biased models or not.

imgbeddings is not responsible for malicious misuse of image embeddings.

## Design Notes

- Note that CLIP was trained on square images only, and imgbeddings will pad and resize rectangular images into a square (imgbeddings deliberately does not center crop). As a result, images too wide/tall (e.g. more than a 3:1 ratio of largest dimension to smallest) will not generate robust embeddings.
- This package only works with image data intentionally as opposed to leveraging CLIP's ability to link image and text. For downstream tasks, using your own text in conjunction with an image will likely give better results. (e.g. if training a model on an image embeddings + text embeddings, feed both and let the model determine the relative importance of each for your use case)

For more miscellaneous design notes, see [DESIGN.md](DESIGN.md).

## License

MIT
