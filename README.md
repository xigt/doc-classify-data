# `doc-classify` data

This repository contains the training data used for training the [`doc-classify`](https://github.com/xigt/doc-classify) document classifier. The document classifier is used to prefilter the million+ documents obtained through an extremely broad, high-recall approach to a more manageable subset of suspected linguistic documents, which can then be used as input to the [`igt-detect`](https://github.com/xigt/igtdetect) IGT instance detector.

The serial application of these two classifiers is crucial in extending the coverage of IGT instances for the [ODIN](http://xigt.org/odin/) database. 

## What's Contained Here

This repository consists of two files:

### `doc_labels.txt`

This document contains a list of `doc_id 1|0` pairs.

* `1` corresponds to a linguistic document
* `0` corresponds to a non-linguistic document.

### `doc_urls.txt`

This document contains a list of `doc_id {URL}` pairs, where the URL is the link to the original PDF.

Only links are provided, as the copyrights for these documents are retained by the documents' copyright holders.

## How to Use This Data For Replication

The process we followed for our experiments was:

1. Download all the PDFs contained in the URL list.
2. Run [PDFlib TET](https://www.pdflib.com/en/products/tet/) to convert PDF data to TETML. <BR/>([pdfminer](https://pypi.python.org/pypi/pdfminer/) is also supported by our code, but we used TET in our experiments)
3. Use [`freki`](https://github.com/xigt/freki) to convert the TETML/pdfminer output to the `freki` output format.
4. Train the [`doc-classify`](https://github.com/xigt/doc-classify) classifier  using the training labels provided here.
5. Apply the trained model to remaining documents.